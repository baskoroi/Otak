#reference-book #computer-networking

## Chapter 1 - Primer on Latency and Bandwidth

### Importance of speed / performance
Why is speed/performance important to any online business?
- Better user engagement
- Better user retention
- Higher conversions
In some businesses/sectors where speed is ultra-important (e.g. high-frequency trading), speed can mean profits/losses of money (up to millions of dollars!)

![[Pasted image 20231127124806.png]]

### Latency and bandwidth
Two factors defining speed/performance:
- *Latency*: how long (i.e. *total time*) a packet goes from source to destination
- *Bandwidth*: maximum throughput of a logical/physical communication path

Latency itself has *four* components:
- *Propagation delay*: amount of time a packet travels from source to destination;
	- t = s/v
	- i.e the entire journey from the client (sent via WiFi) to the server (received via Ethernet), from above screenshot
- *Transmission delay*: how long it takes to push a packet into the link;
	- "link": could be WiFi path, cable, ISP as per above screenshot, etc
	- e.g. 1 Mbps vs 100 Mbps link, and a 10 Mb file:
		- it takes 10 seconds to push the entire file into a 1 Mbps link
		- and 0.1 seconds to push the entire file into a 100 Mbps link
- *Processing delay*: how long it takes to process the packet's details and whereabouts;
	- much of the processing logic is done in hardware, so the delay is usually small (but exists!)
- *Queuing delay*: how long an incoming packet is waiting in the queue until it can be processed
	- if the packets arrive faster than it can be processed, it will wait in the incoming buffer of the receiving end (server, etc.)
All those delays above sum up to the total latency between client and server.

Factors causing each delay to increase or decrease:
- distance between source & destination -> propagation delay
- link speed -> transmission delay
- number of intermediary routers -> transmission & processing delay
- traffic load along the path -> queuing delay

***Bufferbloat***: too many packets buffering in a network router or switch, causing lag. 
- bad solution: enlarge the incoming buffer
	- why bad? breaks TCP's congestion avoidance mechanism and 
- good solution: using the new active queue management algorithm (implemented within Linux 3.5+ kernels)

### Speed of light and propagation latency
Speed of light:
- c = 299,792,458 m/s (in vacuum)
- in real life: there is refractive index inside every link material that's slowing said light down 
	- fiber optic has refractive index of 1.5 (thus making speed of light = ~200,000,000 m/s)
![[Pasted image 20231127141849.png]]

Studies have shown that we humans will report lag upon a delay of > 200 ms.
- Solution: CDNs, multi-AZ servers, etc. (But sure, there are tradeoffs!)

### Last-mile latency
It's usually the last miles of a connection where latency is the greatest.
- To connect one's home/office to the Internet, signals from ISP need to be aggregated and forwarded to a local routing node.
- Hops across servers may be necessary to transmit packets from source to destination (and v.v.)
	- Can be measured using `traceroute` tool (in the past, now it's not possible)

Latency matters more than bandwidth, especially during page loads / API calls.
- Streaming a movie is bandwidth-limited, whereas page loads are latency-limited.

### Optical fiber vs metal cables
Metal cables are subject to:
- higher signal loss;
- electromagnetic interference; and
- higher lifetime maintenance costs.

Whereas for optical fibers:
- They are more often used than cables for longer-distance hops, given its faster signal propagation
- has WDM (wavelength-division mulltplexing), which helps them carry different wavelengths (channels) of light throughout the link
	- because of this, in 2010, researchers were able to multiplex 400 wavelengths with peak capacity of 171 Gbit/s per channel -> > 70 Tbit/s of total bandwidth for a single fiber link!

### Bandwidth at the network edge

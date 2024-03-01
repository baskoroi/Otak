#reference-book #system-design

## Chapter 1 - Reliable, Scalable, and Maintainable Applications

### Introduction
- Data-intensive app (DIA) vs compute-intensive app:
	- Compute-intensive: CPU power = bottleneck
	- Data-intensive: data influx = bottleneck -> amount of data (volume), complexity of data (variety), speed at which it comes into system and changes (velocity)
- Building blocks (i.e. data systems / DSs) of a DIA:
	- database(s)
	- cache(s)
	- search indexes
	- stream processing
	- batch processing
- Oooh, look at this special-purpose composite DS, built of smaller general-purpose DSs!
	![[Pasted image 20240115163134.png]]
- **All building blocks = data systems!** (regardless of their commonalities/similarities and differences). Why?
	- Boundaries between data system categories blur.
		- e.g. Redis = database with pub-sub capability, Kafka = pub-sub with database durability
	- DIAs have demanding/wide-ranging requirements, such that a single data system can no longer satisfy all of said requirements.
		- DIAs break down tasks -> each task is done efficiently on a single DS -> application code stitch together the DSs and their results
- By creating this composite data system -> we are not only app developers, we are also data system designers!
	- Some guarantees need to be made, e.g. cache invalidated as soon as data is edited, 
	- Many questions / concerns arise, three of which are most important:
		- **Reliability:** how well the system runs, even when things go wrong?
		- **Scalability:** how stable is the data processing when load increases?
		- **Maintainability:** how easy is it to maintain/evolve the system, given newer requirements?
### Reliability
- Things that go wrong = faults.
- Systems that can cope with faults: fault-tolerant / resilient.
- Fault vs failure:
	- Fault: component / data deviating from its spec.
	- Failure: the system as a whole stops providing service.
- We cannot reduce the probability of a fault to zero, but we can create *fault-tolerant* systems.
	- Even more interestingly, we can do something like Netflix's Chaos Monkey:
		- i.e. induce more faults to challenge our system and from there create mechanisms to correct it when those faults occur.
- Types of faults:
	- **Hardware faults:**
		- e.g.: hard disk crash, hard disk MTTF (mean time to failure), faulty RAM, power blackout, network fluctuations
		- Solutions:
			- Multi-machine redundancy -> overkill for small apps
			- Cloud platforms -> increase cost and failure probability (since more machines get involved in processing)
			- S/W fault-tolerance mechanisms of entire machines -> more advantageous.
	- **Software faults:**
		- Hardware vs software faults:
			- Hardware faults = random / independent of each other component
			- Software faults = systematic, harder to anticipate, higher probability of system *failures* due to correlation across nodes
		- Software faults tend to not occur until an unusual set of circumstances cause it.
		- There's no quick solution, just:
			- rethinking assumptions and system interactions,
			- thorough testing,
			- process isolation,
			- enabling restart upon (sub-)system crash,
			- monitoring and analyzing production system behavior
	- **Human errors:**
		- Human errors are inevitable, given human flaws/imperfection.
		- Solutions:
			- Minimize opportunities for error;
			- Decouple environments/components, e.g. prod vs stg;
			- Test thoroughly at all levels, e.g. unit tests, integration tests, QA/manual tests, automated tests;
			- Allow quick & easy recovery from human errors;
			- Set up detailed monitoring, e.g. performance metrics, error rates
			- Apply good management practices
- Why is reliability important?
	- Reliability is important in both mission-critical systems (nuclear power plants, air traffic control software) and smaller businesses
	- Loss of reliability = loss of $, business problems, disturbed productivity, radiation, large accidents, etc.
	- There are some situations where we sacrifice reliability to reduce development cost or operational cost -- but be very careful in taking such decisions.
### Scalability
- Scalability = a system's ability to cope with increased load.
#### Load parameters
- Load parameters: *quantitatively* describe the load
	- e.g. Requests/sec to a web server, reads to writes ratio in DB, number of concurrent users in a chatroom, hit rate on a cache
	- Choose the parameters based on your system architecture
##### **Case study: Twitter**
- Twitter has two main operations: (per Nov 2012)
	- **Post tweet** (avg: 4.6k requests/sec, max: 12k requests/sec)
		- Hard not because of 12k reqs/sec, but because of fan-out.
			- Fan-out: how many requests to other services make in order to serve one request.
				- In Twitter's case = each user follows many people, and each user is followed by many people.
				- Refer to fan-out in electronic engineering
	- **Home timeline** (300k requests/sec)
- Possible solutions for post tweet:
	- Insert tweet to DB as usual, and load the tweets from users the current user follows (i.e. followees).
		- Faster writes, slower reads.
	- Maintain cache for each user's home timeline
		- A new tweet is posted? Add to said cache.
		- Faster reads, fast but *TOO MANY* writes.
			- What if Justin Bieber (with 20m followers) wanted to post a tweet?
#### Describing Performance
- Two questions when investigating effect of increased load:
	- Increase a load parameter -> Keep the system resources (CPU, memory, network bandwidth) unchanged -> How much is the performance affected?
	- Increase a load parameter -> How much resources to increase to maintain same performance?
- Both questions need performance *numbers*/metrics
	- Examples:
		- throughput (number of records to process per second)
		- response time (duration between a client sending a request and receiving a response)
			- latency <> response time
				- latency -> the time a request waits to be processed
				- response time -> already includes network delays
##### Response time
![[Pasted image 20240118150531.png]]
- Response time = not a number, but a distribution of values.
	- mean vs median: choose median
		- Why? mean does not represent how many users "suffer" a certain response time
			- Why? 

## Chapter 2 - Data Models and Query Languages

Note here...
## Chapter 3 - z
#reference-book #system-design

## Chapter 1 - Reliable, Scalable, and Maintainable Applications

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
	- Hardware faults:
		- e.g.: hard disk crash, hard disk MTTF (mean time to failure), faulty RAM, power blackout, network fluctuations
		- Solutions:
			- Multi-machine redundancy -> overkill for small apps
			- Cloud platforms -> increase cost and failure probability (since more machines get involved in processing)
			- S/W fault-tolerance mechanisms of entire machines -> more advantageous.
	- Software faults:
		- 
	- Human error:
## Chapter 2 - Data Models and Query Languages

Note here...

## Chapter 3 - z
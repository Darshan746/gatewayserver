Spring cloud sleuth

	provide a spring boot auto configuration for distubuted tracing
	
	it add a trace and span ids to all the logs, so you can just extract from a given trace or span in a log aggregator
	
	it does this by adding the filters and interacting with the other spring component to let the correlation ids being generated pass through to all the system call
	
	
	Spring cloud sleuth will add three pieces of information  to all the logs written by microservices
		<App-name>,<Trace-Id>,<Span-id>

<Application-name> this is going to be the application name where the log entry being made 

Spring cloud sleuth get this name from the spring.application.name property

Trace-Id: it is equivalant to the correlation-id ,its a unique number that represent an entire transaction

Span-id: it is a unique ID that represent a part of overall transaction , Each service participating within the transaction will have its own span-Id
Span-id are particularly relevant when you integrate with zipkin to visualize your transactions




Zipkin
------

Zipkin is a opensource data visualization toolthat can help aggregating all the logs and gather timing data needed to trouble shoot latency problem in microservices architectures


It allows us to break the transactions down into its component pieces and visually identify where there might be a performance hotspot  

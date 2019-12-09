# ANT309-R1 - [REPEAT 1] Responding to customer needs in real time with Amazon MSK

How things were in the 80's:
	- 

Data Flywheel:
	- Data Collected -> Data Analyzed -> Applications Evolve -> Happier Customers

"Datasphere Growth" 61% YoY
	- IOT is a major contributor
		- 90ZTB by 2021
		- 30% of data will be analyzed in real-time

"Data Reactivity"

Why process data in real-time:
	- Wow customers
	- Threats
		- Instrumeting telemtry in network to respond to anomalies
	- Environmental changes
	- Timely decisions
	- Boost agility

Foundation of real-time analytics system:
	1. Data can be produced, captured, and process in milliseconds
	2. Data is buffered, enabling parallel and independent I/O
	3. Data must be captured and processed in the order it was produced.

Data streams are for real-time:
	- Commit log
		- Record of events that were produced by a producer
	- Producers and cosumers are decoupled
	- Data is retained, not destroyed
	- Write order is preserved
	- Produce -> consume in milliseconds
	- Logical grouping of "partitions" or "shards"

Current Trends:
	- Data streams being used for messaging
	- Replacing batch workflows to lower latency
	- Event "spinal cord" for micro-services
	- Database integrations are happening via change streams
	- In-stream machine learning and AI for real-time automation

2 AWS Data Streaming Services:
	- Kinesis
	- MSK

Kafka:
	- Performant
		- Gigabytes per second, 10ms p99
	- Open source
	- Versatile
	- Lots of framework integration
		- Flink
		- Spark
	- Challenges:
		- Difficult to setup + scale
			- Zookeeper
		- Hard to achieve high availability
		- No console, no visible metrics
		- Hard AWS integrations

MSK:
	- Fully managed production ready Apache Kafka cluster
	- Real-deal, not a fork
	- Global availability
	- Security
	- Least expensive managed Kafka provider
	- 100 brokers per MSK cluster

Example:
	- Publish JMX data into something like Prometheus
	- Integrations now to export metrics via MSK into 3rd party providers (like Datadog)

Flink integration with MSK clusters + EC2 Kafka clusters

Adobe Use-Case:
	- Scale:
		- 100B messages per day
		- 200 Kafka Brokers
		- 25,0000 topics
		- 288k partitions
		- 15 data centers
	- Adobe Experience/Marketing Platform
		- Capture millions of customer interaction data (on the edge) in real-time
		- Generate customer profile
		- ML and AI attribution scores
		- Proprietary Kafka pipeline called "data power grid"
			- Integrate services
			- Enrich data in real-time
			- Features:
				- REST API to produce and consume:
					- Firewall friendly
					- Language agnostic
				- Intelligent routing
					- Message-based routing
					- Topic-based routing
				- Message Filtering
					- Filter events on server side
					- Flexible filtering criteria
					- Messages filtered according to permissions
			- Cross polenation of messages across regions (messages are replicated by "Mirror Makers")
		- Stream Processing
			- Kafka Connect for source and sink connectors
			- Stream processing using Flink
			- Event filtering, transformations, and branching
		- <Insert images>
			- Cluster replication for proteting main Kafka pipeline
		- Spinnaker tool helping them get close to one click deployments
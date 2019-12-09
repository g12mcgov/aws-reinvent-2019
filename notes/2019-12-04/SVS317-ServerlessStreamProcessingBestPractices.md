# Stream Processing

What is Streaming?
	1. High volume
	2. Continuous
	3. Ordered, incremental
	4. Low latency

Popular because:
	- Batch vs. Stream Processing (real time metrics, real-time spending alerts/caps, etc...)

Serveless operational model
	- No provisioning
	- Automatic scaling
	- Pay for value

Amazon Kinesis
	- Data streams
	- Data analytics
	- Data Firehose
	- MSK (Managed streaming service for Kafka)

4 Key stages:
	1. Ingestion (and buffer)
		- 2 services:
			- Data streams
				- Need consumer (they would "fall off the stream")
			- Data firehose
				- Deals with delivery
					- No consumer
				- Define and configure what destination you want to right to.
		- When use one vs the other?
			- Data streans -> low latency (less than 1 second) - custom processing per incoming record
			- Firehouse - 60s latency
		- Write to them via many sources
			- SDK
			- API
			- Kinesis Agent
			- Kinesis Producer Library (KPL)
			- 3rd party and open source
				- Log4k
				- Kafka
		- Best Practices:
			- Optimizations
				1. End-to-end latency
					- Be mindful of per-shard max record and throughput limits
					- Auto-scaling of shards
				2. Overall cost
					- Buffer and batch
					- Compression and encoding of messages
	2. Process
		- Kinesis:
			- AWS Kinesis Data Analytics
			- Spark
			- Flink
			- AWS Kinesis Client Library
		- AWS Lambda
			- No servers to manage
			- No stream consumption costs when no new records to process
			- Execution Models:
				- Synchronous (push)
				- Asynchronous (event)
				- Poll-based
			- Example:
				- Producer emitting data
				- Lambda polling each shard once per second
				- Can subscribe up to 5 lambda functions to a single stream (fan-out)
			- Ehanced pan-out
				- Change from polling shards to pushing to the lambda service
			- Batching is good for consumers as well
			- Retrying batches / messages
				- Can configure / customize failure/retry behavior on lambda
					- On failure destination -> Send records to Amazon SNS or Amazon SQS
			- Does not make sense for:
				- Stateful stream processing (such as windowed aggregations)
				- Buffering large voumes of streaming data before writing elsewhere
			- Best Practices:
				1. Retry/failure handling
				2. Optimizations for end-to-end latency
					- Ehanced fan out for futher scale with sub-second latency
				3. Optimizations for overall cost
	3. Store
		- Journey to datalake
			- S3 = great
			- Athena for querying (like on top of S3)
			- Data Firehose for writing into S3.
			- Lookup: ORC and Parquet
		- Best Practices:
			1. Optimizations for long-term usability of data
			2. Optimizations for overall cost
	4. Analyze
		- QuickSight for visualization
		- SageMaker
		- Data Analytics
			- Real time analytcs on the data when it's in the stream:
				1. SQL
					- Windows -> emits a new stream for that window
				2. Apache Flink Java written program)

Comcast X1:
	- Canary score = release validity check
		- Metrics:
			- Heap size
	- Lambda execution context - do expensive operation (like establishing connection to a Redis cluster just once - save it for future invocations)
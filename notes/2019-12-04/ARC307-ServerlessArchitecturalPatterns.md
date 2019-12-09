# ARC307-R2 - [REPEAT 2] Serverless architectural patterns and best practices


* PDF example - Serverless CI/CD for enterprise

* Jeremy Daley

* Lambda memory tuning

* Saga - things failed, retry. Basically a state machine

* Patterns:
	- "Comfortable REST"
		- Basic:
			- API gateway -> Lambda -> DynamoDB
		- Operations:
			- AWS X-Ray
			- Amazon CloudWatch Logs & Metrics
		- Reliability:
			- Rate limit
		- Security:
			- Amazon Cognito
			- AWS Secrets Manager
		- Performance:
			- On-demand tables support uo to 40k read/write request units
		- Cost:
			- Power tuning to tune cost
	- "Cherry Pick"
		- Operations:
			- GraphQL API
			- AWS AppSync
			- AWS Step Function
				- State machines for long transactions
				- Retry / handle failures on Lambda functions
		- Security:
			- Enforce authorization at the API, data, field and operation level
		Peformance:
			- Use purpose-built databases
		- Cost:
			- Enable caching (new)
				- Cache resolvers
				- Cache data from a particular field of JSON key
		![](../../images/2019-12-04/ARC307-ServerlessArchitecturalPatterns_1.png)
	- "Call Me Maybe" (Webhook)
		- Operations:
			- Limit concurrency of lamdbda function if overwhelming database (or other downstream services)
		- Reliability:
			- Kinesis as a buffer + a better mechanism to concurrency.
			- Lambda destinations for failed requests
			- AWS DLQ
		- Security:
			- Enforce authorization and obfuscate senstive data on the stream (contains a key, field, etc...)
		- Performance:
			- For low-volume traffic, Kinesis can batch records for up to 5 minutes
		- Cost:
			- Amazon SQS + DynamoDB to easily scale webhooks
	- "Big Fan" (Fan-out)
		- Operations:
			- API gateway can integrate with AWS services directly
		- Reliability:
			- AWS SNS + DLQ (higher durability, batching, etc)
		- Security:
			- Enforce authorization, verify signature of Amazon SNS messages
		- Performance:
			- Use message filtering for efficient processing to limit fan-out to consumers
		- Cost:
			- Compress and aggregate messages when possible
			- Consider Kinesis for larger payloads
	- "I'm a Streamer" (Streaming)
		- Operations:
			- Kinesis
			- Enable source stream record backup
		- Reliability:
			- Favor dedicated firehouse per context/domain
		- Security:
			- Enforce authorization
			- Obfuscate data / remove sensitive data
		- Performance:
			- Paquet transformation -> glue for discovering data schema -> athena to query
		- Cost:
			- Use message filtering to prevent unwanted events. Tune buffer/compression
	- "The Strangler"
		- Operations:
			- API Gateway (hides implementation details)
			- Centralize logs, metrics, and distributing tracing
		- Reliability:
			- Use a corporate load ablancer virtual IP to send traffic to
		- Security:
			- Enforce authorization
		- Performance:
			- Gradually shift functionalities to newer computer/database platforms
		- Cost:
			- Use serverless for new functionalities
		- HSBC Example
			- Notification lambda function that converts message into iOS, Android, etc format
			![](../../images/2019-12-04/ARC307-ServerlessArchitecturalPatterns_2.png)
	- Summary:
		- - Operations = understand the health and lifecycle of your application
		- - Reliability = build resiliency and protect non-serverless resources
		- Security = Focus on managing boundaries and AppSec
		- Performance = Optimize for low, steady, and/or peaks
		- Cost = Factor in developent, people, opportunity, and maintenance cost

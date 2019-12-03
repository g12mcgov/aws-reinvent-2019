# Process Data Using Cloud Databases and Serverless Technologies

Amazon Quicksight:
	- Cloud based BI tooling / visualization

AWS DMS & AWS SCT:
	- Data migration
	- Schema transformation
	- Hetergoenous DB migrations
	- Warehousing

Serverless:
	- Amazon Aurora
		- Shut down / boot up on demand
		- Use Cases:
			- Infrequently used applications (blogs)
			- Sporadic load behavior
		- Includes endpoint for querying + load balancer
	- Amazon Glue
		- ETL jobs
		- 3 components:
			1. Data catalog
			2. Job authoring
			3. Job execution
		- Serverless Spark platform
	- Amazon Athena
		- Based off of Presto
		- Query manager
			- Can query S3
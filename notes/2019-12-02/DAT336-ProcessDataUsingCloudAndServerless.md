# DAT336 - Process data using cloud databases and serverless technologies

* Amazon Quicksight:
	- Cloud based BI tooling / visualization

* AWS DMS & AWS SCT:
	- Data migration
	- Schema transformation
	- Hetergoenous DB migrations
	- Warehousing

* Serverless:
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

* Lab:
	- VPC Id: vpc-03cb74ce9940c9d93
	- SourceEC2EndpointDNS: ec2-52-211-48-36.eu-west-1.compute.amazonaws.com
	- TargetAuroraEndpointDns: reinvent2019-auroradestinationdbcluster-v8suikmqztrl.cluster-c9kgcybfxdxl.eu-west-1.rds.amazonaws.com
	- Target S3 Bucket Name: reinvent2019-targets3bucket-1k7gk6z6djuda	


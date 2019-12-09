# DAT209-L - Leadership session: AWS purpose-built databases

* Why are there so many DBs in industry?
	- Main frame
	- Client server
	- 3 tier architecture
	- Microservice architecture

* Common Database Categories:
	1. Relational
	2. Key Value
		- Ride sharing app example (high scalibility)
	3. Document
		- Don't want to deal with schema management
	4. In-Memory
		- Online video game example w/ leaderboard
			- Would never do full table scan
	5. Graph
		- Highly connected data
		- Shoe store example w/ recommendations
	6. Time-Series
		- Amazon TimeStream
		- Vibration, temperature
		- What makes time-series DB?
			- Access strictly by time
			- No updates, only inserts
			- Compression etc
	7. Ledger
		- Once written to, can never be updated
	8. Wide Column

* Top of mind for customers:
	- Move to fully managed
		Services:
			- RDS
			- Aurora
			- ElasicCache
			- DocDB
		Tools:
			- SCT
			- DMS
		Programs:
			- MAP (Migration Acceleration Program)
			- ProServe
			- Partner
			- DB Freedom (Reducing risk + accelerating migrations)
	- "Break free"
		- Commercial system to OpenSource server
	- New modern apps
		- Micro-services from the get-go
		- Loosely coupled
		- Highly distributed

* Lyft + DynamoDB:
	- Storing GPS locations particular to your ride
		- Key is ride (user)
		- Horizontally scalable, single digit millisecond performance

* ZipRecruiter + Amazon Aurora & Amazon RDS:
	- Need for rich query-set
		- Cannot use something like DynamoDB where query is known up-front

* Liberty Mutual + DocumentDB:
	- JSON structure representing insurance policies for customers
	- Need for flexible data model

* DynamoDB vs. DocumentDB:
	- DynamoDB = known access pattern w/ bottomless scale
	- DocumentDB = evolvable data model but unknown queries

* UbiSoft + ElastiCache:
	- Optimized for latency over durability - microseconds vs. milliseconds
	- Optimized datastructures (sorted set, for example)

* Nike + Neptune (Graph Databases):
	- Connections between things like Athlete, Skill, Fan, Sport

* Klarna + Amazon QLDB (Ledger):
	- Journals
	- Examples: Banking systems, transactions, etc
	- Typically done with relational databases + access control + auditing (relying on one database to keep track of the other database)
	- Cryptographic verfication (SHA256) hashes to verify things have not changed in the ledger
		- Trusting the hash key

* Fender:
	- Migrated from SQL Servers to a collection of different AWS products (DynamoDB, S3, etc...)

* Database Management:
	- Challenging to manage large-scale Cassandra cluster at scale
	- Amazon Managed (Apache) Cassandra Service (MCS)
		- Serverless

* Athena Federated Query:
	- Run queries against many data stores
	- Can write own connectors for interacting with other data stores

* Machine Learning:
	- Select and train the model
	- Write app code to read from DB
	- Query and format data for ML algo
	- Call ML service to run algo
	- Format output

* Aurora Integration with ML:
	- Integrations with Athena, SageMaker
	- Interaction with AWS ML services inside SQL
		- Example of querying a table, then running a column through sentiment analysis, returned in a new table
	![](../../images/2019-12-03/DAT209-L-AwsPurposeBuiltDatabases.png)


## ANT325-R - [REPEAT] Slow queries? Understanding the nuances of slow queries - Drew Baugher (Amazon) - dbbaughe@amazon.com

Coordinator nodes:
	- Every one has cluster state (copy - can be stale)

2 Search Types:
	- Query
	- Fetch

Scatter Phase
	- Fan out query to shards that matter
	- Return just IDs

Gather Phase
	- Accumulate data from global top hits (just IDs at this point)

Size:
	- 10 to 50GB per shard recommended

Scripting:
	- Very bad performance

Segments:
	- Low-level Lucene datastructure
	- Large number == slow queries

"Force merge" - Merges shards on one or more indices
	- Don't do it when active writes are happening

Refresh Interval:
	- Time before your ingested documents become searchable
	- Moving between in-memory buffers to actual search data structures in Lucene
	- Set to -1 if no need to refresh data
		- Not ingesting documents anymore into that index
	- Default is 1 second

Caches:
	- 3 caches
		 - File system
		 - Node cache
		 	- Every index / node on that index shares it
		 	- LRU
		 - Shard cache
		 	- Spefifically for shard
		 	- Keeps around most commonly used
		 - Cache key is the JSON body
		 	- Ordering matters in the JSON (out-of-order lists will cause cache miss)
	- API for cache
		- /request_cache
		- Can also clear cache

Indeces can be sorted but only at creation

Profile API:
	- Send "profile" in query body

Slowlogs:
	- Query

Task API:
	- Queries that are hanging
	- All tasks being executed on the cluster

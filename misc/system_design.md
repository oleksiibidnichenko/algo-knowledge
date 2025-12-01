## System design notes
### Generic plan
1. Clarify what part of the design task should we focus on (particular feature, maybe the high level structure)
2. Clarify functional and non-functional requirements
   2.1. Functional requirements: what should the app do (e.g. for OTA it should update Linux, support delta update etc.);
   2.2. Non-functional requirements - the following params have to be considered:
        2.2.1. scalability - how many users/devices/operations per second should be handled?
        2.2.2. performance - how fast do we have to perform functional ops?
        2.2.3. data throughput - traffic / number of CPU cores, amount of RAM;
        2.2.4. availability - can the system be down and for how long? Also should we be "Fail-open" or "Fail-closed"?
        2.2.5. fault tolerance - specific implementation techniques, backup strategies etc.

### Example of data throughput calculation (Twitter based example)
Everything here is based on either assumptions or on inputs that we will get from the clarification
of non-functional requirements.
1. Twitter database has 100M active users;
2. On average a single user reads 100 tweets;
3. On average a single user writes 5 tweets per day;
4. Average size of a single tweet is 1 Mb;
5. Traffic calculation:
   5.1. Server outbound (reads): 10B tweets a day, or ~112K tweets a second, or 100 Gb a second;
   5.2. Server inbound (writes): 500M tweets a day, or ~6K tweets a second, or 6 Gb a second;

Note: a day has 86000 seconds

### Approximate time for different memory access ops.
- L1 cache access: 1ns;
- Branch mispredict: 3ns;
- L2 cache access: 4ns;
- mutex lock/unlock: 17ns;
- main memory (RAM): 100ns;
- SSD random access read: 16000ns;
- packet round trip within the same data center: 0.5ms;
- packet round trip CA to Netherlands: 150ms.

### HTTP error codes
**2xx - Success**
- 200 OK - Request succeeded
- 201 Created - Resource was created
- 202 Accepted - Request accepted for processing
- 204 No Content - Request succeeded but no content to return

**3xx - Redirection**
- 301 Moved Permanently - Resource permanently moved
- 302 Found - Resource temporarily moved
- 304 Not Modified - Cached version is still valid

**4xx - Client Error**
- 400 Bad Request - Invalid request syntax
- 401 Unauthorized - Authentication required
- 404 Not Found - Resource not found
...

**5xx - Server Error**
- 500 Internal Server Error - Generic server error
- 502 Bad Gateway - Invalid response from upstream server
- 504 Gateway Timeout - Upstream server timeout

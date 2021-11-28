# OneBrick System Design

![onebrick system design](https://github.com/ahrezaldy/onebrick-sysdes/blob/master/OneBrick%20System%20Design.pdf)

### Service 1 (Crawler)
- This service main purpose is to crawl data from 3rd party / external source, as many as they can, and save the raw data to internal database.
- The database better use NoSQL, because the data could be different between each source, and also prone to change in the future.
- Example data: foreign exchange, stock market

### Service 2 (Data Processor)
- This service main purpose is to process / aggregate data from Service 1 & Service 3 (explained later), so we will have better data structure for our client / app.
- Also can be used for analytic purpose.
- The database better use relational database, since we also need to save sensitive data (e.g: transaction data).

### Service 3 (Controller)
- This service will provide API for our client / app.
- Behind the API, this service could be calling external source directly or getting record from our database, depending of the case.
- Example case for calling external source directly: balance data from bank, since we will tightly depend on bank for this data.
- Example case for getting record from our database: transaction data, we should record all transaction happened in our platform.
- This service also can utilize cache to reduce database load & also for faster data I/O. For example: we no need to call aggregated stock past data repeatedly. The data will be always same for every request, so we no need to bother database for that. We can save that kind of data in cache.

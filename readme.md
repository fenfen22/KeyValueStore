Key-value stores are ont of the simplest forms of database.

The map cpntainer from the C++ STL is a key-value store, like the hashmap in java, and the dictionary in python.

Key-value stores generally share the following interface:
(1) Get(key): get some data previously saved under the identifier "key", or fail if no data was stored for "key"
(2) Get(key, value):store the "value" in memory under the identifier "key", so we could access the value later referencing the same "key". If some data was already present under the "key", this data would be updated.
(3) Delete(key): delete the data that was stored under the "key"

Most underlying implementations are either hash tables or some kind of self-balancing trees, like B-trees or Red-balck trees. Sometimes, the data is too big to fit in memory, or the data must be persisted in case the system crashed for any reason. In that case, using the file system becomes mandatory.

NoSQL(Not only SQL)
1. do not use the SQL query language
2. may not provide full support of the ACID paradiam (atomicity, consistency, isolation, durability)
3. may offer a distributed, fault-tolerant architeture

Unlike relation databases, key-value stores have no knowledge of the data in the values, and do not habe any scheme like in MySQL or PostgreSQL. This is mean that it is impossible to query only part of the data by doing any kind of filtering, as it can be done in SQL with the WHERE clause. If we don't know where to look for, we have to iterate over all the keys, get their corresponding values, apply whatever filtering that you need on those values, an keep only the ones you need. This could be very computationally intensive.

This key-value store that is using the file system for permanent storage and which offers a networking interface would cover the whole range of topics list above. This project that deal with all domains of back-end engineering.

The performance of key-value stores depeends on:
1. the hardware
2. the file system being used
3. the actual application and order in which the keys are being accessed
4. the data set, and in particular the lengths of keys and values and the possibility for key collisions when hash talbe are used.

Here are points that could make this key-value store project stand out from the crowd:
1. adapt to a specific data representation (graphs, geographic data, etc)
2. adapt to a specific operation (performing very well for reads only, or writes only)
3. adapt to s apecific issue （automatic parameter tuning, as many key-value stores have many options, and it's sometimes a mess to find the best ones）
4. offer more data access options, for instance in levelDB, data can be accessed forward or backward, with iterators, ad it has sorting on the keys. Not all key-values stores can do that.

The goal of this project is to develop a lightweight key-value store in understandable C++ code. 
1. use hash table for the underlying data structure
2. the data will be persistent on disk
3. a network interface will also be implemented
4. will not run for absolute speed, but for conciseness and clarity in both design and implementation
5. minimize the memory footprint of the database file on disk


Analysis about Kyoto Cabinet and LevelDB

key-value stores have very similar components:
1. interface: the set of methods and classes exposed to the clients of a key-value store so they can interact it (API)   Get(), Put(), Delete()
2. Parametrization: the way that options are being set and passed to components across the whole system.
3. Data storage: the interface used to access the memory where the data, i.e. keys and values, are stored. If the data must be persisted on non-volatile storage such as hard drive or flash memory, then problems of synchronization and consurrency may arise.
4. Data structure: the algorithms and methods being used to organize the data, and allow for efficient storage and retrieval. (a hash table or B+ tree, a Log-Structured Merge Tree (LevelDB) )
5. Memory management: the algorithms and techniques being usd to manage the memory used by the system.
6. Iteration: the way by which all the keys and values in a database can be enumerated and accesses sequentially. The solution are mostly iteration and cursors.
7. String: The data structure used to represent and access strings of characters. For key-value stores, a great deal of time is being on passing and processing strings. std::string from the STL might not be the best solution.
8. Lock Management: 
9. Error Management
10. Logging
11. Transaction Management: Mechanism over a set of operations which ensures that all the operations are executed correctly. None of the operations is exectuted and database is left unchanged in case of an error.
12. Compression: algorithms used to compress the data
13. Comparators: provide ways to order two keys with regard to each other
14. Checksum: used to test and ensure the integrity of the data.
15. Snapshot: provides a read-only view of the entire database as it was when the snapshot was created.
16. Partitioning: referred to as Sharding, this consists in splitting the data set into multiple data storages, possibly distributed across multiple nodes a network.
17. Replication: In oder to ensure durability in case of system or hardware failure, some key-value stores allow for multiple copies of the data, - or of partitions of the data - to be maintined simultaneously, preferbly on multiple nodes.
18. Testing Framework: used to test the system, including unit and integration testing.
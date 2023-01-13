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
3. adapt to s apecific issue
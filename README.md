## CPRE 563: Advanced Data Storage Systems Final Project 
This is a fork of the original RocksDB (https://github.com/facebook/rocksdb).
An implementation of a compression-aware compaction mechanism is implemented in this project. Originally detailed in a survey [Jarnilla et al.], the compaction mechanism in question is simply an injection of some influence of the compression ratio. In general, it can be described as compaction ratio = (100/R) * N. The method of testbenching used in this project was db_bench. A couple relative db_bench calls can found below and the in our final project report /TODO: Link report. A function to determine the compact ratio of SST files dynamically during the db_bench as well. This compaction mechansim was also designed to work with a ScaleFlux CSD 3000. To do so, we have created a simple function to determine the CSD's compression ratio by invoking and parsing sfx-cap-info. More details can be found in our final report. /TODO: Link report

An example of a relavent db_bench call:
```
sudo ./db_bench --db=/home/path/to/test.db --benchmarks=fillrandom,stats --num=2000000 --key_size=16 --value_size=4096 --compression_type=none --stats_level=5 --stats_per_interval=1 --statistics=1 --disable_wal=true --compression_ratio=1 --seed=1745714556555094 --perf_level=3 2>&1
```
- Benchmarks set to fill with random keys and record statistics (We used the same seed across testbenches to ensure consistency during testing - more in our report)
- 2 GB size with key size of 16 and a value size of 4 kb
- No compression type (As we were using the ScaleFlux CSD, we wanted to use the transparent compression instead of invoking software compression)
- Output maximum statistic details (level 5) at performance level 3

- Jaranilla, C., & Choi, J. (2023). Requirements and Trade-Offs of Compression Techniques in Key–Value Stores: A Survey. Electronics, 12(20), 4280. https://doi.org/10.3390/electronics12204280 

Below is a copy of the README.md from the original RocksDB github

## RocksDB: A Persistent Key-Value Store for Flash and RAM Storage

[![CircleCI Status](https://circleci.com/gh/facebook/rocksdb.svg?style=svg)](https://circleci.com/gh/facebook/rocksdb)

RocksDB is developed and maintained by Facebook Database Engineering Team.
It is built on earlier work on [LevelDB](https://github.com/google/leveldb) by Sanjay Ghemawat (sanjay@google.com)
and Jeff Dean (jeff@google.com)

This code is a library that forms the core building block for a fast
key-value server, especially suited for storing data on flash drives.
It has a Log-Structured-Merge-Database (LSM) design with flexible tradeoffs
between Write-Amplification-Factor (WAF), Read-Amplification-Factor (RAF)
and Space-Amplification-Factor (SAF). It has multi-threaded compactions,
making it especially suitable for storing multiple terabytes of data in a
single database.

Start with example usage here: https://github.com/facebook/rocksdb/tree/main/examples

See the [github wiki](https://github.com/facebook/rocksdb/wiki) for more explanation.

The public interface is in `include/`.  Callers should not include or
rely on the details of any other header files in this package.  Those
internal APIs may be changed without warning.

Questions and discussions are welcome on the [RocksDB Developers Public](https://www.facebook.com/groups/rocksdb.dev/) Facebook group and [email list](https://groups.google.com/g/rocksdb) on Google Groups.

## License

RocksDB is dual-licensed under both the GPLv2 (found in the COPYING file in the root directory) and Apache 2.0 License (found in the LICENSE.Apache file in the root directory).  You may select, at your option, one of the above-listed licenses.

---
title: "Choosing a Backend"
description: ""
project: "riak_kv"
project_version: "2.9.0p5"
menu:
  riak_kv-2.9.0p5:
    name: "Choosing a Backend"
    identifier: "planning_choose_backend"
    weight: 102
    parent: "planning"
toc: true
aliases:
  - /riak/2.9.0p5/ops/building/planning/backends/
  - /riak/kv/2.9.0p5/ops/building/planning/backends/
  - /riak/2.9.0p5/setup/planning/backend/
  - /riak/2.9.0/setup/planning/backend/
  - /riak/kv/2.9.0/setup/planning/backend/
  - /riak/kv/2.9.0p1/setup/planning/backend/
  - /riak/kv/2.9.0p2/setup/planning/backend/
  - /riak/kv/2.9.0p3/setup/planning/backend/
  - /riak/kv/2.9.0p4/setup/planning/backend/
---


[plan backend bitcask]: {{<baseurl>}}riak/kv/2.9.0p5/setup/planning/backend/bitcask
[plan backend leveldb]: {{<baseurl>}}riak/kv/2.9.0p5/setup/planning/backend/leveldb
[plan backend memory]: {{<baseurl>}}riak/kv/2.9.0p5/setup/planning/backend/memory
[plan backend multi]: {{<baseurl>}}riak/kv/2.9.0p5/setup/planning/backend/multi
[plan backend leveled]: {{<baseurl>}}riak/kv/2.9.0p5/setup/planning/backend/leveled
[dev api backend]: {{<baseurl>}}riak/kv/2.9.0p5/developing/api/backend

Pluggable storage backends are a key feature of Riak KV. They enable you to
choose a low-level storage engine that suits specific operational needs.
For example, if your use case requires maximum throughput, data
persistence, and a bounded keyspace, then Bitcask is a good choice. On
the other hand, if you need to store a large number of keys or to use
secondary indexes, LevelDB is likely a better choice.

The following backends are supported:

* [Bitcask][plan backend bitcask]
* [LevelDB][plan backend leveldb]
* [Memory][plan backend memory]
* [Multi][plan backend multi]
* [Leveled][plan backend leveled]

Riak KV supports the use of custom storage backends as well. See the
storage [Backend API][dev api backend] for more details.

Feature or Characteristic                      |Bitcask|LevelDB|Memory|Leveled|
:----------------------------------------------|:-----:|:-----:|:----:|:----:|
Default Riak KV backend                        |✓      |       |      |      |
Persistent                                     |✓      |✓      |      |✓     |
Keyspace in RAM                                |✓      |       |✓     |      |
Keyspace can be greater than available RAM     |       |✓      |      |✓     |
Keyspace loaded into RAM on startup<sup>1</sup>|✓      |       |      |      |
Objects in RAM                                 |       |       |✓     |      |
Object expiration                              |✓      |       |✓     |      |
Secondary indexes                              |       |✓      |✓     |✓     |
Tiered storage                                 |       |✓      |      |✓     |

<sup>1</sup> Noted here since this can affect Riak start times for large
keyspaces.
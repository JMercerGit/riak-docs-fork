---
title: "PBC Data Type Counter Store"
description: ""
project: "riak_kv"
project_version: 3.0.14
menu:
  riak_kv-3.0.14:
    name: "Data Type Counter Store"
    identifier: "pbc_dt_counter_store"
    weight: 117
    parent: "apis_pbc"
toc: true
aliases:
  - /riak/3.0.14/dev/references/protocol-buffers/dt-counter-store
  - /riak/kv/3.0.14/dev/references/protocol-buffers/dt-counter-store
---

An operation to update a [counter]({{<baseurl>}}riak/kv/3.0.14/developing/data-types).

## Request

```protobuf
message CounterOp {
    optional sint64 increment = 1;
}
```

The `increment` value specifies how much the counter will be incremented
or decremented, depending on whether the `increment` value is positive
or negative. This operation can be used to update counters that are
stored on their own in a key or [within a map]({{<baseurl>}}riak/kv/3.0.14/developing/api/protocol-buffers/dt-map-store).

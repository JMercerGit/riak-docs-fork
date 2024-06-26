---
title: "Node.js Client API"
description: "Node.js Client API"
menu:
  riak_ts-1.0.0:
    name: "Node.js"
    identifier: "ts_node.js_api"
    weight: 403
    parent: "developing"
project: "riak_ts"
project_version: "1.0.0"
lastmod: 2015-12-15T00:00:00-00:00
sitemap:
  priority: 0.1
toc: true
aliases:
    - /riakts/1.0.0/developing/nodejs/
---

You can develop with Riak TS through the Node.js client. This
document covers the Node.js protobuf requests to Riak TS.

## Overview

To use Riak TS with Node.js, we've added several new commands in
the `Riak.Commands.TS` namespace.

Language | Source | Documentation | Download
:--------|:-------|:--------------|:--------
Node.js | [riak-nodejs-client](https://github.com/basho/riak-nodejs-client) | [api docs](http://basho.github.com/riak-nodejs-client/), [wiki](https://github.com/basho/riak-nodejs-client/wiki) | [NPM](https://www.npmjs.com/package/basho-riak-client), [GitHub Releases](https://github.com/basho/riak-nodejs-client/releases)

## TS Commands

>**Note:** These commands are automatically retried if they fail due to network
error.

### Commands

 * `Get`    - Fetch a single row based on the primary key values provided.
 * `Store`  - Store 1 or more rows to a Riak TS table.
 * `Delete` - Delete a single row based on the primary key values provided.
 * `Query`  - Allows you to query a Riak TS table, with the given query string.
 * `ListKeys` - Lists the primary keys of all the rows in a Riak TS table.

### Command Details

#### `Get`

```javascript
var Riak = require('basho-riak-client');

var key = [ 'family', 'series', 'KEY' ];

var cb = function (err, rslt) {
    // NB: rslt will be an object with two properties:
    // 'columns' - table columns
    // 'rows' - row matching the Get request
};

var cmd = new Riak.Commands.TS.Get.Builder()
    .withTable('TimeSeriesData')
    .withKey(key)
    .withCallback(cb)
    .build();

client.execute(cmd);
```

Retrieve time series value by key.

|Builder Method | Type    | Description                 |
|---------------|---------|-----------------------------|
|`withTable`    | string  | The time series table name  |
|`withKey`      | array   | The time series value's key |

*Return Type*: response object with `columns` and `rows` properties.

#### `Store`

```javascript
var Riak = require('basho-riak-client');

var now = new Date();

var fiveMinsAgo = new Date(now);
fiveMinsAgo.setMinutes(now.getMinutes() - 5);

var tenMinsAgo = new Date(now);
tenMinsAgo.setMinutes(now.getMinutes() - 10);

var fifteenMinsAgo = new Date(now);
fifteenMinsAgo.setMinutes(now.getMinutes() - 15);

var twentyMinsAgo = new Date(now);
twentyMinsAgo.setMinutes(now.getMinutes() - 20);

var rows = [
    [ 'family', 'series', twentyMinsAgo, 'hurricane', 82.3 ],
    [ 'family', 'series', fifteenMinsAgo, 'rain', 79.0 ],
    [ 'family', 'series', fiveMinsAgo, 'wind', null ],
    [ 'family', 'series', now, 'snow', 20.1 ]
];

var cb = function (err, rslt) {
    // NB: rslt will be true when successful
};

var cmd = new Riak.Commands.TS.Get.Builder()
    .withTable('TimeSeriesData')
    .withRows(rows)
    .withCallback(cb)
    .build();

client.execute(cmd);
```

Stores time series data in the Riak cluster.

|Builder Method | Type   | Description                |
|---------------|--------|----------------------------|
|`withTable`    | string | The time series table name |
|`withRows`     | array  | The time series data       |

*Return Type*: boolean

#### `Delete`

```javascript
var Riak = require('basho-riak-client');

var key = [ 'family', 'series', 'KEY' ];

var cb = function (err, rslt) {
    // NB: rslt will be an object with two properties:
    // 'columns' - table columns
    // 'rows' - row matching the Get request
};

var cmd = new Riak.Commands.TS.Delete.Builder()
    .withTable('TimeSeriesData')
    .withKey(key)
    .withCallback(cb)
    .build();

client.execute(cmd);
```

Delete time series value by key.

|Builder Method | Type    | Description                 |
|---------------|---------|-----------------------------|
|`withTable`    | string  | The time series table name  |
|`withKey`      | array   | The time series value's key |

*Return Type*: boolean

#### `Query`

```javascript
var Riak = require('basho-riak-client');

var cb = function (err, rslt) {
    // NB: rslt will be an object with two properties:
    // 'columns' - table columns
    // 'rows' - row matching the Query request
};

var query = "select * from TimeSeriesData \
    where time > 0 and time < 10 and \
    family = 'hash1' and series = 'user1'";

var cmd = new Riak.Commands.TS.Query.Builder()
    .withQuery(query)
    .withCallback(cb)
    .build();

client.execute(cmd);
```

Queries time series data in the Riak cluster.

|Builder Method | Type    | Description                 |
|---------------|---------|-----------------------------|
|`withTable`    | string  | The time series table name  |
|`withQuery`    | string  | The time series query       |

*Return Type*: response object with `columns` and `rows` properties.

#### `ListKeys`

```javascript
var Riak = require('basho-riak-client');

var allKeys = [];
var callback = function(err, resp) {
    Array.prototype.push.apply(allKeys, resp.keys);
    if (resp.done) {
        // NB: at this point all keys have been received
    }
};

var cmd = new Riak.Commands.TS.ListKeys.Builder()
    .withTable('TimeSeriesData')
    .withStreaming(true)
    .withTimeout(1000)
    .withCallback(callback)
    .build();

cluster.execute(cmd);
```

Lists all keys in a time series table via a stream.

|Builder Method | Type    | Description                                       |
|---------------|---------|---------------------------------------------------|
|`withTable`    | string  | The time series table name                        |
|`withStreaming`| boolean | `true` if you would like callback per-key chunk   |
|`withTimeout`  | integer | Timeout in milliseconds for the list keys command |

*Return Type*: response object with `keys` property.

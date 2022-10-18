﻿---
title_supertext: "Installing on"
title: "Alpine Linux"
description: ""
project: "riak_kv"
project_version: 3.0.10
menu:
  riak_kv-3.0.10:
    name: "Alpine Linux"
    identifier: "installing_alpine_linux"
    weight: 302
    parent: "installing"
toc: true
aliases:
  - /riak/3.0.10/ops/building/installing/Installing-on-Alpine-Linux
  - /riak/kv/3.0.10/ops/building/installing/Installing-on-Alpine-Linux
  - /riak/3.0.10/installing/Alpine-Linux/
  - /riak/kv/3.0.10/installing/Alpine-Linux/
---

[install source index]: {{<baseurl>}}riak/kv/3.0.10/setup/installing/source/
[security index]: {{<baseurl>}}riak/kv/3.0.10/using/security/
[install source erlang]: {{<baseurl>}}riak/kv/3.0.10/setup/installing/source/erlang
[install verify]: {{<baseurl>}}riak/kv/3.0.10/setup/installing/verify


### Riak 64-bit Installation
To install Riak on Alpine Linux:

1. Add `http://files.tiot.jp/alpine/v3.16/main` to /etc/apk/repositories and remove `/home/dev/packages/main` if it is present.
2. <placeholder for public key>
3. Run `apk update`
4. Run `apk add riak` for the latest Riak KV version

## Next Steps

Now that Riak is installed, check out [Verifying a Riak Installation][install verify].






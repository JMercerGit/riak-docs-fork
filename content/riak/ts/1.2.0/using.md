---
title: "Using Riak TS"
description: "Using Riak TS"
menu:
  riak_ts-1.2.0:
    name: "Use"
    identifier: "using"
    weight: 300
    pre: database
project: "riak_ts"
project_version: "1.2.0"
lastmod: 2016-02-16T00:00:00-00:00
sitemap:
  priority: 0.1
toc: true
aliases:
    - /riakts/1.2.0/using/
---

[activating]: creating-activating/
[aggregate]: aggregate-functions/
[arithmetic]: arithmetic-operations/
[configuring]: configuring/
[installing]: ../installing/
[planning]: planning/
[querying]: querying/
[writing]: writingdata/

Now that you've downloaded the package from ZenDesk and [installed][installing] Riak TS, there's a recommended path for setting up and using it:

1. [Plan][planning] your Riak TS table. Once created, tables can't be edited, so it's important to get it right the first time.
2. [Create and activate][activating] your Riak TS table. (You'll need `sudo` and `su` access for this step.)
3. [Write data][writing] to your table.

Once you've completed these steps you can go on to [query][querying] your data,[customize your Riak TS configuration][configuring], analyze your data with [aggregate functions][aggregate], or apply some [arithmetic operations][arithmetic].

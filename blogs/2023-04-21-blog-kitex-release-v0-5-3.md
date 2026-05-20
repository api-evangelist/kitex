---
title: "Blog: Kitex Release v0.5.3"
url: "https://www.cloudwego.io/blog/2023/04/21/kitex-release-v0.5.3/"
date: "Fri, 21 Apr 2023 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
Introduction to Key Changes Feature Failure retry：add configuration to support disable timeout retry when do failure retry, which is for the non-idempotent request Codegen tool：support codegen in windows. Error code: fine grained rpc timeout error code Thrift Fast Codec: support unknown fields Background of “unknown fields”: In Thrift, adding fields in the IDL is transparent to the party that has not updated the IDL. Updating the IDL and generating code is necessary to access new fields, which requires all downstream nodes to upgrade when a node on the invocation Chain updates the IDL.…

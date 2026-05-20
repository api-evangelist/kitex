---
title: "Blog: Kitex Release v0.10.0"
url: "https://www.cloudwego.io/blog/2024/06/12/kitex-release-v0.10.0/"
date: "Wed, 12 Jun 2024 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
Introduction to Key Changes Performance Optimization Long connection: conncurrency = 100, qps increased by 4%, p99 decreased by 18% connection multiplexing: conncurrency = 100, qps increased by 7%, p99 decreased by 24% gRPC: conncurrency = 100, qps increased by 8%，p99 decreased by 10% Code Generation Simplification and Optimization Remove non-serialization code (By default) : the original kitex_gen Thrift code includes Processor code to maintain consistency with Apache Thrift. However, Kitex does not need these codes. To solve users’ code generation painpoint, this version Kitex removes this…

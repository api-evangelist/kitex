---
title: "Blog: Kitex Release v0.6.0"
url: "https://www.cloudwego.io/blog/2023/06/14/kitex-release-v0.6.0/"
date: "Wed, 14 Jun 2023 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
Introduction to Key Changes Feature 1. GRPC Metainfo Pass Through The gRPC client sets the header to ctx by default, and external methods can use GetHeaderMetadataFromCtx to obtain meta information. It can be used to obtain meta information within transmeta and set it to rpcinfo, or to obtain header information within middlewares.

---
title: "Blog: Kitex Release v0.12.0"
url: "https://www.cloudwego.io/blog/2025/01/03/kitex-release-v0.12.0/"
date: "Fri, 03 Jan 2025 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
Introduction to Key Changes Simplified Product Recommendation - Remove Apache Thrift Dependency We strongly recommend removing Apache Codec to resolve the compilation issues caused by Apache’s incompatible changes and to reduce the product size by 50% . Please replace it with Kitex’s own Thrift codec: FastCodec or Frugal, which does not rely on Apache Thrift Codec. Future version plans: Kitex will remove Apache products by default.

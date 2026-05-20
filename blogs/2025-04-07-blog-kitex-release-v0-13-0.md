---
title: "Blog: Kitex Release v0.13.0"
url: "https://www.cloudwego.io/blog/2025/04/07/kitex-release-v0.13.0/"
date: "Mon, 07 Apr 2025 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
We recommend upgrading directly to Kitex version v0.13.1, as we have fixed a potential Goroutine leak issue of the gRPC Client in v0.13.0. Introduction to Key Changes New Features New streaming interface StreamX supports gRPC, existing Kitex gRPC users can migrate v0.12.0 released the StreamX interface to optimise the streaming experience, and supported the custom streaming protocol TTHeader Streaming, but did not support gRPC. So existing users could not migrate.

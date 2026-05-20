---
title: "Blog: Kitex Release v0.14.0"
url: "https://www.cloudwego.io/blog/2025/06/26/kitex-release-v0.14.0/"
date: "Thu, 26 Jun 2025 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
Introduction to Key Changes New Features Generic Call: The generic Client supports streaming calls, allowing a single Client to handle both streaming and non-streaming scenarios It supports streaming generic calls, adapting to gRPC/TTHeader Streaming and supporting map/JSON and Protobuf binary generic calls. A brief code example is as follows: cli , err := genericclient . NewClient ( "actualServiceName" , g ) // Ping-Pong generic resp , err := cli .

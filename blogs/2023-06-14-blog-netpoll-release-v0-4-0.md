---
title: "Blog: Netpoll Release v0.4.0"
url: "https://www.cloudwego.io/blog/2023/06/14/netpoll-release-v0.4.0/"
date: "Wed, 14 Jun 2023 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
Feature: [ #249 ] feat: add Detach function to support detach connection from its poller Optimize: [ #250 ] optimize: WriteDirect implementation to avoid panic and duplicate creation of redundant LinkBufferNode when remainLen is 0 Bugfix: [ #256 ] fix: close the poll that has already been created when calling the openPoll fails [ #251 ] fix: err to e0 [ #226 ] fix: poller read all data before connection close [ #237 ] fix: shard queue state closed mistake [ #189 ] fix: close connection when readv syscall return 0, nil Refactor [ #233 ] refactor: simplify race and norace event loop

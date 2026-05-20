---
title: "Blog: Netpoll Release v0.6.0"
url: "https://www.cloudwego.io/blog/2024/03/04/netpoll-release-v0.6.0/"
date: "Mon, 04 Mar 2024 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
Feature [ #306 ] feat: lazy init pollers to avoid create any poller goroutines if netpoll is not used [ #303 ] feat: add WithOnDisconnect callback [ #300 ] feat: netpoll exception implement net.Error interface [ #294 ] feat: add SetRunner option Fix [ #307 ] fix: ctx race when disconnect callback run with connect callback [ #304 ] fix: connection leak when poller close connection but onRequest callback just finished [ #296 ] fix: stop timer when read triggered by err Chore [ #302 ] ci: bump the version of actions/checkout and actions/setup-go

---
title: "Blog: Netpoll Release v0.5.0"
url: "https://www.cloudwego.io/blog/2023/09/26/netpoll-release-v0.5.0/"
date: "Tue, 26 Sep 2023 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
Optimize [ #274 ] optimize: increase first bookSize to 8KB to reduce overhead for connection read at begin [ #273 ] optimize: ignore EOF when read a closed connection Fix [ #283 ] fix: protect operator dont be detach twice [ #280 ] fix: detach operator race [ #278 ] fix: OnRequest should wait all readable data consumed when sender close connection [ #276 ] fix: compile error by miss package [ #238 ] fix: close conn when server OnRequest panic Docs [ #243 ] docs: rm outdated info

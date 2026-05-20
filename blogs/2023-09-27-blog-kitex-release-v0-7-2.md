---
title: "Blog: Kitex Release v0.7.2"
url: "https://www.cloudwego.io/blog/2023/09/27/kitex-release-v0.7.2/"
date: "Wed, 27 Sep 2023 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
Introduction to Key Changes Features 1. Retry: limit perncetage of retry requests The feature improves the usability of backup requests: if a request exceeds the retry delay threshold, a backup request will be sent; but if the request succeeds within the timeout threshold, it will not be treated as an error. Therefore large amount of backup requests may be sent due to a network jitter, which increases the pressure on the server and could even cause an avanlache.

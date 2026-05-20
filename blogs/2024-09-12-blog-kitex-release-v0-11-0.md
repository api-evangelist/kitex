---
title: "Blog: Kitex Release v0.11.0"
url: "https://www.cloudwego.io/blog/2024/09/12/kitex-release-v0.11.0/"
date: "Thu, 12 Sep 2024 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
Highly recommend upgrading Kitex version to v0.11.3 or higher, because there’s some bugfix on v0.11.0. Introduction to Key Changes New Feature Mixed Retry : Supports enabling both “Failure Retry” and “Backup Request” strategies simultaneously, which can reduce tail requests while increasing the success rate of retries, for more detail: Retry Custom Payload Validation : To avoid inconsistencies in data transmission caused by hardware failures or data tampering, Kitex provides validation functionality for payload messages and supports custom extensions. For usage: Payload Validator .

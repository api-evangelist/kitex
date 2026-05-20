---
title: "Blog: Volo Release 0.4.1"
url: "https://www.cloudwego.io/blog/2023/03/20/volo-release-0.4.1/"
date: "Mon, 20 Mar 2023 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
In Volo 0.4.1, in addition to the usual bugfixes, some new features have been introduced. More detailed Thrift Decode error messages Previous versions of Thrift Decode error messages reported only the most basic errors, without any context. For example, it contained the following structural relationships struct A { 1 : required B b . } struct B { 2 : required C c . } struct C { 3 : required string a . } If an error occurs while decoding field a of struct C .

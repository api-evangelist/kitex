---
title: "Blog: Volo Release 0.3.0"
url: "https://www.cloudwego.io/blog/2022/12/22/volo-release-0.3.0/"
date: "Thu, 22 Dec 2022 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
In Volo 0.3.0 version, in addition to regular bugfixes, we also brought several important features. Service Trait refactoring In version 0.3.0 of Volo, we refactored Service Trait to make the implementation of Service Trait easier and provide more flexibility. Specifically, we changed the definition of Service Trait from: pub trait Service < Cx , Request > { /// Responses given by the service. type Response ; /// Errors produced by the service. type Error ; /// The future response value. type Future < 'cx > : Future < Output = Result < Self :: Response , Self :: Error >> + Send + 'cx where…

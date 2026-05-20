---
title: "Blog: Volo Release 0.8.0"
url: "https://www.cloudwego.io/blog/2023/10/23/volo-release-0.8.0/"
date: "Mon, 23 Oct 2023 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
In Volo 0.8.0, we mainly refactored the Service trait and all previous places that used async_trait by using two newly stabilized features: AFIT (Async Fn In Trait) and RPITIT (Return Position Impl Trait In Traits). This not only brings a slight performance improvement, but also significantly enhances the usability of writing Service, as you can directly write async fn call. Break Change Service trait refactoring In the latest nightly, Rust’s two highly anticipated heavyweight features, AFIT (Async Fn In Trait) and RPITIT (Return Position Impl Trait In Traits), have been stabilized, which…

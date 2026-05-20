---
title: "Blog: Volo Release 0.9.0"
url: "https://www.cloudwego.io/blog/2024/01/04/volo-release-0.9.0/"
date: "Thu, 04 Jan 2024 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
In Volo 0.9.0, we mainly changed the default generated HashSet/HashMap type to AHashMap/AHashSet, which is expected to bring certain performance improvements. Additionally, with the release of Rust 1.75 , Volo is already available in stable rust. Break Change Modification of the default generated HashSet / HashMap type In the new version of the generated code, the default generated HashMap/HashSet type is changed to AHashMap/AHashSet, which gives better performance than std map, refer to ahash .

---
title: "Blog: Hertz Release v0.9.0"
url: "https://www.cloudwego.io/blog/2024/05/30/hertz-release-v0.9.0/"
date: "Thu, 30 May 2024 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
<p>The Hertz v0.9.0 release mainly supports general iteration and optimization.</p>
<h2 id="feature">Feature</h2>
<ol>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1101">#1101</a>] feat: add method to exile requestContext</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1056">#1056</a>] feat: add more default type for binding</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1057">#1057</a>] feat: add SetHandlers when fast fail for no valid host and invalid rPath</li>
</ol>
<h2 id="optimize">Optimize</h2>
<ol>
<li>[<a href="https://github.com/cloudwego/hertz/pull/921">#921</a>] optimize(hz): sort route strictly which preventing sorting inconsistencies</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1037">#1037</a>] optimize: filter shortConnErr in tracer</li>
</ol>
<h2 id="fix">Fix</h2>
<ol>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1102">#1102</a>] fix: resp set trailer will panic</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1107">#1107</a>] fix: router sort</li>
</ol>
<h2 id="refactor">Refactor</h2>
<ol>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1064">#1064</a>] refactor(hz): client query enum</li>
</ol>

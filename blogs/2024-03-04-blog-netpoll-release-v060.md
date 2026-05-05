---
title: "Blog: Netpoll Release v0.6.0"
url: "https://www.cloudwego.io/blog/2024/03/04/netpoll-release-v0.6.0/"
date: "Mon, 04 Mar 2024 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
<h2 id="feature">Feature</h2>
<ol>
<li>[<a href="https://github.com/cloudwego/netpoll/pull/306">#306</a>] feat: lazy init pollers to avoid create any poller goroutines if netpoll is not used</li>
<li>[<a href="https://github.com/cloudwego/netpoll/pull/303">#303</a>] feat: add WithOnDisconnect callback</li>
<li>[<a href="https://github.com/cloudwego/netpoll/pull/300">#300</a>] feat: netpoll exception implement net.Error interface</li>
<li>[<a href="https://github.com/cloudwego/netpoll/pull/294">#294</a>] feat: add SetRunner option</li>
</ol>
<h2 id="fix">Fix</h2>
<ol>
<li>[<a href="https://github.com/cloudwego/netpoll/pull/307">#307</a>] fix: ctx race when disconnect callback run with connect callback</li>
<li>[<a href="https://github.com/cloudwego/netpoll/pull/304">#304</a>] fix: connection leak when poller close connection but onRequest callback just finished</li>
<li>[<a href="https://github.com/cloudwego/netpoll/pull/296">#296</a>] fix: stop timer when read triggered by err</li>
</ol>
<h2 id="chore">Chore</h2>
<ol>
<li>[<a href="https://github.com/cloudwego/netpoll/pull/302">#302</a>] ci: bump the version of actions/checkout and actions/setup-go</li>
</ol>

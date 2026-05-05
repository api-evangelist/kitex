---
title: "Blog: Hertz Release v0.10.0"
url: "https://www.cloudwego.io/blog/2025/05/21/hertz-release-v0.10.0/"
date: "Wed, 21 May 2025 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
<p>The Hertz v0.10.0 release adds two features and some fixes.</p>
<ol>
<li>Integrate SSE functionality. Refer to <a href="https://www.cloudwego.io/docs/hertz/tutorials/basic-feature/sse/">SSE</a> for usage.</li>
<li>Added http.Handler adaptor, extending Hertz using the official net/http ecosystem. Refer to <a href="https://www.cloudwego.io/docs/hertz/tutorials/basic-feature/http-adaptor/">Adaptor</a> for usage.</li>
</ol>
<h2 id="feature">Feature</h2>
<ol>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1327">#1327</a>] feat(adaptor): new HertzHandler for http.Handler</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1349">#1349</a>] feat(sse): SetLastEventID</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1343">#1343</a>] feat(sse): reader supports cancel stream</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1341">#1341</a>] feat(server): detect request race</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1339">#1339</a>] feat(sse): add LastEventID helpers</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1335">#1335</a>] feat(protocol): new sse pkg</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1322">#1322</a>] feat: std transport sense client connection close</li>
</ol>
<h2 id="fix">Fix</h2>
<ol>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1340">#1340</a>] fix: only use netpoll &amp; sonic on amd64/arm64 linux/darwin</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1333">#1333</a>] fix(protocol): unexpected set resp.bodyStream</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1329">#1329</a>] fix(client): stream body for sse instead of timeout</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1332">#1332</a>] fix(server): Shutdown checks ExitWaitTimeout</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1316">#1316</a>] fix: prioritize custom validator</li>
</ol>
<h2 id="tests">Tests</h2>
<ol>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1336">#1336</a>] test(protocol): fix hardcoded listen addr</li>
</ol>
<h2 id="chore">Chore</h2>
<ol>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1353">#1353</a>] chore: update netpoll dependency</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1337">#1337</a>] chore(hz): update hz tool v0.9.7</li>
<li>[<a href="https://github.com/cloudwego/hertz/pull/1328">#1328</a>] ci: disable codecov annotations</li>
</ol>

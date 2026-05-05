---
title: "Blog: Kitex Release v0.11.0"
url: "https://www.cloudwego.io/blog/2024/09/12/kitex-release-v0.11.0/"
date: "Thu, 12 Sep 2024 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
<blockquote>
<p>Highly recommend upgrading Kitex version to v0.11.3 or higher, because there&rsquo;s some bugfix on v0.11.0.</p></blockquote>
<h2 id="introduction-to-key-changes"><strong>Introduction to Key Changes</strong></h2>
<h3 id="new-feature">New Feature</h3>
<ol>
<li><strong>Mixed Retry</strong>: Supports enabling both &ldquo;Failure Retry&rdquo; and &ldquo;Backup Request&rdquo; strategies simultaneously, which can reduce tail requests while increasing the success rate of retries, for more detail: <a href="https://www.cloudwego.io/docs/kitex/tutorials/service-governance/retry/">Retry</a></li>
<li><strong>Custom Payload Validation</strong>: To avoid inconsistencies in data transmission caused by hardware failures or data tampering, Kitex provides validation functionality for payload messages and supports custom extensions. For usage: <a href="https://www.cloudwego.io/docs/kitex/tutorials/advanced-feature/payload_validator/">Payload Validator</a>.</li>
</ol>
<h3 id="feature-optimization">Feature optimization</h3>
<ol>
<li><strong>Frugal ARM Optimization</strong>: Frugal v0.2.0 now supports a new implement by reflection</li>
<li><strong>Kitex Tool Improvement</strong>: Kitex Tool provide a new param <code>-rapid</code> to integrates Thriftgo and there&rsquo;s a slightly improved speed.</li>
<li><strong>Generating Multiple Handlers for Multiple Services</strong>：Since this version, Kitex tool provide each service with independent handler file and register them into server，for more details: <a href="https://www.cloudwego.io/docs/kitex/tutorials/advanced-feature/multi_service/multi_handler/">Generating Multiple Handlers for Multiple Services</a></li>
</ol>
<h3 id="others">Others</h3>
<ol>
<li>Support Go 1.18~1.23. Minimum support for Golang 1.18，if your golang version is lower than 1.18, you&rsquo;ll see <code>note: module requires Go 1.18</code> when you compile.</li>
<li>Remove Apache Thrift，and refactor all related interface into github.com/cloudwego/gopkg/thrift.</li>
</ol>
<h2 id="full-release-log"><strong>Full Release Log</strong></h2>
<h3 id="feature">Feature:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1509">#1509</a>] feat(retry): support Mixed Retry which integrating Failure Retry and Backup Request</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1478">#1478</a>] feat: customized payload validator</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1514">#1514</a>] feat(grpc): server returns cancel reason</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1513">#1513</a>] feat(tool): support updating import path for PkgInfo</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1425">#1425</a>] feat(tool): support generating multiple handlers for multiple services</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1491">#1491</a>] feat(grpc): add GetTrailerMetadataFromCtx</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1492">#1492</a>] feat: add GetCallee to kitexutil to get the service name of callee</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1479">#1479</a>] feat(tool): embed thriftgo into kitex tool</p>
<h3 id="optimize">Optimize:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1485">#1485</a>] optimize: add cachekey to discovery event for debug</p>
<h3 id="fix">Fix:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1525">#1525</a>] fix: move json-iterator back to support marshal <code>map[any]any</code></p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1471">#1471</a>] fix(streaming): resolve ctx diverge in server-side streaming</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1515">#1515</a>] fix(gRPC): pass error when client transport is closed</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1501">#1501</a>] fix(generic): judge business error directly</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1503">#1503</a>] fix: return an unknown service/method exception to client correctly under multi_service server scenario</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1487">#1487</a>] fix(generic): fix a generic serviceInfo compatible issue</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1489">#1489</a>] fix(codec): wrap trans error for apache thrift read error</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1486">#1486</a>] fix(trans/netpoll): log when panic in onConnRead</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1476">#1476</a>] fix: fix GetServerConn interface assert for streamWithMiddleware</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1481">#1481</a>] fix(gonet): adjust gonet server read timeout to avoid read error</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1466">#1466</a>] fix: allow HEADERS frame with empty header block fragment</p>
<h3 id="refactor">Refactor:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1512">#1512</a>] refactor: thrift and generic codec uses bufiox interface for encoding and decoding</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1490">#1490</a>] refactor: optimized apache codec without reflection</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1483">#1483</a>] refactor: use github.com/cloudwego/gopkg/protocol/thrift/apache</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1474">#1474</a>] refactor: rm apache thrift in internal/mocks</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1470">#1470</a>] refactor: rm apache thrift in pkg/generic &amp; netpollmux</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1450">#1450</a>] refactor(generic): remove apache thrift.TProtocol from generic</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1441">#1441</a>] refactor: deprecate bthrift, use cloudwego/gopkg</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1455">#1455</a>] refactor(test): perf optimize and log loc correct</p>
<h3 id="tests">Tests:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1469">#1469</a>] test: replace judgement of mem stats of client finalizer by closed count check</p>
<h3 id="perf">Perf:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1527">#1527</a>] perf(grpc): bdp ping rate limit</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1511">#1511</a>] perf(thrift): encodeBasicThrift write logic didn&rsquo;t use kitex BinaryProtocol</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1504">#1504</a>] perf(grpc): zero allocation in hot path</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1497">#1497</a>] perf: add option to enable spancache for fastpb</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1495">#1495</a>] perf(thrift): use kitex BinaryProtocol replace apache BinaryProtocol for apache thrift codec</p>
<h3 id="chore">Chore:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1532">#1532</a>] chore: update dependency</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1522">#1522</a>] chore(generic): make generic streaming APIs internal</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1465">#1465</a>] chore(generic): add an external method to create service info for generic streaming client</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1468">#1468</a>] build: adapt to go1.23rc2</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1482">#1482</a>] chore(generic): add generic base using gopkg base</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1463">#1463</a>] chore: fix grpc keepalive test by start server responsiblly</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1462">#1462</a>] chore(test): fix xorshift64 in consist_test.go</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1454">#1454</a>] chore(ci): speed up multiple ci processes 8min -&gt; 1min</p>

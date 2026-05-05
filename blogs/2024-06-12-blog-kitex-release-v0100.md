---
title: "Blog: Kitex Release v0.10.0"
url: "https://www.cloudwego.io/blog/2024/06/12/kitex-release-v0.10.0/"
date: "Wed, 12 Jun 2024 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
<h2 id="introduction-to-key-changes"><strong>Introduction to Key Changes</strong></h2>
<h3 id="performance-optimization">Performance Optimization</h3>
<ol>
<li>Long connection: conncurrency = 100, qps increased by 4%, p99 decreased by 18%</li>
<li>connection multiplexing: conncurrency = 100, qps increased by 7%, p99 decreased by 24%</li>
<li>gRPC: conncurrency = 100, qps increased by 8%，p99 decreased by 10%</li>
</ol>
<h3 id="code-generation-simplification-and-optimization">Code Generation Simplification and Optimization</h3>
<ol>
<li><strong>Remove non-serialization code (By default)</strong>: the original kitex_gen Thrift code includes Processor code to maintain consistency with Apache Thrift. However, Kitex does not need these codes. To solve users&rsquo; code generation painpoint, this version Kitex removes this part of the code, increasing the generation speed by about 10%.</li>
<li><strong>Remove Apache Codec code (Remove if configured)</strong>：Kitex has custom FastCodec code, and the original Apache Codec is only required when using Buffered protocol. The new version of Kitex implements SkipDecoder. If enabled, the serialization will be completely independent of Apache Codec, reducing the generated code size by about 50%. Refer to this doc for usage <a href="https://www.cloudwego.io/docs/kitex/tutorials/code-gen/skip_decoder/">SkipDecoder</a></li>
</ol>
<h3 id="new-feature">New Feature</h3>
<ol>
<li><strong>Thrift Serialize Data Ondemands</strong>：Support defining FieldMask to achieve on-demand serialization of data (field clipping, merging, RPC Performance optimization, etc.), see details <a href="https://github.com/cloudwego/thriftgo/tree/main/fieldmask">Thrift FieldMask RFC</a></li>
</ol>
<h3 id="feature-optimization">Feature optimization</h3>
<ol>
<li><strong>CircuitBreaker</strong>： Support for customized circuit breaker error types.</li>
<li><strong>Failure Retry</strong>：The code configuration of the customized result retry adds the ctx parameter to facilitate users to check whether to retry based on ctx information.</li>
<li><strong>Remove cache from consistent hashing</strong>：Solve the issue of high latency and memory increase caused by scattered hash keys. After removing the cache, it can effectively reduce memory usage and cache management consumption in scenarios where keys are particularly scattered or even close to random distribution.</li>
</ol>
<h3 id="user-experience-and-tool-optimization">User Experience and Tool Optimization</h3>
<ol>
<li><strong>Kitex tool compatibility check</strong>：Optimize the &ldquo;undefined&rdquo; compile error caused by introducing new definitions in old generated code. The Kitex tool will check the Kitex version used in go.mod before generating code. If the Kitex tool and Kitex version are incompatible, the code will not be generated and will provide corresponding upgrade and downgrade prompts and documentation.</li>
</ol>
<h2 id="full-release-log"><strong>Full Release Log</strong></h2>
<h3 id="feature">Feature:</h3>
<ol>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1370">#1370</a>] feat(loadbalance): do not cache all the keys for Consistent Hash</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1359">#1359</a>] feat:(generic) jsonpb using dynamicgo support parse IDL from memory</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1353">#1353</a>] feat(retry): add ctx param for customized result retry funcs</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1352">#1352</a>] feat: add option to specify ip version for default HTTPResolver</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1316">#1316</a>] feat(kitex tool): support dependencies compatibility checking</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1346">#1346</a>] feat(generic): set dynamicgo parse mode</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1336">#1336</a>] feat(tool): fast-codec supports Thrift Fieldmask</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1313">#1313</a>, #1378] feat(thrift codec): implement skipDecoder to enable Frugal and FastCodec for standard Thrift Buffer Protocol</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1257">#1257</a>] feat: CBSuite custom GetErrorType func</li>
</ol>
<h3 id="optimize">Optimize:</h3>
<ol>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1349">#1349</a>] optimize(gRPC): gRPC onError uses CtxErrorf to print log with information in ctx</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1326">#1326</a>] optimize(tool): remove thrift processor for less codegen</li>
</ol>
<h3 id="perf">Perf:</h3>
<ol>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1369">#1369</a>] perf(thrift): optimized skip decoder</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1314">#1314</a>] perf: use dirtmake to reduce memclr cost</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1322">#1322</a>] perf(codec): support fast write nocopy when using netpoll link buffer</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1276">#1276</a>] perf: linear allocator for fast codec ReadString/ReadBinary</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1320">#1320</a>] perf(codec): fast codec use batch alloc</li>
</ol>
<h3 id="fix">Fix:</h3>
<ol>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1379">#1379</a>] fix: fix a bug &ldquo;unknown service xxx&rdquo; when using generic client by not writing IDLServiceName when it&rsquo;s generic service</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1368">#1368</a>] fix(remote): modify the error message thrown when no target service is found</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1374">#1374</a>] fix: init default values when using liner allocator</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1361">#1361</a>] fix: span cache re-cap bytes when using Make</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1362">#1362</a>] fix(payloadCodec): replace the registered PayloadCodec if the type is same when using WithPayloadCodec for server-side</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1364">#1364</a>] fix: fix grpc compressor mcache free panic when data is empty</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1328">#1328</a>] fix(gRPC): release connection in DoFinish for grpc streaming to close the short connection</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1307">#1307</a>] fix(connpool): kitex long pool reset idleList element to nil to prevent conn leak</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1294">#1294</a>] fix(netpollmux): fix a bug that disables multi-service by assigning the first svcInfo to targetSvcInfo</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1308">#1308</a>] fix(generic): not write generic method name for binary generic exception to align with method names of services not using binary generic</li>
</ol>
<h3 id="refactor">Refactor:</h3>
<ol>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1344">#1344</a>] refactor(tool): export thriftgo template definition in kitextool</li>
</ol>
<h3 id="chore">Chore:</h3>
<ol>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1385">#1385</a>] chore: update dynamicgo to v0.2.8</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1383">#1383</a>] chore: upgrade netpoll to v0.6.1</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1376">#1376</a>] chore: integration test use go 1.20 to solve the compatibility issue of official gRPC in kitex-tests repo</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1355">#1355</a>] chore: upgrade netpoll to v0.6.1 pre-release version</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1338">#1338</a>] chore: correct the comment of FreezeRPCInfo</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1347">#1347</a>] chore: use runtimex to replace choleraehyq/pid</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1342">#1342</a>] chore: update sonic/loader to v0.1.1</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1334">#1334</a>] chore: update dynamicgo to v0.2.3</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1324">#1324</a>] chore: update dynamicgo and sonic version</li>
<li>[<a href="https://github.com/cloudwego/kitex/pull/1317">#1317</a>] chore: frugal v0.1.15 (with migrated iasm)</li>
</ol>
<hr />
<p><strong>Thanks a lot to those community contributors who submit some pull requests or share your ideas for this version:</strong>
@XiaoYi-byte</p>

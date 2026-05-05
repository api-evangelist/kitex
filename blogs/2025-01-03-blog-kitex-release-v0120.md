---
title: "Blog: Kitex Release v0.12.0"
url: "https://www.cloudwego.io/blog/2025/01/03/kitex-release-v0.12.0/"
date: "Fri, 03 Jan 2025 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
<h2 id="introduction-to-key-changes"><strong>Introduction to Key Changes</strong></h2>
<h3 id="simplified-product-recommendation---remove-apache-thrift-dependency">Simplified Product Recommendation - Remove Apache Thrift Dependency</h3>
<p>We strongly recommend removing Apache Codec to resolve the compilation issues caused by Apache&rsquo;s incompatible changes and to <strong>reduce the product size by 50%</strong>.</p>
<p>Please replace it with Kitex&rsquo;s own Thrift codec: FastCodec or Frugal, which does not rely on Apache Thrift Codec.</p>
<p>Future version plans: Kitex will remove Apache products by default. User guide: <a href="https://www.cloudwego.io/docs/kitex/best-practice/remove_apache_codec/">Kitex Remove Apache Thrift User Guide</a></p>
<h3 id="new-features">New Features</h3>
<ol>
<li>
<p><strong>Thrift Streaming over TTHeader - Custom Streaming Protocol</strong></p>
<p>Supported streaming calls based on the TTHeader protocol, optimizing stability issues caused by the high complexity of the gRPC streaming protocol.</p>
<p>Provided a new streaming interface, StreamX, to solve various user experience issues with the original streaming interface and provide best practices for streaming interfaces.</p>
<p>For more details: <a href="https://www.cloudwego.io/docs/kitex/tutorials/basic-feature/streamx/">StreamX User Documentation and Best Practices</a></p>
</li>
<li>
<p><strong>Graceful Shutdown for gRPC Streaming</strong></p>
<p>Added support for a graceful shutdown feature to address upstream errors caused by service upgrades or updates.</p>
<p>For usage: <a href="https://www.cloudwego.io/docs/kitex/tutorials/basic-feature/protocol/streaming/grpc/graceful_shutdown/">gRPC Streaming Graceful Shutdown</a></p>
</li>
</ol>
<h3 id="experience-optimization">Experience Optimization</h3>
<ol>
<li>
<p><strong>gRPC Streaming Log Optimization</strong></p>
<p>For streaming concatenation scenarios, if the downstream error is due to an exit of the upstream Stream exiting, the error will include the suffix &ldquo;[triggered by {serviceName}]&rdquo; will be included in the error, which is convenient for locating the problem.</p>
<p>Errors returned by Send such as <code>the stream is done</code> now reflect the actual error that caused the stream to close.</p>
</li>
<li>
<p><strong>Code Generation Tool Kitex Tool</strong></p>
<p><strong>Optimization of Generation Speed and Tool Installation</strong>: Now Thriftgo is built into Kitex, significantly improving generation speed, especially for scenarios with particularly large IDL files. There is no need to install or upgrade Thriftgo anymore.</p>
<p><strong>Minimizing Product Size</strong>: To minimize product size, Frugal can be used. For gray scale adoption, it supports specifying certain structs to use Frugal serialization.
For more details, refer to <a href="https://www.cloudwego.io/docs/kitex/tutorials/code-gen/code_generation/">Code Generation Tool</a> for instructions on -frugal-struct and -gen-frugal parameters.</p>
</li>
</ol>
<h3 id="breaking-change---no-impact-for-99-of-users">Breaking Change - No Impact for 99% of Users</h3>
<p>Kitex will strive to ensure compatibility with normal usage methods. Some users may have dependencies on certain code definitions of Kitex, and this version adjustment of Kitex will have an impact on these users.</p>
<ul>
<li>
<p>Removing <code>thrift.NewBinaryProtocol</code>
<code>thrift.NewBinaryProtocol</code> is Kitex&rsquo;s implementation of the Apache thrift.TProtocol interface. Because the trans part directly uses Kitex&rsquo;s ByteBuffer, the performance is better than Apache thrift.TBinaryProtocol.
The Deprecation comment has been added to it in v0.11.0.</p>
<p><strong>Removing Reason</strong>: To remove the Apache Thrift dependency, the implementation needs to be removed.</p>
<p><strong>User Modification Method</strong>: This implementation was originally used with Apache Codec. If you still need to rely on Apache Codec, please directly use Apache&rsquo;s TBinaryProtocol.
If you think that it has an impact on performance, you can fork the old version of Kitex, refer to github/cloudwego/kitex v0.10.0</p>
<div class="highlight"><pre tabindex="0"><code class="language-go"><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #204a87; font-weight: bold;">import</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #4e9a06;">"github.com/apache/thrift/lib/go/thrift"</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">tProt</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #ce5c00; font-weight: bold;">:=</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">thrift</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">NewTBinaryProtocol</span><span style="color: #000; font-weight: bold;">(</span><span style="color: #000;">thrift</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">NewTMemoryBufferLen</span><span style="color: #000; font-weight: bold;">(</span><span style="color: #0000cf; font-weight: bold;">1024</span><span style="color: #000; font-weight: bold;">),</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #204a87; font-weight: bold;">true</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #204a87; font-weight: bold;">true</span><span style="color: #000; font-weight: bold;">)</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span></code></pre></div></li>
<li>
<p><strong>Removing <code>generic.ServiceInfo</code></strong></p>
<p>Generic removed an API <code>generic.ServiceInfo</code>.</p>
<p><strong>Removing Reason</strong>: To prepare for future multi-service registration on a generic server, the generic implementation has been refactored (v0.11.0), and this API is no longer used.</p>
<p><strong>User Modification Method</strong>: This API was replaced by <code>generic.ServiceInfoWithGeneric</code>. Please use it instead.</p>
<div class="highlight"><pre tabindex="0"><code class="language-go"><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #204a87; font-weight: bold;">import</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #4e9a06;">"github.com/cloudwego/kitex/pkg/generic"</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #8f5902; font-style: italic;">// removed</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #204a87; font-weight: bold;">func</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">ServiceInfo</span><span style="color: #000; font-weight: bold;">(</span><span style="color: #000;">pcType</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">serviceinfo</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">PayloadCodec</span><span style="color: #000; font-weight: bold;">)</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #ce5c00; font-weight: bold;">*</span><span style="color: #000;">serviceinfo</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">ServiceInfo</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #8f5902; font-style: italic;">// please use this instead</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #204a87; font-weight: bold;">func</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">ServiceInfoWithGeneric</span><span style="color: #000; font-weight: bold;">(</span><span style="color: #000;">g</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">Generic</span><span style="color: #000; font-weight: bold;">)</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #ce5c00; font-weight: bold;">*</span><span style="color: #000;">serviceinfo</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">ServiceInfo</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span></code></pre></div></li>
</ul>
<h2 id="full-release-log"><strong>Full Release Log</strong></h2>
<h3 id="feature">Feature:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1541">#1541</a>][<a href="https://github.com/cloudwego/kitex/pull/1633">#1633</a>] feat(ttstream): support ttheader streaming and streamv2 interface</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1623">#1623</a>] feat(gRPC): optimize gRPC error prompt and metrics, assisting in troubleshooting problems</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1556">#1556</a>] feat(gRPC): support gRPC graceful shutdown</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1467">#1467</a>][<a href="https://github.com/cloudwego/kitex/pull/1627">#1627</a>][<a href="https://github.com/cloudwego/kitex/pull/1619">#1619</a>] feat(generic): support thrift streaming(over gRPC) for json generic client</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1607">#1607</a>] feat(tool): kitex tool support gen frugal codec for certain struct</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1526">#1526</a>] feat(generic): support an option to remove go.tag annotation</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1536">#1536</a>] feat(generic): support an option to set IDL ParseMode for each client</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1510">#1510</a>] feat: register service with service level middleware</p>
<h3 id="optimize">Optimize:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1635">#1635</a>] optimize: add two function for binary protocol to get bufiox reader and writer</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1630">#1630</a>] optimize(tool): implement no recursive generate to support incremental update</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1617">#1617</a>] optimize(retry): optimize UpdatePolicy and add test cases to check invalid retry policy. &lt;v0.11.0, if the FailurePolicy is nil and type is 0 or &gt;1, will trigger nil panic. The bug has been fixed in v0.11.0, this pr is to add test cases and optimize UpdatePolicy to ignore the nil panic</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1606">#1606</a>] optimize(tool): use embedded thriftgo as default option</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1595">#1595</a>] optimize(tool): optimize pb tool code</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1599">#1599</a>] optimize(tool): call FastWriteNocopy in FastWrite to avoid misuse by users</p>
<h3 id="refactor">Refactor:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1615">#1615</a>] refactor: get rid of apache thrift in go.mod</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1611">#1611</a>][<a href="https://github.com/cloudwego/kitex/pull/1614">#1614</a>] refactor: move ttheader codec logic to gopkg</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1553">#1553</a>] refactor(codec/thrift): unified typecodec implementation and adjust new file layout</p>
<h3 id="perf">Perf:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1581">#1581</a>][<a href="https://github.com/cloudwego/kitex/pull/1628">#1628</a>] perf(timeout): refactor new rpctimeout implementation to improve performance</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1564">#1564</a>][<a href="https://github.com/cloudwego/kitex/pull/1567">#1567</a>] perf: reduce object allocation for circuitbreak middleware and retry context</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1557">#1557</a>] perf(rpcinfo): remove lock for rpcinfo.RPCStats</p>
<h3 id="fix">Fix:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1622">#1622</a>] fix(generic): use jsoniter instead of sonic for json generic-call, since sonic doesn&rsquo;t support map[interface{}]interface{}</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1562">#1562</a>] fix: deep copy function of the generated code cannot copy the empty string</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1602">#1602</a>] fix(gRPC): check if the type assertion succeed in ProtocolMatch to avoid panic</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1598">#1598</a>] fix(retry): fix issue that mixed retry cannot update its config correctly</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1590">#1590</a>][<a href="https://github.com/cloudwego/kitex/pull/1572">#1572</a>] fix(generic): set default values for optional fields of primitive types with generic with dynamicgo</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1580">#1580</a>] fix(netpoll): fix timeout caused by partial use of the Read method of remote.ByteBuffer</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1574">#1574</a>] fix(trace): stream event handler ignore io.EOF event</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1563">#1563</a>] fix(generic): fix the issue where the generic client sets the parse mode of CombineServices and then requests causes &ldquo;unknown service&rdquo; error</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1568">#1568</a>] fix(wpool): fix the issue of wpool object allocation, and incorrect ctx causing profiler errors.</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1558">#1558</a>][<a href="https://github.com/cloudwego/kitex/pull/1555">#1555</a>] fix(bthrift): fix the issue of no recursion conversion of unknown field type under bthrift</p>
<h3 id="chore">Chore:</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1593">#1593</a>][<a href="https://github.com/cloudwego/kitex/pull/1560">#1560</a>][<a href="https://github.com/cloudwego/kitex/pull/1561">#1561</a>][<a href="https://github.com/cloudwego/kitex/pull/1559">#1559</a>] chore(test): fix data race issue, unstable issue and long time running issue of some test cases</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1634">#1634</a>][<a href="https://github.com/cloudwego/kitex/pull/1632">#1632</a>][<a href="https://github.com/cloudwego/kitex/pull/1573">#1573</a>] chore(dep): upgrade frugal, localsession and other cloudwego dependency versions</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1616">#1616</a>] chore(generic): remove deprecated apis/interfaces/variables</p>

---
title: "Blog: Kitex Release v0.15.1"
url: "https://www.cloudwego.io/blog/2025/09/29/kitex-release-v0.15.1/"
date: "Mon, 29 Sep 2025 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
<h2 id="introduction-to-key-changes"><strong>Introduction to Key Changes</strong></h2>
<h3 id="announcements"><strong>Announcements</strong></h3>
<ol>
<li><strong>Go Version Support Changes</strong>: Kitex&rsquo;s minimum declared Go version has been adjusted to Go1.20 and supports up to Go1.25
<ul>
<li>Currently does not affect Go v1.18/v1.19 compilation, but after being declared for higher versions, subsequent versions will introduce features of higher versions</li>
</ul>
</li>
<li><strong>Breaking Change for Partial interfaces</strong>: No impact on regular users, but may affect those with extensions or special api dependencies. For details, refer to the [<strong>Special Changes</strong>] section.</li>
</ol>
<h3 id="new-features"><strong>New Features</strong></h3>
<ol>
<li>
<p><strong>Generic Call: New v2 API Supporting Multi-Services and Streaming Calls</strong></p>
<p>The Thrift binary generic call API now provides v2 version, supporting multi-services and streaming calls. For detailed usage, see <a href="https://www.cloudwego.io/docs/kitex/tutorials/advanced-feature/generic-call/basic_usage/">Generic Call User Guide</a></p>
</li>
<li>
<p><strong>Generic Call: Support for Unknown Service Handler</strong></p>
<p>Facilitates rapid development of streaming proxy, see <a href="https://www.cloudwego.io/docs/kitex/tutorials/advanced-feature/proxy_application_development/">Proxy Application Development Guide</a> for details</p>
</li>
<li>
<p><strong>Generic Call: Support for Server-Level JSON/Map Streaming Generic Calls</strong></p>
<p>See: <a href="https://www.cloudwego.io/docs/kitex/tutorials/advanced-feature/generic-call/basic_usage/">Generic Call User Guide</a> for details</p>
</li>
<li>
<p><strong>TTHeader Streaming: Support for ctx Cancel to Control Flow Lifecycle</strong></p>
<ul>
<li>Quickly terminate streaming calls, saving model resources</li>
<li>Aligns with gRPC, for detailed usage see <a href="https://www.cloudwego.io/docs/kitex/tutorials/basic-feature/streamx/streamx_lifecycle_control/">Stream Lifecycle Control Best Practices</a></li>
<li>Supports Client actively invoking cancel to end streaming calls</li>
<li>Supports Client sensing the ctx cancel signal of the current Handler and cascading to end streaming calls</li>
</ul>
</li>
<li>
<p><strong>Streaming Error Handling Optimization</strong></p>
<ul>
<li>Quickly address specific error scenarios, accelerate troubleshooting of cascade cancel link issues, see <a href="https://www.cloudwego.io/docs/kitex/tutorials/basic-feature/streamx/streamx_error_handling/">Stream Error Handling Best Practices</a> for details</li>
<li>In cascade cancel scenarios, error description includes complete cancel link, quickly locating the first-hop service that actively cancels</li>
<li>Error description includes specific error scenarios and corresponding unique error codes</li>
<li>Unified and convenient cancel error handling method, eliminating the need for cumbersome string matching</li>
</ul>
</li>
</ol>
<h3 id="featureexperience-optimization"><strong>Feature/Experience Optimization</strong></h3>
<ol>
<li>
<p><strong>Generic Client: Optimize Background Goroutine Startup Logic</strong></p>
<p>Starting from Kitex v0.13.0, a generic client supports both Ping-Pong and streaming calls, and uses the TTHeader Streaming protocol by default. Each generic client automatically starts a background goroutine to clean up idle connections for TTHeader Streaming.</p>
<p>If users previously used the generic client incorrectly (e.g., creating a generic client for each request), upgrading to Kitex v0.13.x would result in a large number of background goroutines being created, leading to goroutine leaks, even though streaming generics are not actually used.</p>
<p>The v0.15.1 version only creates background goroutines when streaming generalization is actually used.</p>
</li>
</ol>
<h3 id="code-generation-tool-kitex-tool"><strong>Code Generation Tool Kitex Tool</strong></h3>
<ol>
<li>
<p><strong>Strict Enum Value Checking</strong></p>
<p>For scenarios where Thrift IDL defines enum value overflow, strict generation checks have been added, see <a href="https://www.cloudwego.io/docs/kitex/tutorials/code-gen/idl_enumeration_type/">Kitex Tool Enum Type Checking Instructions</a> for details</p>
<p>This change will cause some products to fail to generate because correctness already has issues, posing a significant risk to the service!</p>
</li>
</ol>
<h3 id="special-change---minor-services-may-be-affected"><strong>Special Change - Minor Services May Be Affected</strong></h3>
<blockquote>
<p>Interface Breaking Change that has no impact on 99.9% of users</p></blockquote>
<p>Kitex will ensure compatibility with normal usage patterns of internal users. However, individual users may have dependencies on definitions in the Kitex repository, and this version adjustment of Kitex will have an impact on these users.</p>
<p>This version has made minor adjustments to non-standard usage of <code>remote.Message</code>, <code>rpcinfo.RPCInfo</code> or <code>generic.Generic</code> interfaces. If there are special usages, they need to be adjusted to conform to the new version&rsquo;s interface definition.</p>
<ol>
<li><code>rpcinfo.RPCInfo().Invocation()</code> added <code>MethodInfo()</code> method, returning MethodInfo for the current RPC:</li>
</ol>
<div class="highlight"><pre tabindex="0"><code class="language-diff"><span style="display: flex;"><span>commit 62979e4b95e5a5ed73d0bfd9e218cfc61c5ce253
</span></span><span style="display: flex;"><span>type Invocation interface {
</span></span><span style="display: flex;"><span> PackageName() string
</span></span><span style="display: flex;"><span> ServiceName() string
</span></span><span style="display: flex;"><span> MethodName() string
</span></span><span style="display: flex;"><span><span style="color: #00a000;">+ MethodInfo() serviceinfo.MethodInfo
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;"></span> StreamingMode() serviceinfo.StreamingMode
</span></span><span style="display: flex;"><span> SeqID() int32
</span></span><span style="display: flex;"><span> BizStatusErr() kerrors.BizStatusErrorIface
</span></span><span style="display: flex;"><span>}
</span></span></code></pre></div><ol start="2">
<li><code>remote.Message</code> interface removed some redundant interfaces:</li>
</ol>
<div class="highlight"><pre tabindex="0"><code class="language-diff"><span style="display: flex;"><span> // Message is the core abstraction for Kitex message.
</span></span><span style="display: flex;"><span> type Message interface {
</span></span><span style="display: flex;"><span> RPCInfo() rpcinfo.RPCInfo
</span></span><span style="display: flex;"><span><span style="color: #a40000;">- ServiceInfo() *serviceinfo.ServiceInfo
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- SpecifyServiceInfo(svcName, methodName string) (*serviceinfo.ServiceInfo, error)
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;"></span> Data() interface{}
</span></span><span style="display: flex;"><span> NewData(method string) (ok bool)
</span></span><span style="display: flex;"><span> MessageType() MessageType
</span></span><span style="display: flex;"><span> SetPayloadLen(size int)
</span></span><span style="display: flex;"><span> TransInfo() TransInfo
</span></span><span style="display: flex;"><span> Tags() map[string]interface{}
</span></span><span style="display: flex;"><span><span style="color: #a40000;">- ProtocolInfo() ProtocolInfo
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- SetProtocolInfo(ProtocolInfo)
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;"></span> PayloadCodec() PayloadCodec
</span></span><span style="display: flex;"><span> SetPayloadCodec(pc PayloadCodec)
</span></span><span style="display: flex;"><span> Recycle()
</span></span><span style="display: flex;"><span> }
</span></span></code></pre></div><p>Dependencies on <code>ProtocolInfo()</code> should be modified to rely on <code>remote.Message().RPCInfo().Config().TransportProtocol()</code>.</p>
<ol start="3">
<li><code>generic.Generic</code> interface underwent significant adjustments:</li>
</ol>
<div class="highlight"><pre tabindex="0"><code class="language-diff"><span style="display: flex;"><span> commit 024fedbc2da33956cd81cd0a8226f817e5eac777
</span></span><span style="display: flex;"><span> // Generic ...
</span></span><span style="display: flex;"><span> type Generic interface {
</span></span><span style="display: flex;"><span> Closer
</span></span><span style="display: flex;"><span><span style="color: #a40000;">- // PayloadCodec return codec implement
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- // this is used for generic which does not need IDL
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- PayloadCodec() remote.PayloadCodec
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;"></span> // PayloadCodecType return the type of codec
</span></span><span style="display: flex;"><span> PayloadCodecType() serviceinfo.PayloadCodec
</span></span><span style="display: flex;"><span><span style="color: #a40000;">- // RawThriftBinaryGeneric must be framed
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- Framed() bool
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- // GetMethod is to get method name if needed
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- GetMethod(req interface{}, method string) (*Method, error)
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;"></span><span style="color: #00a000;">+ // GenericMethod return generic method func
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;">+ GenericMethod() serviceinfo.GenericMethodFunc
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;"></span> // IDLServiceName returns idl service name
</span></span><span style="display: flex;"><span> IDLServiceName() string
</span></span><span style="display: flex;"><span><span style="color: #a40000;">- // MessageReaderWriter returns reader and writer
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- // this is used for generic which needs IDL
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- MessageReaderWriter() interface{}
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;"></span><span style="color: #00a000;">+ // GetExtra returns extra info by key
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;">+ GetExtra(key string) interface{}
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;"></span> }
</span></span></code></pre></div><ul>
<li>The <code>PayloadCodec()</code> interface was completely removed. This adjustment was made because, after Kitex generic interface supported the multi-service feature, it no longer relies on hijacking PayloadCodec to inject the generic codec; instead, it&rsquo;s implemented by hijacking Args/Results structs. Currently, only <code>generic.BinaryThriftGeneric()</code> relies on the old method, but this interface has been marked as deprecated. Please migrate to using <code>generic.BinaryThriftGenericV2()</code>, refer to <a href="https://www.cloudwego.io/docs/kitex/tutorials/advanced-feature/generic-call/basic_usage/">Generic Call User Guide</a>.</li>
<li><code>Framed() bool</code> is a deprecated interface because Kitex has defaulted to framed mode for clients since v0.13.*.</li>
<li><code>MessageReaderWriter</code> and <code>GetMethod</code> interfaces are merged into a unified <code>GenericMethod()</code> interface. The new unified interface returns a closure function that accepts context and method name as arguments and returns the corresponding method info. This method info includes the hijacked Args/Results parameters, thus implementing different types of generic call codec logic.</li>
</ul>
<ol start="4">
<li><code>remote.ServiceSearcher</code> Get/Set method changes, <code>codec.SetOrCheckMethodName</code> parameter adjustment:</li>
</ol>
<div class="highlight"><pre tabindex="0"><code class="language-diff"><span style="display: flex;"><span>commit a1008887b9ab4553a79ce82cf6d3db324c344977
</span></span><span style="display: flex;"><span><span style="color: #a40000;">-const keyServiceSearcher = "rpc_info_service_searcher"
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;"></span><span style="color: #00a000;">+type keyServiceSearcher struct{}
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;"></span>
</span></span><span style="display: flex;"><span><span style="color: #a40000;">-// GetServiceSearcher returns the service searcher from rpcinfo.RPCInfo.
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">-func GetServiceSearcher(ri rpcinfo.RPCInfo) ServiceSearcher {
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- svcInfo, _ := ri.Invocation().Extra(keyServiceSearcher).(ServiceSearcher)
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- return svcInfo
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;"></span><span style="color: #00a000;">+// GetServiceSearcher returns the service searcher from context.
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;">+func GetServiceSearcher(ctx context.Context) ServiceSearcher {
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;">+ svcSearcher, _ := ctx.Value(keyServiceSearcher{}).(ServiceSearcher)
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;">+ return svcSearcher
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;"></span> }
</span></span><span style="display: flex;"><span>
</span></span><span style="display: flex;"><span><span style="color: #a40000;">-// SetServiceSearcher sets the service searcher to rpcinfo.RPCInfo.
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">-func SetServiceSearcher(ri rpcinfo.RPCInfo, svcSearcher ServiceSearcher) {
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- setter := ri.Invocation().(rpcinfo.InvocationSetter)
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;">- setter.SetExtra(keyServiceSearcher, svcSearcher)
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;"></span><span style="color: #00a000;">+// WithServiceSearcher sets the service searcher to context.
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;">+func WithServiceSearcher(ctx context.Context, svcSearcher ServiceSearcher) context.Context {
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;">+ return context.WithValue(ctx, keyServiceSearcher{}, svcSearcher)
</span></span></span><span style="display: flex;"><span><span style="color: #00a000;"></span> }
</span></span></code></pre></div><ul>
<li>The old version set <code>ServiceSearcher</code> on rpcinfo; the new version moves it to context to optimize Get/Set performance.</li>
</ul>
<div class="highlight"><pre tabindex="0"><code class="language-diff"><span style="display: flex;"><span>commit a1008887b9ab4553a79ce82cf6d3db324c344977
</span></span><span style="display: flex;"><span>// SetOrCheckMethodName is used to set method name to invocation.
</span></span><span style="display: flex;"><span><span style="color: #a40000;">-func SetOrCheckMethodName(methodName string, message remote.Message) error {
</span></span></span><span style="display: flex;"><span><span style="color: #a40000;"></span><span style="color: #00a000;">+func SetOrCheckMethodName(ctx context.Context, methodName string, message remote.Message) error {
</span></span></span></code></pre></div><ul>
<li>This simultaneously affects the definition of <code>codec.SetOrCheckMethodName</code>, adding <code>context.Context</code> as a parameter.</li>
</ul>
<h2 id="full-change"><strong>Full Change</strong></h2>
<h3 id="feature">Feature</h3>
<ul>
<li>feat(ttstream): support ctx cancel and detailed canceled error by @DMwangnima in <a href="https://github.com/cloudwego/kitex/pull/1821">#1821</a> | <a href="https://github.com/cloudwego/kitex/pull/1859">#1859</a> | <a href="https://github.com/cloudwego/kitex/pull/1856">#1856</a></li>
<li>feat(generic): support new thrift binary generic call api, server streaming generic call and unknown service or method handler by @jayantxie in <a href="https://github.com/cloudwego/kitex/pull/1837">#1837</a> | <a href="https://github.com/cloudwego/kitex/pull/1857">#1857</a></li>
<li>feat(grpc): support dump MaxConcurrentStreams of HTTP2 Client by @DMwangnima in <a href="https://github.com/cloudwego/kitex/pull/1820">#1820</a></li>
</ul>
<h3 id="fix">Fix</h3>
<ul>
<li>fix(retry): shallow copy response to avoid data race by @jayantxie in <a href="https://github.com/cloudwego/kitex/pull/1799">#1799</a> | <a href="https://github.com/cloudwego/kitex/pull/1814">#1814</a></li>
<li>fix(lbcache): check the existence before new Balancer to prevent leakage by @ppzqh in <a href="https://github.com/cloudwego/kitex/pull/1825">#1825</a></li>
<li>fix(generic): descriptor.HTTPRequest.GetParam nil pointer exception by @jayantxie in <a href="https://github.com/cloudwego/kitex/pull/1827">#1827</a></li>
<li>fix(generic): fix generic write int range check by @HeyJavaBean in <a href="https://github.com/cloudwego/kitex/pull/1861">#1861</a></li>
<li>fix(rpcinfo): protect bizErr and extra field of ri.Invocation by lock by @jayantxie in <a href="https://github.com/cloudwego/kitex/pull/1850">#1850</a></li>
<li>fix(timeout): remove timer pool to avoid timer race issue by @jayantxie in <a href="https://github.com/cloudwego/kitex/pull/1858">#1858</a></li>
<li>fix(tool): disable fast api for protobuf by @DMwangnima in <a href="https://github.com/cloudwego/kitex/pull/1807">#1807</a></li>
<li>fix(tool): skip pb code gen for arg -use by @xiaost in <a href="https://github.com/cloudwego/kitex/pull/1819">#1819</a></li>
</ul>
<h3 id="optimize">Optimize</h3>
<ul>
<li>optimize(grpc): access metadata.MD without ToLower by @xiaost in <a href="https://github.com/cloudwego/kitex/pull/1806">#1806</a></li>
<li>optimize(ttstream): lazy init cleaning task for ObjectPool to reduce the impact of lots of goroutines caused by creating too many Generic Client by @DMwangnima in <a href="https://github.com/cloudwego/kitex/pull/1842">#1842</a></li>
<li>optimize(tool): remove string deepcopy because the string type is read-only in Go by @jayantxie in <a href="https://github.com/cloudwego/kitex/pull/1832">#1832</a></li>
</ul>
<h3 id="refactor">Refactor</h3>
<ul>
<li>refactor(ttstream): remove ttstream provider by @jayantxie in <a href="https://github.com/cloudwego/kitex/pull/1805">#1805</a></li>
<li>refactor(rpcinfo): move service/method info from message to rpcinfo, remove protocol info from message and update min go version to 1.20 by @jayantxie in <a href="https://github.com/cloudwego/kitex/pull/1818">#1818</a> | <a href="https://github.com/cloudwego/kitex/pull/1855">#1855</a></li>
<li>refactor(server): remove service middleware and SupportedTransportsFunc api by @jayantxie in <a href="https://github.com/cloudwego/kitex/pull/1839">#1839</a></li>
<li>refactor(server): remove useless TargetSvcInfo field by @jayantxie in <a href="https://github.com/cloudwego/kitex/pull/1840">#1840</a></li>
</ul>
<h3 id="chore">Chore</h3>
<ul>
<li>chore: update dependencies of kitex to support go 1.25 and new features by @jayantxie @AsterDY in <a href="https://github.com/cloudwego/kitex/pull/1848">#1848</a> | <a href="https://github.com/cloudwego/kitex/pull/1834">#1834</a> | <a href="https://github.com/cloudwego/kitex/pull/1862">#1862</a> | <a href="https://github.com/cloudwego/kitex/pull/1836">#1836</a></li>
<li>chore: update version v0.15.0 by @jayantxie in <a href="https://github.com/cloudwego/kitex/pull/1864">#1864</a></li>
<li>docs: fix broken link to blogs by @scientiacoder in <a href="https://github.com/cloudwego/kitex/pull/1813">#1813</a></li>
<li>chore: support custom ctx key to pass to downstream in Service-Inline by @Duslia in <a href="https://github.com/cloudwego/kitex/pull/1709">#1709</a></li>
</ul>

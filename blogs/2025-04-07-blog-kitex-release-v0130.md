---
title: "Blog: Kitex Release v0.13.0"
url: "https://www.cloudwego.io/blog/2025/04/07/kitex-release-v0.13.0/"
date: "Mon, 07 Apr 2025 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
<blockquote>
<p>We recommend upgrading directly to Kitex version v0.13.1, as we have fixed a potential Goroutine leak issue of the gRPC Client in v0.13.0.</p></blockquote>
<h2 id="introduction-to-key-changes"><strong>Introduction to Key Changes</strong></h2>
<h3 id="new-features"><strong>New Features</strong></h3>
<ol>
<li>
<p><strong>New streaming interface StreamX supports gRPC, existing Kitex gRPC users can migrate</strong></p>
<p>v0.12.0 released the StreamX interface to optimise the streaming experience, and supported the custom streaming protocol TTHeader Streaming, but did not support gRPC. So existing users could not migrate.</p>
<p>This version supports gRPC for StreamX, users can migrate to StreamX, and the Server side can be compatible with two streaming protocols at the same time. So there is no need to worry about protocol compatibility after interface migration.</p>
<p>In particular, when adapting gRPC with StreamX, we found that there are still some inconvenient problems. In order to bring a better experience of using the interface, we have adjusted the StreamX interface for the second time, which will affect the users who have already been using StreamX. We apologise for that.</p>
<p>User documentation: <a href="https://www.cloudwego.io/docs/kitex/tutorials/basic-feature/streamx/">StreamX User Documentation</a></p>
</li>
<li>
<p><strong>Prutal - Protobuf&rsquo;s non-generated code serialisation library</strong></p>
<p><a href="https://github.com/cloudwego/prutal">Prutal</a> is officially open source, on par with Thrift&rsquo;s <a href="https://github.com/cloudwego/frugal">Frugal</a>, and the new version of Kitex integrates Prutal by default.</p>
<p>Advantages:</p>
<ul>
<li>
<p>Minimized Code Product Size: Generating Only Structures, No Runtime Code</p>
</li>
<li>
<p>Leveraging Reflection Optimization Similar to Frugal, Achieving Over 50% Speed Increase</p>
</li>
<li>
<p>Generating Code Compatible with Existing Protobuf and Derivative Versions</p>
</li>
</ul>
<p>User documentation: <a href="https://www.cloudwego.io/docs/kitex/tutorials/code-gen/prutal/">Prutal</a></p>
</li>
</ol>
<h3 id="featureexperience-optimization"><strong>Feature/Experience Optimization</strong></h3>
<ol>
<li>
<p><strong>TTHeader Streaming: Support interface-level Recv timeout control</strong></p>
<p>In addition to the existing Client level, this release of TTHeader Streaming supports interface-level Recv timeout configuration, making configuration more flexible.</p>
<p>User documentation: <a href="https://www.cloudwego.io/docs/kitex/tutorials/basic-feature/streamx/streamx_timeout_control/">StreamX Timeout Control</a></p>
</li>
</ol>
<h3 id="special-change"><strong>Special Change</strong></h3>
<ol>
<li>
<p><strong>Default Thrift transport protocol changed from Buffered to Framed</strong></p>
<p>This change leverages FastCodec for higher codec performance. Since Kitex server supports protocol detection, this behavioral change is compatible. Framed protocol is generally supported by most thrift frameworks, and we assess the impact to be minimal. However, if the downstream does not support Framed protocol, please manually revert to the Buffered protocol as follows:</p>
</li>
</ol>
<div class="highlight"><pre tabindex="0"><code class="language-go"><span style="display: flex;"><span><span style="color: #000;">cli</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #ce5c00; font-weight: bold;">:=</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">xxx</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">NewClient</span><span style="color: #000; font-weight: bold;">(</span><span style="color: #4e9a06;">"service_name"</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">client</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">WithTransportProtocol</span><span style="color: #000; font-weight: bold;">(</span><span style="color: #000;">transport</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">PurePayload</span><span style="color: #000; font-weight: bold;">))</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span></code></pre></div><h3 id="others"><strong>Others</strong></h3>
<ol>
<li><strong>Code Product Simplification</strong></li>
</ol>
<ul>
<li>
<p>Kitex Tool would not generate the repeated verification code for Set data structure and the <code>DeepEqual</code> function for each structure by default.</p>
<ul>
<li>
<p>If you only want to restore<code>DeepEqual</code>, add<code>-thrift gen_deep_equal=true</code>to the generation command.</p>
</li>
<li>
<p>If you want to restore the repeated verification of Set, add<code>-thrift validate_set=true, -thrift gen_deep_equal=true</code>to the generation command.</p>
</li>
</ul>
</li>
<li>
<p>Kitex Tool would not generate the Apache Codec related code by default.</p>
<ul>
<li>If you want to restore it, add<code>-thrift no_default_serdes=false</code>to the generation command.</li>
</ul>
</li>
</ul>
<ol start="2">
<li>
<p><strong>Go Supported Version Change</strong></p>
<p>Support version Go 1.19~1.24, the lowest supported version becomes Go 1.19.</p>
<p>if Go version is too low, there will be a prompt when compiling:<code>note: module requires Go 1.19</code>.</p>
</li>
</ol>
<h2 id="full-change"><strong>Full Change</strong></h2>
<h3 id="feature">Feature</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1719">#1719</a>] feat: prutal for replacing protoc</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1736">#1736</a>] feat(ttstream): support WithRecvTimeout stream call option</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1702">#1702</a>] feat(gRPC): add grpc client conn dump to help debug the conn and stream status</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1723">#1723</a>] feat(codec/thrift): use fastcodec/frugal if apache codec not available</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1724">#1724</a>] feat: add tail option to support for delayed initialization of some client options</p>
<h3 id="optimize">Optimize</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1728">#1728</a>] optimize(apache): remove apache codec gen and set default protocol from buffered to framed</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1732">#1732</a>] optimize(rpcinfo): purify the transport protocol of rpcinfo in a single rpc request</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1711">#1711</a>] optimize(tool): disable set validate and deep equal code gen to simplify kitex_gen</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1717">#1717</a>] optimize(gRPC): return more detailed error when received invalid http2 frame</p>
<h3 id="fix">Fix</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1734">#1734</a>] fix(ttstream): adjust stream state transition and remove all SetFinalizer to avoid memory leak</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1735">#1735</a>] fix(generic): support both relative and absolute check for idl includes parse to make it compatible with generation tool</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1725">#1725</a>] fix: code gen import issue for streamx mode, stream call judgement bug and set ttheader streaming as default</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1727">#1727</a>] fix(tool): fix tool UseStdLib remains unexpected lib issue</p>
<h3 id="refactor">Refactor</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1658">#1658</a>] refactor: streamx api to adapt both grpc and ttheader streaming protocol and provide more user-friendly interface</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1729">#1729</a>] refactor(tool): move pb tpl code to sep pkg</p>
<h3 id="chore">Chore</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1743">#1743</a>] chore: update dependencies version</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1740">#1740</a>] chore(generic): deprecate NewThriftContentProvider</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1741">#1741</a>] chore(streamx): remove redundant streamx package</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1738">#1738</a>] ci: fix typos &amp; crate-ci/typos</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1737">#1737</a>] chore: update dependency and change go support to 1.19-1.24</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1720">#1720</a>] Revert &ldquo;fix(ttstream): pingpong method refers to server interface defined in Kitex generation code when streamx is enabled and there are other streaming methods&rdquo;</p>

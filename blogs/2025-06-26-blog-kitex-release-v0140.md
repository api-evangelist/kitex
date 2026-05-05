---
title: "Blog: Kitex Release v0.14.0"
url: "https://www.cloudwego.io/blog/2025/06/26/kitex-release-v0.14.0/"
date: "Thu, 26 Jun 2025 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
<h2 id="introduction-to-key-changes"><strong>Introduction to Key Changes</strong></h2>
<h3 id="new-features"><strong>New Features</strong></h3>
<ol>
<li>
<p><strong>Generic Call: The generic Client supports streaming calls, allowing a single Client to handle both streaming and non-streaming scenarios</strong></p>
<p>It supports streaming generic calls, adapting to gRPC/TTHeader Streaming and supporting map/JSON and Protobuf binary generic calls.</p>
<p>A brief code example is as follows:</p>
<div class="highlight"><pre tabindex="0"><code class="language-go"><span style="display: flex;"><span><span style="color: #000;">cli</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">err</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #ce5c00; font-weight: bold;">:=</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">genericclient</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">NewClient</span><span style="color: #000; font-weight: bold;">(</span><span style="color: #4e9a06;">"actualServiceName"</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">g</span><span style="color: #000; font-weight: bold;">)</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"></span><span style="color: #8f5902; font-style: italic;">// Ping-Pong generic</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"></span><span style="color: #000;">resp</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">err</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #ce5c00; font-weight: bold;">:=</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">cli</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">GenericCall</span><span style="color: #000; font-weight: bold;">(</span><span style="color: #000;">ctx</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #4e9a06;">"PingPongTest"</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">req</span><span style="color: #000; font-weight: bold;">)</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"></span><span style="color: #8f5902; font-style: italic;">// ClientStreaming generic</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"></span><span style="color: #000;">cliStream</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">err</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #ce5c00; font-weight: bold;">:=</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">cli</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">ClientStreaming</span><span style="color: #000; font-weight: bold;">(</span><span style="color: #000;">ctx</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #4e9a06;">"ClientStreamingTest"</span><span style="color: #000; font-weight: bold;">)</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"></span><span style="color: #8f5902; font-style: italic;">// ServerStreaming generic</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"></span><span style="color: #000;">srvStream</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">err</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #ce5c00; font-weight: bold;">:=</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">cli</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">ServerStreaming</span><span style="color: #000; font-weight: bold;">(</span><span style="color: #000;">ctx</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #4e9a06;">"ServerStreamingTest"</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">req</span><span style="color: #000; font-weight: bold;">)</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"></span><span style="color: #8f5902; font-style: italic;">// BidiStreaming generic</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span><span style="display: flex;"><span><span style="color: #f8f8f8; text-decoration: underline;"></span><span style="color: #000;">bidiStream</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">err</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #ce5c00; font-weight: bold;">:=</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #000;">cli</span><span style="color: #000; font-weight: bold;">.</span><span style="color: #000;">BidiStreaming</span><span style="color: #000; font-weight: bold;">(</span><span style="color: #000;">ctx</span><span style="color: #000; font-weight: bold;">,</span><span style="color: #f8f8f8; text-decoration: underline;"> </span><span style="color: #4e9a06;">"BidiStreamingTest"</span><span style="color: #000; font-weight: bold;">)</span><span style="color: #f8f8f8; text-decoration: underline;">
</span></span></span></code></pre></div><p>Refer to this document for details: <a href="https://www.cloudwego.io/docs/kitex/tutorials/advanced-feature/generic-call/basic_usage/">Generic Call</a>.</p>
</li>
</ol>
<h3 id="featureexperience-optimization"><strong>Feature/Experience Optimization</strong></h3>
<ol>
<li>
<p><strong>Streaming: Improved observability and debugging experience</strong></p>
<p><strong>TTHeader Streaming</strong></p>
<ul>
<li>If Tracer configured, failure to create a stream will now be reported with metrics.</li>
<li>When a panic occurs on the Server side, the full stack trace will now be printed for easier troubleshooting.</li>
</ul>
<p><strong>gRPC Streaming</strong></p>
<ul>
<li>If Tracer configured, failure to create a stream will now be reported with metrics.</li>
</ul>
</li>
</ol>
<h3 id="others"><strong>Others</strong></h3>
<ol>
<li>
<p><strong>Code Product Simplification</strong></p>
<p>Kitex tool no longer generates fastpb, only affecting Protobuf users.</p>
<p>If high-performance Protobuf encoding/decoding is required, you can enable prutal by configuring environment variable <code>KITEX_TOOL_USE_PRUTAL_MARSHAL=1</code>.</p>
</li>
</ol>
<h2 id="full-change"><strong>Full Change</strong></h2>
<h3 id="feature">Feature</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1759">#1759</a>] feat(tool): add env for using prutal to marshal</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1782">#1782</a>] feat(ttstream): process MetaFrame and reflect to rpcinfo</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1777">#1777</a>] feat(client): report err when create Stream failed</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1763">#1763</a>] feat: support ttheader streaming generic call</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1771">#1771</a>] feat(tool): add thriftgo patcher extension</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1755">#1755</a>] feat: add generic binary pb for streamx</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1752">#1752</a>] feat(generic): support generic pb binary for streaming</p>
<h3 id="optimize">Optimize</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1788">#1788</a>] optimize: go net implementation</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1786">#1786</a>] optimize(tool): remove tool fastpb generation</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1783">#1783</a>] optimize(gRPC): parse PayloadCodec in server side</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1780">#1780</a>] optimize(ttstream): log the error thrown by invoking handler</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1769">#1769</a>] optimize: injection of options in ttstream</p>
<h3 id="fix">Fix</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1792">#1792</a>] fix(gRPC): inject current method name to rpcinfo in server-side to fix FROM_METHOD missing</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1787">#1787</a>] fix(ttstream): metrics missing caused by server-side rpcinfo not set correctly</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1778">#1778</a>] fix: enabling json mode of map generic not work</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1774">#1774</a>] fix(server): trans server conn count race issue</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1742">#1742</a>] fix(generic): align dynamicgo&rsquo;s write base behavior with old generic (only for internal logic)</p>
<h3 id="refactor">Refactor</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1770">#1770</a>] refactor: refactor generic streaming</p>
<h3 id="test">Test</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1793">#1793</a>] test: add go1.18 to scenario-test</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1765">#1765</a>] refactor: refactor generic streaming</p>
<h3 id="docs">Docs</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1794">#1794</a>] docs: update CONTRIBUTING.md to change PR base branch to main</p>
<h3 id="chore">Chore</h3>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1795">#1795</a>] chore: update dependency</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1776">#1776</a>] chore: remove testify dependency</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1757">#1757</a>] chore: update prutal to v0.1.1</p>
<p>[<a href="https://github.com/cloudwego/kitex/pull/1753">#1753</a>] ci: disable codecov annotations</p>

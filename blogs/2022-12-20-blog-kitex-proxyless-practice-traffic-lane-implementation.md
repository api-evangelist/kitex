---
title: "Blog: Kitex Proxyless Practice：Traffic Lane Implementation with Istio and OpenTelemetry"
url: "https://www.cloudwego.io/blog/2022/12/20/kitex-proxyless-practicetraffic-lane-implementation-with-istio-and-opentelemetry/"
date: "Tue, 20 Dec 2022 00:00:00 +0000"
author: ""
feed_url: "https://www.cloudwego.io/index.xml"
---
Preface: Kitex Proxyless enables the Kitex service to interact directly with istiod without envoy sidecar. It dynamically obtains service governance rules delivered by the control plane based on the xDS protocol and converts them to Kitex rules to implement some service governance functions, such as traffic routing. Based on Kitex Proxyless, Kitex can be managed by Service Mesh without sidecar.

---
title: Spring PetClinic SpringBoot Based Microservices On Kubernetes
linkTitle: PetClinic Kubernetes Workshop
weight: 2
archetype: chapter
authors: ["Pieter Hagen"]
description: Learn how to enable automatic discovery and configuration for your Java-based application running in Kubernetes. Experience real-time monitoring to help you maximize application behavior with end-to-end visibility.
time: 90 minutes
---

The goal of this workshop is to introduce the features of Splunk's **automatic discovery and configuration** for Java.

The workshop scenario will be created by installing a simple (**un-instrumented**) Java microservices application in Kubernetes.

Following simple steps to install the Splunk OpenTelemetry Collector with automatic discovery for existing Java based deployments, we will see how easy it is to send metrics, traces and logs to **Splunk Observability Cloud**.

> [!SPLUNK]Prerequisites
>
> * Outbound SSH access to port **2222**.
> * Outbound HTTP access to port **81**.
> * Familiarity with the Linux command line.

During this workshop we will cover the following components:

* Splunk Infrastructure Monitoring (**IM**)
* Splunk automatic discovery and configuration for Java (**APM**)
  * Database Query Performance
  * AlwaysOn Profiling
* Splunk Log Observer (**LO**)
* Splunk Real User Monitoring (**RUM**)

_Splunk Synthetics is feeling a little left out here, but we cover that in other workshops_ {{% icon icon="heart" %}}

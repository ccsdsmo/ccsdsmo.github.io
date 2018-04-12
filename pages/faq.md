---
layout: page
title: FAQ
weight: 9
permalink: /faq
---

* TOC {:toc}

### Is a subscription needed to receive telemetry? / How does commanding-in-the-blind work?

This is foreseen using hardcoded aggregations, as written in the [M&C book, page 2-11](https://public.ccsds.org/Pubs/522x1b1.pdf):

> In many situations it is expected that basic summary or overview information about the state of a system or spacecraft be published without an initial consumer request. For example, for safety reasons it is normal for a spacecraft to broadcast basic status information when in recovery/safe mode to help diagnose any communication issues that might exist.
>
> Whilst no operations for this situation have been explicitly defined it should be noted that it is completely valid for a service provider to publish these aggregation updates without having received a subscription request from a consumer. In this situation the registration request from the consumer is hardcoded into the provider application, the MO publish/subscribe concept is not modified but in effect parts of it have been hardcoded into the deployment.

### How does Parameter time-stamping work in the Aggregation Service?

The Aggregation Service allows the monitoring of multiple Parameters simultaneously. Inside an Aggregation, Parameters are grouped into Parameter Sets. Therefore an Aggregation is a list of Parameter Sets.
Each Parameter Set has two Time related values, deltaTime and intervalTime.

* _deltaTime_ is the time between a Parameter Set and it's previous. If the Parameter Set is the first, then deltaTime is relative to the aggregation's report timestamp (i.e. the MAL message delivering the aggregation).
* _intervalTime_ is the time between each Parameter in a Parameter Set.

Note that both deltaTime and intervalTime are optional fields, the default value is 0.

### What accuracy can be supported for aggregations?

Timestamp intervals in the Aggregations are defined using the Duration field type as defined in the [Message Abstraction Layer](https://public.ccsds.org/Pubs/521x0b2e1.pdf).

> The Duration structure (...) represents a length of time in seconds. It may contain a fractional component.

The accuracy of the duration field is then defined per deployment via what is named a Mapping Configuration Parameters.

For example the [Space Packet Transport Binding and Binary Encoding](https://public.ccsds.org/Pubs/524x1b1.pdf) states that the Duration field is configured using: P-Field of the [CUC Time Code Format](https://public.ccsds.org/Pubs/301x0b2s.pdf).

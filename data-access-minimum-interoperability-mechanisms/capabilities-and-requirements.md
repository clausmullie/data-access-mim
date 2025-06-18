---
# SPDX-License-Identifier: CC0-1.0
# SPDX-FileCopyrightText: Authors
---

# MIM0: Data Access (mvp 0.3)

## Table of contents

- [Objective](#objective)
- [Capabilities and Requirements](#capabilities-and-requirements)

## Objective

Facilitate the ways data can be accessed, once data sets are discovered and agreements are in place.

## Capabilities and requirements

The key words MAY, MUST, MUST NOT, and SHOULD in this document are to be interpreted as described in [BCP 14](https://www.rfc-editor.org/info/bcp14), [[RFC2119](https://www.rfc-editor.org/rfc/rfc2119)], [[RFC8174](https://www.rfc-editor.org/rfc/rfc8174)] when, and only when, they appear in all capitals, as shown here. 

### C.1 Data Access Modalities

Public sector data systems should support a variety of standardized methods for accessing data, including downloads, subscriptions, streams, and real-time feeds, to ensure flexibility and usability for different types of users and use cases.

#### Requirements

- Data **MUST** be retrievable via at least one standard web-based mechanism  
- Systems **MUST** allow retrieval of data in at least one machine-readable format  

### C.2 API Interface and Behavior

APIs provided for data access should be well-structured, documented, and adhere to best practices for interface design and behavior, enabling consistent, predictable, and interoperable integration across systems.

#### Requirements

- APIs **MUST** be documented using a machine-readable specification  
- APIs **MUST** support standard content negotiation  
- APIs **MUST** include metadata for last modified timestamp, available data formats, pagination, and rate limits  
- APIs **MUST** return appropriate HTTP status codes and error messages  
- APIs **MUST** follow RESTful URL conventions with predictable endpoint structures  

### C.3 Direct File Download Capability

Systems should provide direct file download access as a simple, universal method for data retrieval that works without API complexity and enables bulk data access.

#### Requirements

In situations where API access is not possible:
- Data **MUST** be available for direct download in at least one structured format (See MIM3)
- Download URLs **MUST** be stable and predictable  

### C.4 Publish & Subscribe Mechanisms

#### C.4.1 Message Queue Integration Capability

Support asynchronous data delivery through standardized messaging protocols for reliable, high-throughput integration between systems.

#### Requirements

- Systems **MUST** implement at least one standard messaging protocol (AMQP, Apache Kafka, or MQTT)  
- Systems **MUST** support structured message formats (see MIM1)  
- Systems **MUST** provide message acknowledgment mechanisms  
- Systems **MUST** ensure at-least-once delivery guarantees  
- Systems **MUST** implement durable message storage for critical data  

#### C.4.2 Real-Time Data Streaming Capability

Enable continuous data delivery through standardized streaming protocols for applications requiring up-to-date information.

#### Requirements

- Systems **MUST** support at least one streaming protocol (WebSockets, Server-Sent Events, or HTTP/2 streaming)  
- Systems **MUST** send structured data payloads (JSON format minimum)  
- Systems **MUST** include timestamps and sequence identifiers in stream messages  
- Systems **MUST** provide connection heartbeat or keep-alive mechanisms  
- Systems **MUST** handle client disconnections gracefully with reconnection support  

### C.5 Metadata

The system is capable of generating and exposing metadata that describes datasets in a consistent, machine-readable format.

#### Requirements

- Systems **MUST** provide consistent and clear metadata accompanying datasets  
- Metadata **MUST** be available in a machine-readable format  

### C.6 Data Access Reliability and Quality

The system ensures that data access is governed by a published Service License Agreement (SLA) defining uptime, performance, and quality metrics.

#### Requirements

- API access **MUST** include a Service License Agreement  

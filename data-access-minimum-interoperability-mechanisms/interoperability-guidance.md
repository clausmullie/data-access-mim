<!--
# SPDX-License-Identifier: CC0-1.0
# SPDX-FileCopyrightText: Authors
-->

# Interoperability Guidance

This provides additional context and clarification to the Data Access Minimum Interoperability Mechanism.

## Table of contents

- [Capabilities and Requirements](#capabilities-and-requirements)

### C.1 Data Access Modalities

#### Additional best practice to consider:

* Data **SHOULD** be available in common downloadable formats (see MIM3)
* Systems **SHOULD** support bulk data access or export
* Systems **SHOULD** provide at least one subscription mechanism
* Systems **SHOULD** provide real-time data streaming when appropriate
* Time series datasets **SHOULD** allow querying over specified time ranges
* Systems **MAY** support access via message queue systems

### C.2 API Interface and Behavior

#### Additional best practice to consider:

* APIs **SHOULD** support retrieval of current data
* APIs **SHOULD** support retrieval of historical data when applicable
* APIs **SHOULD** support geospatial querying when applicable (see MIM7)
* APIs **SHOULD** support subscription to changes when applicable
* APIs **SHOULD** expose next expected update timestamp
* APIs **SHOULD** support explicit versioning of endpoints
* APIs **SHOULD** provide example payloads or test queries
* APIs **SHOULD** support standard HTTP caching headers
* APIs **SHOULD** communicate rate limit status via standard HTTP headers
* APIs **SHOULD** return structured error bodies
* APIs **MAY** support partial responses or query projections
* APIs **MAY** expose a standard health/status endpoint
* APIs **MAY** support pagination for datasets exceeding 1000 records

### C.3 Direct File Download Capability

#### Additional best practice to consider:

* Downloaded files **SHOULD** include metadata headers or companion files
* Systems **SHOULD** provide both full and incremental data exports

### C.4 Publish & Subscribe Mechanisms

#### C.4.1 Message Queue Integration Capability

#### Additional best practice to consider:

* Systems **SHOULD** support topic-based message routing
* Systems **SHOULD** provide message ordering guarantees within partitions/topics
* Systems **SHOULD** implement configurable retention policies
* Systems **SHOULD** support batch message processing
* Systems **SHOULD** provide monitoring and metrics for queue health
* Systems **MAY** support exactly-once delivery semantics
* Systems **MAY** implement message filtering or routing rules
* Systems **MAY** support multiple consumer groups

#### C.4.2 Real-Time Data Streaming Capability

#### Additional best practice to consider:

* Systems **SHOULD** support client-side filtering or subscription parameters
* Systems **SHOULD** implement backpressure handling for slow consumers
* Systems **SHOULD** provide stream replay capability for recent data
* Systems **SHOULD** support multiple concurrent streaming connections
* Systems **MAY** support compression for high-volume streams
* Systems **MAY** implement stream checkpointing for reliability

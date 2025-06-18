<!--
# SPDX-License-Identifier: CC0-1.0
# SPDX-FileCopyrightText: Authors
-->

# Readers guide

This readers guide provides additional context and clarification to the Data Access Minimum Interoperability Mechanism.

## Table of contents

- [Capabilities and Requirements](#capabilities-and-requirements)
- [Mechanisms](#mechanisms)
- [Interoperability Guidance](#interoperability-guidance)
- [Conformance and Compliance Testing](#conformance-and-compliance-testing)

### C.1 Data Access Modalities

**Data MUST be retrievable via at least one standard web-based mechanism**

You must be able to get the data using a regular web browser, just like visiting any website.
No special software is needed.
This ensures universal accessibility and lowers the barrier for entry.

**Systems MUST allow retrieval of data in at least one machine-readable format**

The data must be in a format that computers can easily understand and process.
These formats enable seamless integration with software applications, analytics tools, and automated workflows.
This is useful when building dashboards, conducting data analysis, or integrating data into third-party systems.

#### Additional best practice to consider:

* Data **SHOULD** be available in common downloadable formats (see MIM3)
* Systems **SHOULD** support bulk data access or export
* Systems **SHOULD** provide at least one subscription mechanism
* Systems **SHOULD** provide real-time data streaming when appropriate
* Time series datasets **SHOULD** allow querying over specified time ranges
* Systems **MAY** support access via message queue systems

### C.2 API Interface and Behavior

**APIs MUST be documented using a machine-readable specification**

The instructions for interacting with the API must be provided in a standardized format like OpenAPI/Swagger.
This allows tools and developers to automatically understand and test the API.
It reduces implementation time and minimizes errors.
It is especially useful for teams building client applications or services that consume the API.

**APIs MUST support standard content negotiation**

The API should be able to return data in multiple formats (e.g., JSON or XML) based on what the client requests.
This supports flexibility in integration.
It is useful in multi-platform environments where legacy systems and modern apps coexist.

**APIs MUST include metadata for last modified timestamp, available data formats, pagination, and rate limits**

The API must communicate key information such as the last update time of the data, the formats in which data is available, pagination details for large datasets, and any restrictions on access frequency.
This helps clients manage data freshness, optimize data access, and avoid service interruptions.
This is particularly useful in high-frequency applications like sensor data monitoring.

**APIs MUST return appropriate HTTP status codes and error messages**

The API must use standard HTTP status codes (e.g., 200, 404, 429) and provide meaningful error messages to indicate the success or failure of requests.
This improves troubleshooting, debugging, and overall developer experience.
This is essential in any production environment where reliability and transparency are important.

**APIs MUST follow RESTful URL conventions with predictable endpoint structures**

The structure of API URLs should follow clear and consistent RESTful patterns.
This makes it easier for developers to intuitively understand and use the API without constantly referring to documentation.
It is especially useful for large APIs with multiple endpoints, as it improves discoverability and consistency.

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

**In situations where API access is not possible: Data MUST be available for direct download in at least one structured format (CSV, JSON, or XML)**

If APIs are unavailable or not suitable, users should still be able to download the data as files in structured formats.
This ensures that access is not dependent on programmatic tools.
It is useful for offline analysis or archival purposes.

**Download URLs MUST be stable and predictable**

The URLs for downloading data should remain consistent over time to prevent breaking integrations or automated workflows.
Stable URLs allow users to set up recurring downloads and ensure continuity of data access.
This is particularly useful in scripts, batch processes, and long-term projects.

#### Additional best practice to consider:

* Downloaded files **SHOULD** include metadata headers or companion files
* Systems **SHOULD** provide both full and incremental data exports

### C.4 Publish & Subscribe Mechanisms

#### C.4.1 Message Queue Integration Capability

**Systems MUST implement at least one standard messaging protocol (AMQP, Apache Kafka, or MQTT)**

The system must support a common, industry-accepted messaging protocol to facilitate interoperability with other systems.
This allows data to be distributed efficiently and reliably across services.
It is especially useful in large-scale distributed systems or IoT applications.

**Systems MUST support structured message formats (see MIM1)**

Messages exchanged must follow a defined and parsable structure, such as JSON or Protobuf.
This enables automated processing and ensures that receiving systems can interpret the data correctly.

**Systems MUST provide message acknowledgment mechanisms**

The system must include a way for message recipients to confirm receipt.
This ensures delivery assurance and enables fault-tolerant communication.
It is particularly important in systems where data loss is unacceptable.

**Systems MUST ensure at-least-once delivery guarantees**

Every message should be delivered to its recipient at least once.
Although duplicates may occur, this guarantee ensures reliability in communication.
This is useful in scenarios like telemetry, where missing data is more problematic than repeated entries.

**Systems MUST implement durable message storage for critical data**

Messages must be stored in a persistent manner to survive system failures.
This protects against data loss and supports replay functionality if needed.
This is vital in mission-critical applications like emergency response.

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

**Systems MUST support at least one streaming protocol (WebSockets, Server-Sent Events, or HTTP/2 streaming)**

The system must enable continuous real-time data flow using a standard streaming protocol.
This facilitates instant data delivery for applications requiring live updates.
It is especially useful in sensor monitoring.

**Systems MUST send structured data payloads (JSON format minimum)**

Real-time messages must use a consistent and machine-readable format.
This ensures the data can be parsed and used immediately by clients.
Structured payloads are essential in environments requiring automated decisions or actions.

**Systems MUST include timestamps and sequence identifiers in stream messages**

Each message should contain a time and order indicator to help reconstruct event sequences and detect missing or out-of-order data.
This is critical for auditing, synchronization, and data integrity in real-time systems.

**Systems MUST provide connection heartbeat or keep-alive mechanisms**

The system should periodically send signals to confirm an active connection.
This helps detect connection failures promptly.
It’s especially useful in networks with unstable connections or mobile environments.

**Systems MUST handle client disconnections gracefully with reconnection support**

If a client disconnects, the system must support automatic or manual reconnection without data loss.
This ensures robust data delivery even in the face of network disruptions.
It is particularly beneficial in mobile or remote deployments.

#### Additional best practice to consider:

* Systems **SHOULD** support client-side filtering or subscription parameters
* Systems **SHOULD** implement backpressure handling for slow consumers
* Systems **SHOULD** provide stream replay capability for recent data
* Systems **SHOULD** support multiple concurrent streaming connections
* Systems **MAY** support compression for high-volume streams
* Systems **MAY** implement stream checkpointing for reliability

### C.5 Metadata (or also MIM3?)

**Systems MUST provide consistent and clear metadata accompanying datasets**

Metadata must describe the dataset clearly, including source, scope, structure, and update frequency.
This helps users understand the context and usability of the data.
This is especially helpful for researchers, data scientists, and policy analysts.

**Metadata MUST be available in a machine-readable format**

Metadata must be provided in formats like JSON, XML, or RDF to enable automated cataloging and discovery.
This supports data interoperability and integration across platforms.
This is useful in data portals and knowledge graphs.

### C.6 Data access reliability and quality

**API access MUST include a Service License Agreement**

The API must be accompanied by a legal agreement outlining terms of use, limitations, and responsibilities.
This establishes trust, sets expectations, and reduces risk for both providers and consumers.
This is essential in enterprise and government data services.

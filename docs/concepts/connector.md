# Connector

Connectors are designed to interface with external APIs, services, and systems. The architecture usually consists of:

* **Connector Definition:** The connector defines the interaction schema, including the authentication method, supported API endpoints, data formats, and necessary configurations. This may include OAuth tokens, API keys, or other authentication mechanisms.
* **API Gateway:** The API Gateway acts as an intermediary between the platform and the external services. It ensures that requests made by the PaaS platform are routed correctly and that responses are handled efficiently.
* **Data Transformation:** Often, data returned by an external service isn’t in the right format for use within the platform. A connector will handle data transformation—converting it into a consistent, structured format that can be processed by the platform.
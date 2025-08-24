# Glossary

This glossary defines key terms and concepts used throughout the Open PaaS Platform documentation. Use this reference to understand platform-specific terminology and technical concepts.

## API Key
A unique identifier used to authenticate requests to external services. API keys provide programmatic access with configurable permissions and rate limits.

## Batch Processing
Processing large volumes of data in scheduled jobs or bulk operations. Optimized for resource-intensive transformations with progress tracking and resumable operations.

## Connector
A component that interfaces with external APIs, services, and systems. Connectors handle authentication, data transformation, and communication protocols to integrate external services with the Open PaaS Platform.

## Event Handler
Processes asynchronous events from webhooks, message queues, and internal triggers. Ensures reliable event delivery and supports event replay for debugging.

## OAuth 2.0
An authorization framework that enables applications to obtain limited access to user accounts. Used for secure authentication with external services.

## Real-time Processing
Immediate processing of streaming data with sub-second latency requirements. Optimized for webhook processing, live data synchronization, and instant notifications.

## SDK (Software Development Kit)
Native libraries for Python and Node.js that provide type-safe interfaces for all platform operations. Handles authentication, connection management, and API interactions.

## Webhook
HTTP callbacks that external services send to notify your application of events. The platform processes webhooks through the Event Handler for real-time integrations.

## Workflow Orchestrator
Manages complex multi-step processes with dependencies. Supports conditional logic, parallel execution, and error handling across multiple external systems.
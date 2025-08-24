# Data Ingestion with Open PaaS Platform

This guide explains how to ingest data from various external sources into the Open PaaS Platform. Follow these steps to set up data connectors, configure field mappings, and establish automated data ingestion workflows.

---

## Before You Begin

Ensure you have the following:

- Access to Open PaaS Platform with data ingestion permissions
- External data source credentials (API keys, database connections, etc.)
- Basic understanding of data formats (JSON, CSV, XML)
- Python 3.x and the Open PaaS Platform SDK installed
- Familiarity with the platform basics from [Create Your First Connector](../getting-started/quick-start.md)

## Create Data Ingestion Connector

1. identify and configure your data source:

    ```python
    from openpaas_sdk import OpenPaaSClient, DataConnector

    # Initialize the platform client
    client = OpenPaaSClient(api_key="your_api_key")

    # Create a data connector for REST API
    api_connector = DataConnector(
        name="customer_data_api",
        source_type="rest_api",
        config={
            "base_url": "https://api.yourservice.com/v1",
            "auth_type": "bearer_token",
            "auth_token": "your_api_token",
            "rate_limit": 100  # requests per minute
        }
    )
    ```

2. Configure Data Mapping: Define how external data maps to your platform schema:

    ```python
    # Define field mappings
    api_connector.add_field_mapping({
        "external_customer_id": "customer_id",
        "full_name": "name", 
        "email_address": "email",
        "created_at": "registration_date",
        "subscription_tier": "plan_type"
    })

    # Set data types and validation rules
    api_connector.add_validation_rules({
        "customer_id": {"type": "string", "required": True},
        "email": {"type": "email", "required": True},
        "registration_date": {"type": "datetime", "format": "ISO8601"}
    })
    ```

3. Test the Connection: Verify your connector works before full deployment:

    ```python
    # Test connection and data retrieval
    test_result = api_connector.test_connection()
    if test_result.success:
        print(f"Connection successful. Found {test_result.sample_count} records")
        print("Sample data:", test_result.sample_data)
    else:
        print(f"Connection failed: {test_result.error}")
    ```

## Troubleshooting
If you encounter any issues with data ingestion, refer to the [Troubleshooting Guide](/troubleshooting/troubleshooting).

## See Also

* [Real-time Sync](/integrations/real-time-sync) - Set up continuous data synchronization

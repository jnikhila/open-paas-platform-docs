# Real-time Data Synchronization

This guide explains how to set up continuous real-time data synchronization between external systems and the Open PaaS Platform. Follow these steps to configure change data capture, define sync rules, and handle real-time events effectively.

---

## Before You Begin

Make sure you have the following:

- Access to Open PaaS Platform with real-time sync permissions
- External system with change data capture (CDC) or webhook capabilities
- Network connectivity between systems (consider firewall rules)
- Python 3.x and the Open PaaS Platform SDK installed
- Understanding of your data schema and sync requirements
- Familiarity with [Create Your First Connector](../getting-started/quick-start.md)

## Create a Real-time Sync Connector

1. Configure Your Data Source: Set up the source system for real-time data capture:

    ```python
    from openpaas_sdk import OpenPaaSClient, RealtimeSync

    # Initialize the platform client
    client = OpenPaaSClient(api_key="your_api_key")

    # Create real-time sync for database changes
    sync_connector = RealtimeSync(
        name="customer_realtime_sync",
        source_type="postgresql_cdc",
        config={
            "host": "db.yourcompany.com",
            "port": 5432,
            "database": "production_db",
            "username": "sync_user",
            "password": "secure_password",
            "tables": ["customers", "orders", "products"],
            "ssl_mode": "require"
        }
    )
    ```

2. Define Sync Rules: Configure what data to sync and how to handle changes:

    ```python
    # Set up change detection rules
    sync_connector.add_sync_rule(
        table="customers",
        operations=["INSERT", "UPDATE", "DELETE"],
        filters={
            "status": "active",
            "updated_at": "> YESTERDAY"
        }
    )

    # Configure field mappings
    sync_connector.add_field_mapping("customers", {
        "customer_id": "id",
        "full_name": "name",
        "email_address": "email",
        "last_modified": "updated_at"
    })

    # Set up conflict resolution
    sync_connector.set_conflict_resolution({
        "strategy": "timestamp_wins",
        "timestamp_field": "updated_at"
    })
    ```

3. Handle Real-time Events: Define how to process incoming change events:

    ```python
    # Handle customer updates
    @sync_connector.on_change("customers")
    def handle_customer_change(event):
        operation = event.operation  # INSERT, UPDATE, DELETE
        old_data = event.old_data
        new_data = event.new_data
        
        if operation == "INSERT":
            print(f"New customer: {new_data['name']}")
            # Trigger welcome workflow
            client.trigger_workflow("customer_welcome", new_data)
        
        elif operation == "UPDATE":
            print(f"Customer updated: {new_data['name']}")
            # Update search index
            client.update_search_index("customers", new_data)
        
        elif operation == "DELETE":
            print(f"Customer deleted: {old_data['name']}")
            # Archive customer data
            client.archive_record("customers", old_data['id'])
        
        return {"status": "processed", "operation": operation}
    ```

4. Test Your Sync Setup: Verify that your real-time sync is working correctly with test data:

    ```python
    # Test the sync connector
    test_result = sync_connector.test_connection()
    if test_result.success:
        print(f"Sync connection successful. Ready to process changes.")
        print(f"Connected tables: {test_result.tables}")
    else:
        print(f"Sync connection failed: {test_result.error}")

    # Simulate a test change event
    test_event = {
        "operation": "INSERT",
        "table": "customers",
        "new_data": {
            "id": "test_123",
            "name": "Test Customer",
            "email": "test@example.com",
            "created_at": "2024-01-01T00:00:00Z"
        }
    }

    # Process test event
    result = sync_connector.process_test_event(test_event)
    print(f"Test event result: {result}")
    ```

## Troubleshooting

If you encounter any issues with real-time sync, refer to the [Troubleshooting Guide](/troubleshooting/troubleshooting).

## See Also

* [Data Ingestion](data-ingestion.md) - Batch data processing
* [Webhook Processing](webhooks.md) - Handle incoming webhooks
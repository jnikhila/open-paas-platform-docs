# Get Started with the Open PaaS Platform

When integrating external data with the Open PaaS Platform, creating an efficient connector is key. This tutorial will guide you through the process of building a connector using the Python SDK, which allows you to seamlessly ingest data from external sources.

---

!!! tip "In this tutorial, you will:"
    - :man_raising_hand: Set up your environment and install the Python SDK.
    - :rocket: Create a basic connector to ingest data from an external source.
    - :globe_with_meridians: Use the Python SDK to interact with the Open PaaS Platform.

## Set Up Your Environment

Before building, ensure your environment is ready:

- You've _Python 3.8_ or higher. Verify your Python version with:  
  ```bash
  python --version
  ```
- A text editor like Visual Studio Code or PyCharm.
- Open PaaS Platform Python SDK installed. If not already, install the SDK with the following command:  
  ```bash
  pip install open-paas-platform-sdk
  ```

## Create Your First Connector

To start interacting with the Open PaaS Platform and ingest data, you need to create a connector. A connector is a component that helps the Open PaaS Platform communicate with external data sources, such as APIs or databases. In this section of the tutorial, you will create a simple connector that ingests data from an external source into the Open PaaS Platform using the Python SDK.

**Understand the Connector**

Before writing the code, let’s first understand what this connector will do:
	* **Authentication**: It will authenticate the request to the Open PaaS Platform using your API key.
	* **Data Ingestion**: It will fetch data from an external source, such as a URL or an API.
	* **Integration**: Finally, it will ingest the fetched data into the Open PaaS Platform, making it available for processing.

Now, that you've understood the basics of connector. Let’s build a simple connector to ingest data from an external source into the Open PaaS Platform. 

1. Open Visual Studio Code (VS Code) and create a new Python file named _connector.py_.
2. Start by importing the Open PaaS PlatformClient class from the SDK. This class allows you to interact with the Open PaaS Platform.
    ```python
    from Open PaaS Platform_sdk import Open PaaS PlatformClient
    ```
3. Next, you’ll initialize the Open PaaS PlatformClient by passing your API key. Replace "your_api_key" with your actual API key. This will authenticate your requests to the Open PaaS Platform.
    ```python
    # Initialize the client with your API key
    client = Open PaaS PlatformClient(api_key="your_api_key")
    ```
4. Now, let’s create the function that will pull data from an external source. In this case, it's `ingest_data`. This function will use the ingest method of the Open PaaS PlatformClient to fetch data from a provided external data source URL.
    ```python
    # Ingest data from an external source
    def ingest_data():
        data = client.ingest("external_data_source_url")
        return data
    ```

5. Now that we’ve gone through each part of the connector, let’s bring it all together. Below is the complete code for the connector:

    ```python
    from Open PaaS Platform_sdk import Open PaaS PlatformClient #(1)

    # Initialize the client with your API key
    client = Open PaaS PlatformClient(api_key="your_api_key") #(2)

    # Ingest data from an external source
    def ingest_data():
        data = client.ingest("external_data_source_url") #(3)
        return data #(4)
    ```

    In this code:

    - **(1)** The Open PaaS Platform_sdk is the library provided by the Open PaaS Platform.
    - **(2)** Open PaaS PlatformClient is the core class within this SDK that enables interaction with the platform’s API. 
        - You use this to manage tasks like authentication and data operations. An instance of the Open PaaS PlatformClient class (here named _client_) is created. 
        - It is initialized with the provided API key (_your_api_key_). 
        - The API key is essential for authentication and grants access to the platform’s services.
    - **(3)** `client.ingest`encapsulates the logic for pulling data from an external source using the Open PaaS PlatformClient instance. It interacts with the platform to fetch data from the specified _external_data_source_url_.
    - **(4)** The data fetched from the platform is returned for further use.

> By completing this section, you’ve created your first connector that integrates an external data source with the Open PaaS Platform. You can now test this connector to verify that the data is ingested successfully.

## Test Your Connector

Now that the connector is ready, you can test it. 

1. Save your connector.py file.
2. Open your terminal. Run the following command to execute the script:
    ```bash
    python connector.py
    ```
3. If everything is working correctly, you will see a message like this in your terminal:
    ```text
     Data ingested into the Open PaaS Platform.
    ```
    This confirms that your connector has successfully ingested the data from the external source into the Open PaaS Platform.

> By completing this section, you’ve tested your first connector that ingests data. You can now experiment with this connector and explore ways to enhance it for more complex data ingestion scenarios.


## Next Steps

:rocket: Congratulations! You've successfully:

1. Installed the Python SDK.
2. Built and tested your first connector.

To explore advanced features, check out the <a href="https://github.com/open-metadata/OpenMetadata" target="_blank"> Advanced SDK Documentation <i class="fa fa-external-link-alt"></i></a> 

Keep experimenting to master the platform and expand your skills!
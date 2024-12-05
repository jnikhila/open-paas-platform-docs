# Integrate Stripe API with Open PaaS Platform

This guide explains how to integrate Stripe’s API with the Open PaaS Platform. Follow these steps to set up payment processing, manage subscriptions, and leverage Stripe’s features effectively.

---

## Before You Begin

Ensure you have the following:

- A <a href="https://stripe.com" target="_blank"> Stripe account <i class="fa fa-external-link-alt"></i></a>
- Publishable and Secret API Keys from the Stripe Dashboard (**Developers > API Keys**).
- Access to Open PaaS Platform with the required API integration permissions.
- Basic understanding of Stripe APIs, webhooks, and authentication concepts.
- Basic familiarity with the Open PaaS Platform. If you’re new, start with the [Open PaaS Platform Tutorial](../../getting-started/quick-start.md).
- Python 3.x and pip installed in your environment.


## Create and Configure a Custom Connector

1. **Create a New Connector in Open PaaS Platform**  
    - Go to **Settings** > **API Integrations**.
    - Select **Create New Connector** and choose **Stripe** from the available options.

2. **Authenticate with Stripe**  
    - Input your Publishable Key and Secret Key from the [Before You Begin](#before-you-begin) section.
    - Test the connection to verify the credentials. You should see a "Connection Successful" message.

3. **Define Connector Properties**  
    - Configure the required endpoints (e.g., `/create-customer`, `/process-payment`) to handle specific Stripe operations.
    - Map input fields to match Stripe’s API schema (e.g., `customer_email`, `payment_method`).

4. **Test Connector Functionality**  
    - Use Stripe’s test keys and [test card numbers](https://stripe.com/docs/testing#international-cards) to simulate API calls.
    - Verify that requests and responses flow as expected between Open PaaS Platform and Stripe.


## Implement Payment Processing

After configuring the connector, use it to execute payment-related operations:

1. **Create a Customer Object** that represents users being charged by using the configured connector:
   ```python
   customer = stripe.Customer.create(
       email='customer@example.com',
       payment_method='pm_card_visa',
       invoice_settings={
           'default_payment_method': 'pm_card_visa',
       },
   )
   ```
2. **Process a Payment** by charging the customer using a Payment Intent. For more information, see Stripe’s official documentation on [Payment Intents](https://stripe.com/docs/api/payment_intents).
    ```python
    charge = stripe.PaymentIntent.create(
        amount=2000,  # Amount in cents (e.g., $20.00)
        currency='usd',
        customer=customer.id,
        description='Charge for services on Open PaaS Platform',
    )
    ```
3. **Handle Recurring Billing** by creatin subscriptions for automated recurring payments:
    ```python hl_lines="5"
    subscription = stripe.Subscription.create(
    customer=customer.id,
        items=[{
            # Replace with your Stripe Price ID
            'price': 'price_12345',  
        }],
    )
    ```
4. **Test Your Implementation** by using Stripe’s [test card numbers](https://stripe.com/docs/testing#international-cards) to ensure payments, subscriptions, and error handling work correctly without affecting real accounts.

## Troubleshooting
* **Invalid API Key Error:** Ensure you are using the correct keys from the Stripe Dashboard.
* **Connection Failed:** Verify network settings and confirm that the Stripe endpoint URLs are correct.
* **Test Mode Transactions Failing:** Check if you are using Stripe’s test card numbers. Real card details won’t work in test mode.
* **Customer Creation Error:** Ensure mandatory fields (e.g., email, payment_method) are included and correctly formatted.
* **Subscription Not Renewing:** Confirm that the price and customer objects are valid and active.

## See also
* [Open PaaS Platform - API References](../../references/reference.md): Explore detailed API specifications for the Open PaaS Platform.
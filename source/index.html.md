---
title: SpePas API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>© 2024 Bitblue Documentation Powered by Bitblue</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the spare-part API
---

# SpePas API Documentation

Welcome to the SpePas API documentation. Read this page to gain a high-level understanding of the API and its key features

## Developer-guide Overview

The SpePas API is built using [**vendure**](https://docs.vendure.io/guides/developer-guide/overview/)
,this doc is tailored to guide developers in integrating the SpePas API with it's mobile app (storefront).

## APIs

Vendure exposes all of its functionality via APIs. Specifically, featuring two GraphQL APIs

[**Shop API**](https://spare-part-server.onrender.com/shop-api)

[**Admin API**](https://spare-part-server.onrender.com/admin-api)

# Key Features

## Communication Architecture

1. **Real-Time Interaction:**
   Real-Time Interaction: The API ensures seamless communication by leveraging the SpePas mobile app and server in real-time. This architecture supports instant updates, guaranteeing a dynamic and responsive spare parts shopping experience for your users

2. **GraphQL for Effortless Integration:**
   Streamline data exchange with GraphQL, simplifying communication between the frontend (storefront) and backend. Utilize GraphQL's flexible query language to request specific data, minimizing unnecessary transfers and optimizing the performance of the mobile app.

## Data Exchange Format

3. **Structured Data with GraphQL:**
   Utilize GraphQL for structured and efficient data exchange. Access information with a single, well-defined endpoint, reducing the complexity of data retrieval for frontend developers.

4. **Rich Product Information:**
   Retrieve detailed spare parts information, including part specifications, vendor details, pricing, and availability. Enhance the user experience by showcasing comprehensive product data within the mobile app.

## Authentication and Authorization

5. **Secure User Authentication:**
   Implement secure user registration and login processes. Allow users to access personalized data, such as saved carts and order history, securely.

6. **Social Logins and OTP Support:**
   Facilitate a seamless onboarding experience by integrating social logins. Enhance security with OTP authentication, providing an additional layer of verification for user accounts.

## Error Handling

7. **Clear and Informative Error Responses:**
   Simplify troubleshooting with clear error responses. The documentation provides detailed messages to help developers quickly identify and resolve issues during integration.

## API Services

**Customer Account Management:**
Integrate features for easy customer account management, including account creation, password management, and secure login methods. Support social logins and OTP for enhanced user authentication.

**Product Management:**
Effortlessly manage product data with support for multiple images and custom fields. Showcase detailed product information within the mobile app for a comprehensive user experience.

**Admin Portal for Store Management:**
Facilitate store management with a dedicated [**admin portal**](https://spare-part-server.onrender.com/admin). Admins can efficiently handle tasks such as inventory management, order processing, and vendor coordination.

**Multi-Vendor Support:**
Enable a multi-vendor ecosystem akin to platforms like Amazon. Vendors can seamlessly manage their inventory, update product details, and process orders through specialized API services.

# Customer Account Management

## Account Creation

To create a new customer account, you can utilize the `createAccount` mutation. Below is an example of how to perform an account creation API call using GraphQL.

### Sample Mutation

Execute the following GraphQL mutation to create a new account:

```graphql
mutation {
  createAccount(
    input: {
      firstName: "Sall"
      lastName: "sample"
      email: "sample@email.com"
      Phone: "022337544"
      password: "pass122"
    }
  ) {
    id
    email
    firstName
    lastName
    createdAt
  }
}
```

### Test Environment

Visit the SpePas Shop API endpoint to perform account creation tests:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

<aside class="notice">
The <code>createAccount</code>  mutation returns the <code>id</code> of the newly created account, along with the provided <code>email</code>, <code>firstName</code>, <code>lastName</code>, and the timestamp of the account's creation <code>createdAt</code>.
</aside>

Learn more from [**Auth**](https://docs.vendure.io/guides/core-concepts/auth/#customer-auth)

### Expected Response

Upon a successful account creation, the API will respond with the newly created account details:

```json
{
  "data": {
    "createAccount": {
      "id": "5",
      "email": "sample@email.com",
      "firstName": "Sall",
      "lastName": "sample",
      "createdAt": "2024-01-27T04:52:09.000Z"
    }
  }
}
```

# User Authentication: Custom Login

To authenticate a user and obtain an authentication token, use the `customLogin` mutation. This mutation requires the user's identifier (email or phone number) and password.

## Sample Mutation

Execute the following GraphQL mutation to perform a custom login:

```graphql
mutation {
  customLogin(input: { identifier: "0536369414", password: "newpassword" }) {
    token
    user {
      id
      firstName
      lastName
      email
    }
  }
}
```

## Usage Notes

- The `customLogin` mutation returns an authentication token (`token`) and user details (`user`) upon successful login.
- Provide the user's identifier (email or phone number) and password in the mutation input.
- The user details include the user's ID (`id`), first name (`firstName`), last name (`lastName`), and email address (`email`).

## Expected Response

Upon successful authentication, the API will respond with the authentication token and user details:

```json
{
  "data": {
    "customLogin": {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjUiLCJpYXQiOjE3MDcwOTU0MjIsImV4cCI6MTcwNzcwMDIyMn0.NRv85gsObfOowpFyqcZlpLMSdrz7Vpitwo-c6T0J-Pw",
      "user": {
        "id": "5",
        "firstName": null,
        "lastName": null,
        "email": "km.graphicz1@gmail.com"
      }
    }
  }
}
```

<aside class="notice">
The user's first name (`firstName`) and last name (`lastName`) may appear as null in this example. Ensure that your user data includes these details for a complete user profile.
</aside>

## Token Usage

Use the obtained authentication token (`token`) in the `Authorization` header of your GraphQL requests to authenticate the user and access protected resources.

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjUiLCJpYXQiOjE3MDcwOTU0MjIsImV4cCI6MTcwNzcwMDIyMn0.NRv85gsObfOowpFyqcZlpLMSdrz7Vpitwo-c6T0J-Pw
```

## Note

Always secure the authentication token and transmit it securely over HTTPS. Regularly rotate tokens and follow best practices to ensure the security of your authentication process.




## Password Recovery

### Generate Password Recovery OTP

To enhance account security, SpePas provides the functionality to generate a one-time password (OTP) for password recovery. Utilize the `generatePasswordRecoveryOtp` mutation to generate a unique OTP for a specified customer's email address.

#### Test Environment

Initiate OTP generation for password recovery tests using the SpePas Shop API endpoint:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

#### Sample Mutation

Execute the following GraphQL mutation to generate an OTP for password recovery:

```graphql
mutation {
  generatePasswordRecoveryOtp(input: { identifier: "sample@email.com" }) {
    success
    message
  }
}
```

<aside class="notice">
The <code>generatePasswordRecoveryOtp</code> mutation returns a <code>success</code> flag indicating whether the OTP was generated successfully, along with a corresponding <code>message</code>.
</aside>

#### Expected Response

Upon successful OTP generation, the API will respond with a success message:

```json
{
  "data": {
    "generatePasswordRecoveryOtp": {
      "success": true,
      "message": "OTP sent successfully"
    }
  }
}
```

### Verify Password Recovery OTP

As part of the password recovery process, SpePas allows users to verify their identity using a one-time password (OTP). Utilize the `verifyPasswordRecoveryOtp` mutation to confirm the authenticity of the OTP associated with a specific customer.

#### Test Environment

Conduct OTP verification for password recovery tests using the SpePas Shop API endpoint:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

#### Sample Mutation

Execute the following GraphQL mutation to verify the OTP for password recovery:

```graphql
mutation {
  verifyPasswordRecoveryOtp(input: { otp: "462452" }) {
    id
    email
  }
}
```

<aside class="notice">
The <code>verifyPasswordRecoveryOtp</code> mutation returns the <code>id</code> and <code>email</code> of the customer upon successful OTP verification.
</aside>

#### Expected Response

Upon successful OTP verification, the API will respond with the customer details:

```json
{
  "data": {
    "verifyPasswordRecoveryOtp": {
      "id": "5",
      "email": "sample@email.com"
    }
  }
}
```

### Resend Password Recovery OTP

In scenarios where the initial OTP for password recovery might be lost or expired, SpePas provides the functionality to resend the OTP. Utilize the `resendPasswordRecoveryOtp` mutation to resend the OTP to the customer's email address.

#### Test Environment

Initiate OTP resend for password recovery tests using the SpePas Shop API endpoint:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

#### Sample Mutation

Execute the following GraphQL mutation to resend the OTP for password recovery:

```graphql
mutation {
  resendPasswordRecoveryOtp(input: { identifier: "sample@email.com" }) {
    success
    message
  }
}
```

<aside class="notice">
The <code>resendPasswordRecoveryOtp</code> mutation returns a <code>success</code> flag indicating whether the OTP was resent successfully, along with a corresponding <code>message</code>.
</aside>

#### Expected Response

Upon successful OTP resend, the API will respond with a success message:

```json
{
  "data": {
    "resendPasswordRecoveryOtp": {
      "success": true,
      "message": "OTP resent successfully"
    }
  }
}
```

## Social Logins

SpePas supports seamless onboarding and login experiences through social logins. Customers can conveniently use their existing social media accounts to create or log in to their SpePas account.

### Supported Social Platforms

1. **Google Login**
2. **Facebook Login**
3. **Twitter Login**

### How to Perform Social Logins

To initiate a social login, follow these steps:

1. Visit the SpePas Shop API endpoint for social logins:
   [**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

2. Choose the social platform you want to use for login.

3. Follow the authentication prompts provided by the selected social platform.

### Sample Social Login Mutation (For Illustration Purposes)

Below is an illustrative example of how a social login mutation might look:

```graphql
mutation {
  socialLogin(platform: "google", accessToken: "your_google_access_token") {
    id
    email
    firstName
    lastName
  }
}
```

### Expected Response

Upon successful social login, the API will respond with the customer details:

```json
{
  "data": {
    "socialLogin": {
      "id": "4",
      "email": "john.doe@example.com",
      "firstName": "John",
      "lastName": "Doe"
    }
  }
}
```

The `socialLogin` mutation returns the `id`, `email`, `firstName`, and `lastName` of the customer upon successful social login.


# Multi-Vendor Support

## Seller Registration

Use the `registerNewSeller` mutation to register a new seller. Provide details such as the shop name, seller's first and last name, email address, and password.

##### Sample Mutation

Execute the following GraphQL mutation to register a new seller:

```graphql
mutation RegisterSeller {
  registerNewSeller(input: {
    shopName: "Test Ent.",
    seller: {
      firstName: "New"
      lastName: "kwamz"
      emailAddress: "new.seller@example.com"
      password: "test",
    }
  }) {
    id
    code
    token
  }
}
```

##### Usage Notes

- The `registerNewSeller` mutation creates a new seller account and associates it with the specified shop.
- The seller can use the provided shop name for branding and identification.
- Vendure's Admin UI can be utilized for sellers to manage their inventory, eliminating the need for a separate seller login mechanism.

##### Expected Response

Upon successful registration, the API will respond with the newly created seller's information, including the ID, shop code, and authentication token.

```json
{
  "data": {
    "registerNewSeller": {
      "id": "5",
      "code": "test-ent.",
      "token": "test-ent.-token"
    }
  }
}
```

## Adding Items to Order

To add items to the order from different sellers, utilize the `addItemToOrder` mutation. This mutation allows customers to specify the product variant ID and quantity for each item they want to purchase.

#### Sample Mutation

Execute the following GraphQL mutation to add items to the order:

```graphql
mutation {
  addItemToOrder(productVariantId: "56", quantity: 1) {
    __typename
    ... on Order {
      id
    }
    ... on ErrorResult {
      errorCode
    }
  }
  add2: addItemToOrder(productVariantId: "58", quantity: 1) {
    __typename
    ... on Order {
      id
    }
    ... on ErrorResult {
      errorCode
    }
  }
}
```

<aside class="notice">
The <code>addItemToOrder</code> mutation includes the <code>__typename</code> field to differentiate between the order type and potential error results. Check the response for the order ID or error code accordingly.
</aside>

#### Expected Response

Upon successfully adding items to the order, the API will respond with the order ID:

```json
{
  "data": {
    "addItemToOrder": {
      "__typename": "Order",
      "id": "4"
    },
    "add2": {
      "__typename": "Order",
      "id": "4"
    }
  }
}
```

In a multi-vendor setup, SpePas allows customers to add items from different sellers to their cart and proceed to checkout. This section covers the process of adding items to the cart and setting up order fulfillment.

## Adding payment to Order

To handle orders in SpePas, utilize the `addPaymentToOrder` mutation. This mutation allows you to associate a payment method with an order.

### Mutation

Execute the following GraphQL mutation to add a payment to an order:

```graphql
mutation {
  addPaymentToOrder(input: { method: "connected-payment-method", metadata: {} }) {
    ... on Order { id }
    ... on ErrorResult {
      errorCode
      message
    }
    ... on PaymentFailedError {
      paymentErrorMessage
    }
  }
}
```

### Usage Notes

- The `addPaymentToOrder` mutation associates the specified payment method with the order.
- Check the response to determine the success or failure of the payment addition.
- The `Order` type includes the `id` field, providing the order ID after a successful payment.
- Errors or payment failures are communicated through the relevant fields in the response.

##### Expected Response

The API will respond based on the outcome of the payment addition:

- **Successful Payment:**

```json
{
  "data": {
    "addPaymentToOrder": {
      "id": "your_order_id"
    }
  }
}
```

- **Error Result:**

```json
{
  "data": {
    "addPaymentToOrder": {
      "errorCode": "your_error_code",
      "message": "error_message"
    }
  }
}
```

- **Payment Failed:**

```json
{
  "data": {
    "addPaymentToOrder": {
      "paymentErrorMessage": "payment_error_message"
    }
  }
}
```

## Set Order Billing Address

To provide a billing address for the order, use the `setOrderBillingAddress` mutation. This mutation allows customers to specify the billing address details, including company, street lines, city, province, postal code, and custom fields.

#### Sample Mutation

Execute the following GraphQL mutation to set the order billing address:

```graphql
mutation {
  setOrderBillingAddress(input: {
    company: null
    streetLine1: "123 james town"
    streetLine2: ""
    city: "accra"
    province: "G.Accra"
    postalCode: "12345"
    countryCode: "GH"
    customFields: { houseNumber: "25" }
  }) {
    ... on Order {
      id
    }
  }
}
```

<aside class="notice">
The <code>setOrderBillingAddress</code> mutation includes the <code>__typename</code> field to differentiate between the order type and potential error results. Check the response for

 the order ID accordingly.
</aside>

#### Expected Response

Upon successfully setting the order billing address, the API will respond with the order ID:

```json
{
  "data": {
    "setOrderBillingAddress": {
      "id": "4"
    }
  }
}
```

## Eligible Shipping Methods

To determine eligible shipping methods for the order, use the `eligibleShippingMethods` query. This query returns a list of available shipping methods, including their IDs, names, and prices with tax.

#### Sample Query

Execute the following GraphQL query to retrieve eligible shipping methods:

```graphql
query Elig {
  eligibleShippingMethods {
    id
    name
    priceWithTax
  }
}
```

#### Expected Response

The API will respond with a list of eligible shipping methods:

```json
{
  "data": {
    "eligibleShippingMethods": [
      {
        "id": "1",
        "name": "Standard Shipping",
        "priceWithTax": 500
      },
      {
        "id": "2",
        "name": "Express Shipping",
        "priceWithTax": 1000
      }
    ]
  }
}
```

## Assign Shipping Method to Order

To assign shipping methods to the order, use the `setOrderShippingMethod` mutation. This mutation allows customers to specify the shipping method IDs for their order.

#### Sample Mutation

Execute the following GraphQL mutation to assign shipping methods to the order:

```graphql
mutation AssignShipping {
  setOrderShippingMethod(shippingMethodId: ["1", "2"]) {
    ... on Order {
      id
    }
  }
}
```

<aside class="notice">
The <code>setOrderShippingMethod</code> mutation includes the <code>__typename</code> field to differentiate between the order type and potential error results. Check the response for the order ID accordingly.
</aside>

#### Expected Response

Upon successfully assigning shipping methods to the order, the API will respond with the order ID:

```json
{
  "data": {
    "setOrderShippingMethod": {
      "id": "4"
    }
  }
}
```

# Stay Tuned for More!

We are continually expanding our platform's features and functionality. Stay tuned for updates, as they will be announced here. We value your feedback and are here to assist you. If you have any questions or need further assistance, please don't hesitate to reach out.


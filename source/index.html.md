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

## changePassword

To update a customer's password on the SpePas platform, use the `changePassword` mutation. Here's an example of how to perform a password change API call using GraphQL.

### Test Environment

Perform password change tests using the SpePas Shop API endpoint:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

### Sample Mutation

Execute the following GraphQL mutation to change a customer's password:

```graphql
mutation {
  changePassword(
    customerId: "4"
    oldPassword: "pass122"
    newPassword: "secure"
  ) {
    id
    email
    lastName
    firstName
  }
}
```

<aside class="notice">
The <code>changePassword</code>  mutation returns the <code>id</code> of the newly created account, along with the provided <code>email</code>, <code>firstName</code>, <code>lastName</code>, and after the password change.
</aside>

### Expected Response

Upon a successful password change, the API will respond with the updated customer details:

```json
{
  "data": {
    "changePassword": {
      "id": "4",
      "email": "salome@email.com",
      "lastName": "MIntah",
      "firstName": "Sall"
    }
  }
}
```

## Generate OTP

To enhance account security, SpePas provides the functionality to generate a one-time password (OTP) for customer accounts. Utilize the `generateOTP` mutation to generate a unique OTP for a specified customer ID.

### Test Environment

Initiate OTP generation tests using the SpePas Shop API endpoint:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

### Sample Mutation

Execute the following GraphQL mutation to generate an OTP for a specific customer:

```graphql
mutation {
  generateOTP(customerId: "4")
}
```

<aside class="notice">
The <code>generateOTP</code> mutation returns the generated OTP as a string. This OTP can be used for additional authentication or verification steps.
</aside>

### Expected Response

Upon successful OTP generation, the API will respond with the generated OTP:

```json
{
  "data": {
    "generateOTP": "443569"
  }
}
```

## verifyOTP

As an additional layer of security, SpePas provides the ability to verify a customer's identity using a one-time password (OTP). Utilize the `verifyOTP` mutation to confirm the authenticity of the OTP associated with a specific customer.

### Test Environment

Conduct OTP verification tests using the SpePas Shop API endpoint:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

### Sample Mutation

Execute the following GraphQL mutation to verify the OTP for a specific customer:

```graphql
mutation {
  verifyOTP(customerId: "4", otp: "971020") {
    id
    email
    firstName
    lastName
  }
}
```

<aside class="notice">
The <code>verifyOTP</code> mutation returns the `id`, `email`, `firstName`, and `lastName` of the customer upon successful OTP verification.
</aside>

### Expected Response

Upon successful OTP verification, the API will respond with the customer details:

```json
{
  "data": {
    "verifyOTP": {
      "id": "4",
      "email": "salome@email.com",
      "firstName": "Sall",
      "lastName": "MIntah"
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

## Registering a New Seller

In SpePas, multi-vendor support allows sellers to register their shops and manage their inventory through the admin portal. Follow the steps below to register a new seller.

### Mutation

Use the `RegisterSeller` mutation to register a new seller. Provide details such as the shop name, seller's first and last name, email address, and password.

```graphql
mutation RegisterSeller {
  registerNewSeller(
    input: {
      shopName: "new Sam' on Render SP"
      seller: {
        firstName: "san"
        lastName: "Kay"
        emailAddress: "test.seller@example.com"
        password: "test"
      }
    }
  ) {
    id
    createdAt
    seller {
      name
    }
  }
}
```

### Usage Notes

- The `registerNewSeller` mutation creates a new seller account and associates it with the specified shop.
- The seller can use the provided shop name for branding and identification.
- Vendure's Admin UI can be utilized for sellers to manage their inventory, eliminating the need for a separate seller login mechanism.

This process enables sellers to seamlessly register and begin managing their shops through the [**admin portal.**](https://spare-part-server.onrender.com/shop-api)

### Expected Response

Upon successful registration, the API will respond with the newly created seller's information, including the ID, creation timestamp, and the shop name.

```json
{
  "data": {
    "registerNewSeller": {
      "id": "3",
      "createdAt": "2024-01-28T02:09:29.000Z",
      "seller": {
        "name": "new Sam' on Render SP"
      }
    }
  }
}
```

# Payment Management

## Add Payment to Order

To handle payments for orders in SpePas, utilize the `addPaymentToOrder` mutation. This mutation allows you to associate a payment method with an order.

### Mutation

Execute the following GraphQL mutation to add a payment to an order:

```graphql

mutation {
  addPaymentToOrder(
    input: { method: "connected-payment-method", metadata: {} }
  ) {
    ... on Order {
      id
    }
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

This mutation is crucial for managing the financial aspects of orders within the SpePas e-commerce platform.

> **Successful Payment:**

```json
{
  "data": {
    "addPaymentToOrder": {
      "id": "your_order_id"
    }
  }
}
```

> **Error Result:**

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

> **Payment Failed:**

```json
{
  "data": {
    "addPaymentToOrder": {
      "paymentErrorMessage": "payment_error_message"
    }
  }
}
```

### Expected Response

The API will respond based on the outcome of the payment addition:

# Stay Tuned for More!

We are constantly working to add more features and functionality to our platform. Please keep an eye out for
updates, as they will be announced here. We value your feedback and would love to hear from you. Feel free to reach out if you have any questions or need assistance.

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

## Overview

The SpePas API is built using [**vendure**](https://docs.vendure.io/guides/developer-guide/overview/)
, a headless e-commerce platform specifically tailored to guide developers in seamlessly integrating the SpePas API with the storefront mobile app. SpePas, your dedicated e-commerce platform for spare parts, presents a host of features curated to elevate the spare parts shopping experience.

## APIs

Vendure exposes all of its functionality via APIs. Specifically,featuring two GraphQL APIs

 [**Shop API**](https://spare-part-server.onrender.com/shop-api)

 [**Admin API**](https://spare-part-server.onrender.com/admin-api)


# Key Features

## Communication Architecture

1. **Real-Time Interaction:**
   Ensure seamless communication by leveraging the SpePas mobile app and server in real-time. This architecture supports instant updates, guaranteeing a dynamic and responsive spare parts shopping experience for your users.

2. **GraphQL for Effortless Integration:**
   Streamline data exchange with GraphQL, simplifying the communication between the frontend and backend. Use GraphQL's flexible query language to request specific data, minimizing unnecessary transfers and optimizing mobile app performance.

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
      email: "sample@email.com"
      password: "pass122"
      firstName: "Sall"
      lastName: "sample"
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

### Expected Response

Upon a successful account creation, the API will respond with the newly created account details:


```json
{
  "data": {
    "createAccount": {
      "id": "5",
      "email": "new@email.com",
       "firstName": "Sall",
      "lastName": "sample",
      "createdAt": "2024-01-27T04:52:09.000Z"
    }
  }
}
```


## Changing password

To reset a customer's password, you can utilize the `changePassword` mutation. Below is an example of how to perform Changing password API call using GraphQL.

### Sample Mutation

Execute the following GraphQL mutation to change a password:

```graphql

mutation {
  changePassword(
    customerId: "4", 
    oldPassword: "pass122",
    newPassword: "secure"
  ){
    id
    email
    lastName
    firstName
  }
}
```

### Test Environment

Visit the SpePas Shop API endpoint to perform account creation tests:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

<aside class="notice">
The <code>createAccount</code>  mutation returns the <code>id</code> of the newly created account, along with the provided <code>email</code>, <code>firstName</code>, <code>lastName</code>, and the timestamp of the account's creation (`createdAt`).
</aside>

### Expected Response

Upon a successful account creation, the API will respond with the newly created account details:

```json
{
  "data": {
    "createAccount": {
      "id": "5",
      "email": "new@email.com",
       "firstName": "Sall",
      "lastName": "sample",
      "createdAt": "2024-01-27T04:52:09.000Z"
    }
  }
}
```


## Generating OTP

To Generate an OTP, you can utilize the `generateOTP` mutation. Below is an example of how to Generate OTP  API call using GraphQL.

### Sample Mutation

Execute the following GraphQL mutation to Generate OTP:

```graphql

mutation {
  generateOTP(customerId: "4")
}

```

### Test Environment

Visit the SpePas Shop API endpoint to perform account creation tests:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

<aside class="notice">
The <code>createAccount</code>  mutation returns the <code>id</code> of the newly created account, along with the provided <code>email</code>, <code>firstName</code>, <code>lastName</code>, and the timestamp of the account's creation (`createdAt`).
</aside>

### Expected Response

Upon a successful account creation, the API will respond with the newly created account details:

```json
{
  "data": {
    "createAccount": {
      "id": "5",
      "email": "new@email.com",
       "firstName": "Sall",
      "lastName": "sample",
      "createdAt": "2024-01-27T04:52:09.000Z"
    }
  }
}
```



## Verify OTP

To Verify an OTP, you can utilize the `verifyOTP` mutation. Below is an example of how to Generate OTP  API call using GraphQL.

### Sample Mutation

Execute the following GraphQL mutation to Generate OTP:

```graphql

mutation {
  verifyOTP(
    customerId: "4",
    otp:  "971020"
  ){
    id
    email
    firstName
    lastName
  }
}
```

### Test Environment

Visit the SpePas Shop API endpoint to perform account creation tests:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

<aside class="notice">
The <code>createAccount</code>  mutation returns the <code>id</code> of the newly created account, along with the provided <code>email</code>, <code>firstName</code>, <code>lastName</code>, and the timestamp of the account's creation (`createdAt`).
</aside>

### Expected Response

Upon a successful account creation, the API will respond with the newly created account details:

```json
{
  "data": {
    "createAccount": {
      "id": "5",
      "email": "new@email.com",
       "firstName": "Sall",
      "lastName": "sample",
      "createdAt": "2024-01-27T04:52:09.000Z"
    }
  }
}
```

## Social login

To authenticate user using social logins like facebook and Gmail, you can utilize the `verifyOTP` mutation. Below is an example of how to Generate OTP  API call using GraphQL.

### Sample Mutation

Execute the following GraphQL mutation to Generate OTP:

```graphql

mutation {
  verifyOTP(
    customerId: "4",
    otp:  "971020"
  ){
    id
    email
    firstName
    lastName
  }
}
```

### Test Environment

Visit the SpePas Shop API endpoint to perform account creation tests:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

<aside class="notice">
The <code>createAccount</code>  mutation returns the <code>id</code> of the newly created account, along with the provided <code>email</code>, <code>firstName</code>, <code>lastName</code>, and the timestamp of the account's creation (`createdAt`).
</aside>

### Expected Response

Upon a successful account creation, the API will respond with the newly created account details:

```json
{
  "data": {
    "createAccount": {
      "id": "5",
      "email": "new@email.com",
       "firstName": "Sall",
      "lastName": "sample",
      "createdAt": "2024-01-27T04:52:09.000Z"
    }
  }
}
```


# Multi-Vendor Support

## Register Seller

To Register a new Seller, you can utilize the `RegisterSeller` mutation. Below is an example of how to register a new Seller using GraphQL.

### Sample Mutation

Execute the following GraphQL mutation to RegisterSeller:

```graphql

mutation RegisterSeller {
  registerNewSeller(input: {
    shopName: "Sam's on Render SP",
    seller: {
      firstName: "Kay"
      lastName: "Mintah"
      emailAddress: "kay.seller@example.com"
      password: "test",
    }
  }) {
    id
    code
    token
  }
}
```

### Test Environment

Visit the SpePas Shop API endpoint to  Register Seller:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

<aside class="notice">
The <code>createAccount</code>  mutation returns the <code>id</code> of the newly created account, along with the provided <code>email</code>, <code>firstName</code>, <code>lastName</code>, and the timestamp of the account's creation (`createdAt`).
</aside>

### Expected Response

Upon a successful account creation, the API will respond with the newly created account details:

```json
{
  "data": {
    "createAccount": {
      "id": "5",
      "email": "new@email.com",
       "firstName": "Sall",
      "lastName": "sample",
      "createdAt": "2024-01-27T04:52:09.000Z"
    }
  }
}
```

## Add Payment To Order

To Register a new Seller, you can utilize the `addPaymentToOrder` mutation. Below is an example of how to register a new Seller using GraphQL.

### Sample Mutation

Execute the following GraphQL mutation to addPaymentToOrder:

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

### Test Environment

Visit the SpePas Shop API endpoint to  Register Seller:

[**Shop API Test Endpoint**](https://spare-part-server.onrender.com/shop-api)

<aside class="notice">
The <code>createAccount</code>  mutation returns the <code>id</code> of the newly created account, along with the provided <code>email</code>, <code>firstName</code>, <code>lastName</code>, and the timestamp of the account's creation (`createdAt`).
</aside>

### Expected Response

Upon a successful account creation, the API will respond with the newly created account details:

```json
{
  "data": {
    "createAccount": {
      "id": "5",
      "email": "new@email.com",
       "firstName": "Sall",
      "lastName": "sample",
      "createdAt": "2024-01-27T04:52:09.000Z"
    }
  }
}
```

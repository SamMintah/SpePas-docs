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

# User Account Creation

To create a user account, initiate the account creation process using the `initiateAccountCreation` mutation. This mutation requires the user's phone number and desired password.

## Sample Mutation

Execute the following GraphQL mutation to initiate the account creation process:

```graphql
mutation {
  initiateAccountCreation(phone: "055308582", password: "securePassword") {
    success
    message
  }
}
```

## Usage Notes

- The `initiateAccountCreation` mutation initiates the account creation process by sending an OTP (One-Time Password) to the provided phone number.
- Provide the user's phone number and desired password in the mutation input.

## Expected Response

Upon successful initiation of the account creation process, the API will respond with a success message:

```json
{
  "data": {
    "initiateAccountCreation": {
      "success": true,
      "message": "OTP sent successfully"
    }
  }
}
```

## OTP Verification

After initiating the account creation process, a one-time password (OTP) will be sent to the user's phone number. The user needs to verify this OTP to complete the account creation process.

### Sample Mutation

Execute the following GraphQL mutation to verify the OTP for account creation:

```graphql
mutation {
  verifyOtp(otp: "462452") {
    token
  }
}

```

### Expected Response

Upon successful OTP verification, the API will respond with an authentication token:

```json
{
  "data": {
    "verifyOtp": {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjIyIiwiaWF0IjoxNzA4MDEwMDA1LCJleHAiOjE3MDgwMTM2MDV9.m8fI_of_lg7wFj6zv59eaRqEsJqfF2oNOdkRLW6lKAs"
    }
  }
}
```

## Token Usage

Use the obtained authentication token (`token`) in the `Authorization` header of your GraphQL requests to authenticate the user and access protected resources.

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjIyIiwiaWF0IjoxNzA4MDEwMDA1LCJleHAiOjE3MDgwMTM2MDV9.m8fI_of_lg7wFj6zv59eaRqEsJqfF2oNOdkRLW6lKAs
```

## Complete Account Creation

After verifying the OTP for account creation, complete the account creation process by providing additional user details using the `completeAccountCreation` mutation. This mutation requires the user's ID, full name, city, street address, and GPS coordinates.

## Sample Mutation

Execute the following GraphQL mutation to complete the account creation process:

```graphql
mutation {
  completeAccountCreation(
    fullName: "John Doe",
    city: "New York",
    street: "123 Street",
    gps: "40.7128° N, 74.0060° W",
  ) {
    token
  }
}
```

## Usage Notes

- The `completeAccountCreation` mutation finalizes the account creation process by providing additional user details.
- Provide the full name (`fullName`), city, street address, and GPS coordinates in the mutation input.

## Expected Response

Upon successful completion of the account creation process, the API will respond with an authentication token:

```json
{
  "data": {
    "completeAccountCreation": {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjIyIiwiaWF0IjoxNzA4MDEwMDA1LCJleHAiOjE3MDgwMTM2MDV9.m8fI_of_lg7wFj6zv59eaRqEsJqfF2oNOdkRLW6lKAs"
    }
  }
}
```

## Token Usage

Use the obtained authentication token (`token`) in the `Authorization` header of your GraphQL requests to authenticate the user and access protected resources.

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjIyIiwiaWF0IjoxNzA4MDEwMDA1LCJleHAiOjE3MDgwMTM2MDV9.m8fI_of_lg7wFj6zv59eaRqEsJqfF2oNOdkRLW6lKAs
```

Ensure the secure usage and transmission of the authentication token over HTTPS.

## Change Password

To change a user's password, utilize the `changePassword` mutation. This mutation requires the user's ID, old password, and the new desired password.

### Sample Mutation

Execute the following GraphQL mutation to change a user's password:

```graphql
mutation {
  changePassword(
    userId: "21",
    oldPassword: "securePassword",
    newPassword: "newww"
  ) {
    id
    phone
    fullName
    city
  }
}
```

### Usage Notes

- The `changePassword` mutation updates the password for the user associated with the provided user ID.
- Provide the user's ID, old password, and the new desired password in the mutation input.

### Expected Response

Upon successful password change, the API will respond with the user's ID, phone number, full name, and city:

```json
{
  "data": {
    "changePassword": {
      "id": "21",
      "phone": "055301582",
      "fullName": "John Doe",
      "city": "New York"
    }
  }
}
```

## Reset User Password

To reset a user's password, utilize the `resetUserPassword` mutation. This mutation requires the user's ID and the new desired password.

### Sample Mutation

Execute the following GraphQL mutation to reset a user's password:

```graphql
mutation {
  resetUserPassword(input: { userId: "21", newPassword: "new_password" }) {
    id
    fullName
    city
    street
    gps
  }
}
```

### Usage Notes

- The `resetUserPassword` mutation resets the password for the user associated with the provided user ID.
- Provide the user's ID and the new desired password in the mutation input.

### Expected Response

Upon successful password reset, the API will respond with the user's ID and other relevant details:

```json
{
  "data": {
    "resetUserPassword": {
      "id": "21",
      "fullName": "John Doe",
      "city": "New York",
      "street": "123 Street",
      "gps": "40.7128° N, 74.0060° W"
    }
  }
}
```

## Initiate Password Reset

To initiate a password reset for a user, utilize the `initiatePasswordReset` mutation. This mutation requires the user's identifier (phone number or email).

### Sample Mutation

Execute the following GraphQL mutation to initiate a password reset:

```graphql
mutation {
  initiatePasswordReset(input: { identifier: "055301582" }) {
    success
    message
  }
}
```

## Usage Notes

- The `initiatePasswordReset` mutation initiates the password reset process for the user associated with the provided identifier (phone number or email).
- Provide the user's identifier in the mutation input.

## Expected Response

Upon successful initiation of the password reset process, the API will respond with a success flag and a corresponding message indicating that the OTP (One-Time Password) was sent successfully:

```json
{
  "data": {
    "initiatePasswordReset": {
      "success": true,
      "message": "OTP sent successfully"
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
  customLogin(identifier: "055308582", password: "securePassword") {
    token
    user {
      id
      email
      fullName
      city
      gps
    }
  }
}
```

## Usage Notes

- The `customLogin` mutation returns an authentication token (`token`) and user details (`user`) upon successful login.
- Provide the user's identifier (email or phone number) and password in the mutation input.
- The user details include the user's ID (`id`), email address (`email`), full name (`fullName`), city, and GPS coordinates (`gps`).

## Expected Response

Upon successful authentication, the API will respond with the authentication token and user details:

```json
{
  "data": {
    "customLogin": {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjIyIiwiaWF0IjoxNzA4MDEyNjIzLCJleHAiOjE3MDg2MTc0MjN9.f5t7Wl3dVWcIILl0v3uCDwwl0eqF_Uoo7MI33lSOIwI",
      "user": {
        "id": "22",
        "email": null,
        "fullName": "John Doe",
        "city": "New York",
        "gps": "40.7128° N, 74.0060° W"
      }
    }
  }
}
```

<aside class="notice">
The user's email address (`email`) may appear as null in this example. Ensure that your user data includes this detail for a complete user profile.
</aside>

## Token Usage

Use the obtained authentication token (`token`) in the `Authorization` header of your GraphQL requests to authenticate the user and access protected resources.

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjIyIiwiaWF0IjoxNzA4MDEyNjIzLCJleHAiOjE3MDg2MTc0MjN9.f5t7Wl3dVWcIILl0v3uCDwwl0eqF_Uoo7MI33lSOIwI
```

Ensure the secure usage and transmission of the authentication token over HTTPS.

# Multi-Vendor Support

## Seller Registration

Use the `registerNewSeller` mutation to register a new seller. Provide details such as the shop name, seller's first and last name, email address, and password.

## Sample Mutation

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

## Usage Notes

- The `registerNewSeller` mutation creates a new seller account and associates it with the specified shop.
- The seller can use the provided shop name for branding and identification.
- Vendure's Admin UI can be utilized for sellers to manage their inventory, eliminating the need for a separate seller login mechanism.

>
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
## Expected Response

Upon successful registration, the API will respond with the newly created seller's information, including the ID, shop code, and authentication token.



## Adding Items to Order

To add items to the order from different sellers, utilize the `addItemToOrder` mutation. This mutation allows customers to specify the product variant ID and quantity for each item they want to purchase.

## Sample Mutation

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

## Expected Response

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

## Sample Mutation

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

## Expected Response

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

# Products

## Retrieve Product Variants with Pagination

Use this query to fetch a subset of product variants with pagination.

### Query:

```graphql
query {
  products(options: { skip: 5, take: 10 }) {
    totalItems
    items {
      variantList {
        items {
          productId
          name
          price
          priceWithTax
          currencyCode
          stockLevel
          createdAt
        }
      }
    }
  }
}
```
---
## Description:
- **totalItems:** Total number of product variants available.
- **items:** List of products with their respective variant details.
  - **variantList:** List of variants for each product.
    - **items:** Individual variant details including ID, name, price, price with tax, currency code, stock level, and creation date.

This query allows you to paginate through product variants, skipping the specified number of items and taking the desired number of items per page. Adjust the `skip` and `take` parameters as needed for pagination.


### Response:

```json
{
  "data": {
    "products": {
      "totalItems": 58,
      "items": [
        {
          "variantList": {
            "items": [
              {
                "productId": "6",
                "name": "High Performance RAM 4GB",
                "price": 13785,
                "priceWithTax": 16542,
                "currencyCode": "USD",
                "stockLevel": "IN_STOCK",
                "createdAt": "2024-01-24T14:54:12.000Z"
              },
               {
                "productId": "7",
                "name": "High Performance RAM 4GB",
                "price": 13785,
                "priceWithTax": 16542,
                "currencyCode": "USD",
                "stockLevel": "IN_STOCK",
                "createdAt": "2024-01-24T14:54:12.000Z"
              },
            ]
          }
        },
      ]
    }
  }
}
```


## Search Products and Sort

You can use this query to search for products based on a search term and sort the results using various criteria such as top-selling, recommended, recently added, price low to high, or price high to low.

### Query:

```graphql
{
  search(input: {
    term: "your_search_term",
    sort: {
      TOP_SELLING: DESC
    }
  }) {
    totalItems
    items {
      productId
      productName
    }
  }
}
```

### Parameters:

- **input:** Specifies the search term and sorting criteria.
  - **term:** The search term you want to use to filter products.
  - **sort:** Specifies the sorting criteria. You can choose from the following options:
    - **TOP_SELLING:** Sort by top-selling items.
    - **RECOMMENDED:** Sort by recommended items.
    - **RECENTLY_ADDED:** Sort by recently added items.
    - **PRICE_LOW_TO_HIGH:** Sort by price from low to high.
    - **PRICE_HIGH_TO_LOW:** Sort by price from high to low.

### Response:

```json
{
  "data": {
    "search": {
      "totalItems": 10,
      "items": [
        {
          "productId": "1",
          "productName": "Product 1"
        },
      ]
    }
  }
}
```

### Description:

- **totalItems:** Total number of products matching the search term.
- **items:** List of products matching the search term, sorted according to the specified criteria.
  - **productId:** The unique identifier of the product.
  - **productName:** The name of the product.

You can adjust the `term` parameter to your desired search term and choose the appropriate sorting option based on your requirements.


<aside class="notice">
  Please note that the sort functionality is currently under development and may not be fully functional. We are working to resolve this issue as soon as possible.
</aside>


# Stay Tuned for More!

We are continually expanding our platform's features and functionality. Stay tuned for updates, as they will be announced here. We value your feedback and are here to assist you. If you have any questions or need further assistance, please don't hesitate to reach out.


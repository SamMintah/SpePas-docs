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

[**Shop API**](https://spepas-api.onrender.com/shop-api)

[**Admin API**](https://spepas-api.onrender.com/admin-api/)

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
mutation getStarted {
  initiateAccountCreation(
    input: { phone: "0201234567890", password: "tryPass" }
  ) {
    success
    message
  }
}
```

![initiate-account](images/signup.png)

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

```graphql
mutation {
  verifyOtp(input: { otp: "567633" }) {
    token
  }
}
```

![verify-otp](images/verifyOtp.png)

### Sample Mutation

Execute the following GraphQL mutation to verify the OTP for account creation:

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

## completeAccountCreation

complete the account creation process by uploading profile picture using the `completeAccountCreation` mutation. This mutation requires the Bearer token , file.

## Token Usage

```json
{
  "Authorization": "Bearer <token>"
}
```

Use the obtained authentication token (`token`) in the `Authorization` header of your GraphQL requests to authenticate the user and access protected resources.

## Create Customer Account

```graphql
mutation createCustomerAccount($file: Upload!) {
  createAccount(
    input: {
      role: CUSTOMER
      customer: {
        fullName: "test 3"
        city: "Accra"
        street: "STR-20"
        gps: "GH-20-ASH"
        profilePicture: $file
      }
    }
  ) {
    success
    message
    token
  }
}
```

Execute the following GraphQL mutation to complete the account creation process:

![Complete Customer Account](images/completecustomer.png)

## Usage Notes

- The `createAccount` mutation is used to finalize the account creation process by providing comprehensive user details.
- The `role` parameter should be set to `CUSTOMER` to specify the type of account being created.
- Ensure to include the following information in the mutation input:
  - **Full Name (`fullName`)**: The complete name of the customer.
  - **City**: The city where the customer resides.
  - **Street Address (`street`)**: The street address of the customer's residence.
  - **GPS Coordinates (`gps`)**: The GPS coordinates for the customer's location.
  - **Profile Picture (`profilePicture`)**: The profile picture file for the customer, uploaded using the `$file` variable.
- The response will contain:
  - **Success (`success`)**: A boolean indicating whether the account creation was successful.
  - **Message (`message`)**: A message providing additional information about the account creation process.
  - **Token (`token`)**: An authentication token for the newly created customer account.

## Expected Response

Upon successful authentication, the API will respond with the authentication token and user details:

```json
{
  "data": {
    "completeAccountCreation": {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjIyIiwiaWF0IjoxNzA4MDEyNjIzLCJleHAiOjE3MDg2MTc0MjN9.f5t7Wl3dVWcIILl0v3uCDwwl0eqFSOIwI",
      "user": {
        "id": "22"
      }
    }
  }
}
```

## Rider Registration

Use the `createAccount` mutation to request a new rider account. Provide details such as the rider's full name, phone number, vehicle type, and other relevant information.

## Sample Mutation

Execute the following GraphQL mutation to register a new rider:

```graphql
mutation createRiderAccount(
  $vehicleRegistrationFile: Upload!
  $profilePicture: Upload
  $nationalIdCard: Upload!
) {
  createAccount(
    input: {
      role: RIDER
      rider: {
        fullName: "Sam-MIntah"
        phone: "0536369414"
        vehicleRegistrationFile: $vehicleRegistrationFile
        profilePicture: $profilePicture
        vehicleType: "two wheel"
        nationalIdCard: $nationalIdCard
      }
    }
  ) {
    success
    message
  }
}
```

![Create New Rider](images/rider1.png) ![Create New Rider](images/rider.png)

### Usage Notes

- The `createAccount` mutation is used to submit a new rider account for review.
- The `role` parameter should be set to `RIDER` to specify the type of account being created.
- Ensure to include the following information in the mutation input:

  - **Full Name (`fullName`)**: The rider's full name.
  - **Phone Number (`phone`)**: The rider's phone number.
  - **Vehicle Registration File (`vehicleRegistrationFile`)**: A file containing the vehicle registration details, uploaded using the `$vehicleRegistrationFile` variable.
  - **Profile Picture (`profilePicture`)**: A profile picture for the rider, uploaded using the `$profilePicture` variable.
  - **Vehicle Type (`vehicleType`)**: The type of vehicle (e.g., "two wheel").
  - **National ID Card (`nationalIdCard`)**: A file containing the rider's national ID card, uploaded using the `$nationalIdCard` variable.

- Fields such as `vehicleRegistrationFile`, `profilePicture`, and `nationalIdCard` are mandatory and must be provided for successful registration:

## Expected Response

```json
{
  "data": {
    "createaccont": {
      "success": true,
      "message": "submitted successfully"
    }
  }
}
```

- It is important to provide valid and accurate information. Invalid data will be disregarded.
- Upon successful review of the provided information, the rider will receive a message with temporary credentials to log in and access their rider account with all necessary permissions.

## Seller Registration

Use the `createAccount` mutation to request a new seller. Provide details such as the shop name, seller's first and last name, email address, and password.

## Sample Mutation

Execute the following GraphQL mutation to register a new seller:

```graphql
mutation createSellerAccount(
  $businessRegistrationFile: Upload!
  $profilePicture: Upload!
) {
  createAccount(
    input: {
      role: SELLER
      seller: {
        shopName: "Shop_ent"
        seller: {
          fullName: "sam Jan"
          emailAddress: "owner@email.com"
          phone: "0536369414"
          businessRegistrationFile: $businessRegistrationFile
          TIN: "5241254"
          profilePicture: $profilePicture
          shopAddress: "No.10 potato strt"
          aboutShop: "about my shop"
        }
      }
    }
  ) {
    success
    message
  }
}
```

![CreateNewSeller](images/submitstore.png) ![CreateNewSeller](images/bottom-storedetails.png)

### Usage Notes

- The `createAccount` mutation is used to submit a new seller account for review.
- The `role` parameter should be set to `SELLER` to specify the type of account being created.
- Ensure to include the following information in the mutation input:
  - **Shop Name (`shopName`)**: The name of the shop.
  - **Full Name (`fullName`)**: The seller's full name.
  - **Email Address (`emailAddress`)**: The seller's email address.
  - **Phone Number (`phone`)**: The seller's phone number.
  - **Business Registration File (`businessRegistrationFile`)**: A file containing the business registration details, uploaded using the `$businessRegistrationFile` variable.
  - **Tax Identification Number (`TIN`)**: The seller's Tax Identification Number.
  - **Profile Picture (`profilePicture`)**: A profile picture for the seller, uploaded using the `$profilePicture` variable.
  - **Shop Address (`shopAddress`)**: The address of the shop.
  - **About Shop (`aboutShop`)**: A brief description of the shop.

## Expected Response

```json
{
  "data": {
    "createaccont": {
      "success": true,
      "message": "submitted successfully"
    }
  }
}
```

Upon successful submission, the API will respond with a success message.

# User Authentication: Login

To authenticate a user and obtain an authentication token, use the `customLogin` mutation. This mutation requires the user's identifier (email or phone number) and password.

## Sample Mutation

Execute the following GraphQL mutation to perform a custom login:

```graphql
mutation customLogin {
  customLogin(input: { identifier: "0501234589", password: "newpas1234" }) {
    token
    user {
      id
      phone
      fullName
      avatar {
        preview
      }
      roles
    }
  }
}
```

![login-customer](images/login.png)

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
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjUiLCJpYXQiOjE3MTc0NTM5MTYsImV4cCI6MTcxNzU0MDMxNn0.jW4chMlJw5HNPPPzGVuziXGZOCbguhUgLT-9t2LWYTQ",
      "user": {
        "id": "5",
        "phone": "052255483",
        "fullName": "John",
        "avatar": {
          "preview": "http://localhost:3000/assets/preview/d4/image_picker_8a1fe57e-8abe-4c50-9027-ba0789f9093a-78441-0000006ac34e2af6__preview.jpg"
        },
        "roles": ["CUSTOMER"]
      }
    }
  }
}
```

## Upload Profile Picture

After verifying the OTP for account creation, complete the account creation process by providing additional user details using the `completeAccountCreation` mutation. This mutation requires the Bearer token , full name, city, street address, and GPS coordinates.

## Token Usage

```json
{
  "Authorization": "Bearer <token>"
}
```

Use the obtained authentication token (`token`) in the `Authorization` header of your GraphQL requests to authenticate the user and access protected resources.

## Sample Mutation

```graphql
mutation UploadProfilePicture($file: Upload!) {
  uploadProfilePicture(file: $file) {
    preview
  }
}
```

Execute the following GraphQL mutation to complete the account creation process:

## Expected Response

Upon successful upload of the picture, the API will respond with image-url:

```json
{
  "data": {
    "preview": "http://localhost:3000/assets/preview/d4/image_picker_8a1fe57e-8abe-4c50-9027-ba0789f9093a-78441-0000006ac34e2af6__preview.jpg"
  }
}
```

## Usage Notes

complete the account creation process by uploading profile picture using the `UploadProfilePicture` mutation. This mutation requires the Bearer token , file.

## Change Password

To change a user's password, utilize the `changePassword` mutation. This mutation requires the Token, old password, and the new desired password.

## Token Usage

```json
{
  "Authorization": "Bearer <token>"
}
```

Use the obtained authentication token (`token`) in the `Authorization` header of your GraphQL requests to authenticate the user and access protected resources.

## Sample Mutation

```graphql
mutation {
  changePassword(oldPassword: "securePassword", newPassword: "securePass") {
    id
    phone
    fullName
    city
  }
}
```

Execute the following GraphQL mutation to change a user's password:

![change-password](images/changePassword.png)

### Usage Notes

- The `changePassword` mutation updates the password for the user associated with the provided
  token, old password, and the new desired password in the mutation input

## Expected Response

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

Upon successful password change, the API will respond with the user's ID, phone number, full name, and city:

## Change Contact

To change a user's password, utilize the `changeContact` mutation. This mutation requires the Token, current phone, and the new contact.

## Token Usage

```json
{
  "Authorization": "Bearer <token>"
}
```

Use the obtained authentication token (`token`) in the `Authorization` header of your GraphQL requests to authenticate the user and access protected resources.

## Sample Mutation

```graphql
mutation {
  changeContact(
    input: {
      currentContact: "0536369414"
      newContact: "0553018065"
      password: "securePass"
    }
  ) {
    id
    phone
    fullName
  }
}
```

Execute the following GraphQL mutation to change a user's phone:

![change-contact](images/changeContact.png)

### Usage Notes

- The `changeContact` mutation updates the password for the user associated with the provided
  token, current phone,the new desired contact and password in the mutation input

## Expected Response

```json
{
  "data": {
    "changeContact": {
      "id": "23",
      "phone": "0553018065",
      "fullName": "Sam Kafui"
    }
  }
}
```

Upon successful contant change, the API will respond with the user's ID, phone number, full name, and city:

## Manage Address

To change a user's password, utilize the `manageAddress` mutation. This mutation requires the Token, title,city,street, and gps.

## Token Usage

```json
{
  "Authorization": "Bearer <token>"
}
```

Use the obtained authentication token (`token`) in the `Authorization` header of your GraphQL requests to authenticate the user and access protected resources.

## Sample Mutation

```graphql
mutation {
  manageAddress(
    input: {
      title: "Home"
      city: "Adenta"
      street: "street 22"
      gps: "Gh-02-200"
    }
  ) {
    id
    addressTitle
    addressCity
    addressGPS
  }
}
```

Execute the following GraphQL mutation to change a user's phone:

![manage-address](images/manageAddress.png)

### Usage Notes

- The `manageAddress` mutation updates the address for the user associated with the provided
  token

## Expected Response

```json
{
  "data": {
    "manageAddress": {
      "id": "23",
      "addressTitle": "Home",
      "addressCity": "Adenta",
      "addressGPS": "Gh-02-200"
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

![forgot-password](images/forgotpassword.png)

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

## OTP Verification

After initiating the account creation process, a one-time password (OTP) will be sent to the user's phone number. The user needs to verify this OTP to complete the account creation process.

```graphql
mutation {
  verifyOtp(input: { otp: "567633" }) {
    token
  }
}
```

### Sample Mutation

Execute the following GraphQL mutation to verify the OTP for account creation:

![verify-otp](images/verifyOtp.png)

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

## Reset User Password

To reset a user's password, utilize the `resetUserPassword` mutation. This mutation requires the user's ID and the new desired password.

## Token Usage

Use the obtained authentication token (`token`) in the `Authorization` header of your GraphQL requests to authenticate the user and access protected resources.

```json
{
  "Authorization": "Bearer <token>"
}
```

### Sample Mutation

Execute the following GraphQL mutation to reset a user's password:

```graphql
mutation {
  resetUserPassword(input: { newPassword: "new_password" }) {
    id
    fullName
    city
    street
    gps
  }
}
```

![setuppassword](images/setuppass.png)

### Usage Notes

- The `resetUserPassword` mutation resets the password for the user associated with the provided token and the new desired password in the mutation input.

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

## Adding new product

using
[**Admin API**](https://spepa-server.onrender.com/admin-api/)

## Token Usage

Use the obtained authentication token (`token`) in the `Authorization` header of your GraphQL requests to authenticate the user and access protected resources.

```json
{
  "Authorization": "Bearer <token>"
}
```

## Sample Mutation

Execute the following GraphQL mutation to add a product:

```graphql
mutation CreateProduct {
  createProduct(
    input: {
      enabled: true
      assetIds: 1
      translations: {
        languageCode: en
        name: "part name"
        description: "product description"
      }
      customFields: {
        Make: "toyota"
        Model: "Camery"
        Year: 2015
        CountryOfOrigin: "Japan"
        PiecesInStock: "20"
        Price: 20.5
        Condition: "NEW"
        Category: "Wheels "
        Subcategory: "wheels"
      }
    }
  ) {
    name
    id
    createdAt
    languageCode
    description
  }
}
```

![CreateNewSeller](images/addProduct.png) ![CreateNewSeller](images/bottom-addproduct.png)

## Expected Response

# Home

This is the query to fetch categories and all products:

## Sample query

```graphql
query {
  query
  Products {
    products {
      totalItems
      items {
        variants {
          id
          name
          priceWithTax
          price
          currencyCode
          sku
          stockLevel
        }
        name
        slug
        assets {
          id
          name
          source
          preview
        }
        customFields {
          Description
          Make
          Year
          CountryOfOrigin
          Condition
          Category
          reviewCount
        }
        reviews {
          totalItems
          items {
            id
            rating
            body
            summary
            response
          }
        }
      }
    }
  }
  collections {
    items {
      name
      assets {
        id
        preview
      }
      productVariants {
        totalItems
        items {
          id
          name
          price
          assets {
            id
            preview
          }
        }
      }
    }
  }
}
```

![home](images/home.png) ![setuppassword](images/products.png)

## Expected Response

Response (summarized):

```json
{
  "data": {
    "collections": {
      "items": [
        {
          "name": "Wheels & parts",
          "assets": [...],
          "productVariants": {
            "totalItems": ...,
            "items": [...]
          }
        },
        {
          "name": "Exterior Accessories",
          "assets": [...],
          "productVariants": {
            "totalItems": ...,
            "items": [...]
          }
        },
        {...},
        {...}
      ]
    },
     "products": {
      "items": [
        {
          "id": "1",
          "name": "Toyota",
          "description": "2015 toyota wheel",
          "assets": [...]
        },
        {
          "id": "2",
          "name": "FORD",
          "description": "2015  F-150 wheel",
          "assets": [...]
        },
        {...},
        {...},
        {...}
      ]
    }
  }
}
```

## Search Products and Sort

You can use this query to search for products based on a search term and sort the results using various criteria such as top-selling, recommended, recently added, price low to high, or price high to low.

### Query:

```graphql
query Search {
  search(input: { term: "Toyota" }) {
    totalItems
    items {
      productAsset {
        id
        preview
      }
      price {
        ... on PriceRange {
          min
          max
        }
      }
      description
      score
      inStock
    }
    collections {
      count
    }
  }
}
```

![home](images/search.png)

```json
{
  "data": {
    "search": {
      "totalItems": 10,
      "items": [
        {
          "productId": "1",
          "productName": "Product 1"
        }
      ]
    }
  }
}
```

## Description:

- **totalItems:** Total number of products matching the search term.
- **items:** List of products matching the search term, sorted according to the specified criteria.
  - **productId:** The unique identifier of the product.
  - **productName:** The name of the product.

You can adjust the `term` parameter to your desired search term and choose the appropriate sorting option based on your requirements.

<aside class="notice">
  Please note that the sort functionality is currently under development and may not be fully functional. We are working to resolve this issue as soon as possible.
</aside>

# Purchasing Parts

## Detailed item page

To fetch a single item you can use the query

## Sample query

Execute the following GraphQL query to fetch sigle item:

```graphql
query {
  product(id: 1) {
    name
    slug
    variants {
      price
    }
    assets {
      id
      preview
    }
    translations {
      description
    }
    customFields {
      Make
      Model
      Year
      numStars
      averageRating
      CountryOfOrigin
      Condition
    }
  }
}
```

![product](images/detailed.png)

## Expected Response

Upon successfully adding items to the order, the API will respond with the order ID:

```json
{
  "data": {
    "product": {
      "name": "Toyota",
      "slug": "toyota",
      "variants": [],
      "assets": [
        {
          "id": "1",
          "preview": "http://localhost:3000/assets/preview/ea/wheelss__preview.png"
        }
      ],
      "translations": [
        {
          "description": "2015 toyota wheel"
        }
      ],
      "customFields": {
        "Make": "Toyota",
        "Model": "camery",
        "Year": 2015,
        "numStars": null,
        "averageRating": null,
        "CountryOfOrigin": "Japan",
        "Condition": "New"
      }
    }
  }
}
```

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

![home](images/addToCart.png) ![setuppassword](images/checkout.png)

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

## Set Order Billing Address

To provide a billing address for the order, use the `setOrderBillingAddress` mutation. This mutation allows customers to specify the billing address details, including company, street lines, city, province, postal code, and custom fields.

#### Sample Mutation

Execute the following GraphQL mutation to set the order billing address:

```graphql
mutation {
  setOrderBillingAddress(
    input: {
      company: null
      streetLine1: "123 james town"
      streetLine2: ""
      city: "accra"
      province: "G.Accra"
      postalCode: "12345"
      countryCode: "GH"
      customFields: { houseNumber: "25" }
    }
  ) {
    ... on Order {
      id
    }
  }
}
```

![home](images/addAddress.png)

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

## Sample Query

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

## Expected Response

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

![home](images/addShipping.png)

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

## Adding payment to Order

To handle orders in SpePas, utilize the `addPaymentToOrder` mutation. This mutation allows you to associate a payment method with an order.

## Mutation

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

![home](images/addPayment.png)

### Usage Notes

- The `addPaymentToOrder` mutation associates the specified payment method with the order.
- Check the response to determine the success or failure of the payment addition.
- The `Order` type includes the `id` field, providing the order ID after a successful payment.
- Errors or payment failures are communicated through the relevant fields in the response.

## Expected Response

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

Certainly! Here is the updated and formatted documentation for each of the provided mutations and queries, with additional explanations and usage notes for clarity:

---

## Wishlist Operations

### Add to Wishlist

Use the `addToWishlist` mutation to add a product variant to the customer's wishlist.

```graphql
mutation AddToWishlist {
  addToWishlist(productVariantId: "2") {
    id
    productVariant {
      id
      name
    }
  }
}
```

### Query Active Customer Wishlist

Use the `activeCustomerWishlist` query to retrieve the current customer's wishlist, including detailed product information.

```graphql
query activeCustomerWishlist {
  activeCustomerWishlist {
    id
    productVariantId
    productVariant {
      product {
        name
        slug
        assets {
          preview
        }
        customFields {
          Make
          Model
          Description
          Year
          CountryOfOrigin
          Condition
          reviewRating
          reviewCount
        }
      }
    }
  }
}
```

![setuppassword](images/wishlist.png)

### Remove from Wishlist

Use the `removeFromWishlist` mutation to remove an item from the customer's wishlist.

```graphql
mutation removeFromWishlist {
  removeFromWishlist(itemId: "9") {
    productVariant {
      product {
        id
        name
      }
    }
  }
}
```

## Issue Reporting

### Report an Issue

Use the `reportIssue` mutation to report an issue with an order, such as missing items.

```graphql
mutation reportIssue($file: Upload!) {
  reportIssue(
    input: {
      orderNumber: "123456"
      issueType: "Missing Items"
      description: "I received my order but some items are missing."
    }
    file: $file
  ) {
    success
    message
  }
}
```

![setuppassword](images/reportissue.png)

## Product Requests

### Submit Product Request

Use the `submitProductRequest` mutation to request a new product to be added to the catalog.

```graphql
mutation SubmitProductRequest($file: Upload!) {
  submitProductRequest(
    input: {
      productName: "Test"
      quantity: 20
      make: "Honda"
      model: "Civic"
      description: "Test"
      year: "2022"
      countryOfOrigin: "Japan"
      condition: "New"
    }
    file: $file
  ) {
    success
    message
  }
}
```

![setuppassword](images/proRequst.png)
![setuppassword](images/request.png)

### Edit Product Request

Use the `editProductRequest` mutation to edit an existing product request.

```graphql
mutation EditProductRequest($file: Upload!) {
  editProductRequest(
    input: {
      id: "1"
      productName: "Test"
      quantity: 20
      make: "Honda"
      model: "Civic"
      description: "Test"
      year: "2022"
      countryOfOrigin: "Japan"
      condition: "New"
    }
    file: $file
  ) {
    id
    productName
    quantity
    make
    model
    description
    year
    countryOfOrigin
    condition
  }
}
```

### Delete Product Request

Use the `deleteProductRequest` mutation to delete a product request.

```graphql
mutation DeleteProductRequest {
  deleteProductRequest(itemId: "2") {
    id
    productName
    quantity
    make
    model
    description
    year
    countryOfOrigin
    condition
    productRequestImage {
      id
      preview
    }
  }
}
```

## Product Reviews

### Submit Product Review

Use the `submitProductReview` mutation to submit a review for a product.

```graphql
mutation submitProductReview {
  submitProductReview(
    input: {
      productId: 4
      summary: "new-review"
      body: "Great product!"
      rating: 5
      authorName: "sam kay"
      authorLocation: "Accra"
    }
  ) {
    id
    state
  }
}
```

![setuppassword](images/review.png)

---

### Usage Notes

- **Adding to Wishlist**: The `addToWishlist` mutation adds a specified product variant to the customer's wishlist. The response includes the ID of the wishlist item and the product variant details.
- **Querying Wishlist**: The `activeCustomerWishlist` query retrieves all items in the customer's wishlist, including detailed product information such as name, slug, preview image, and custom fields.
- **Removing from Wishlist**: The `removeFromWishlist` mutation removes a specified item from the customer's wishlist. The response includes the details of the removed product variant.
- **Reporting an Issue**: The `reportIssue` mutation allows customers to report issues with their orders, including uploading a supporting file. The response indicates the success of the issue report and provides a message.
- **Product Requests**:
  - **Submitting a Request**: The `submitProductRequest` mutation submits a request for a new product to be added to the catalog, including detailed product information and an optional file.
  - **Editing a Request**: The `editProductRequest` mutation edits an existing product request, allowing changes to all product details and an optional file.
  - **Deleting a Request**: The `deleteProductRequest` mutation deletes a specified product request, returning the details of the deleted request.
- **Submitting a Product Review**: The `submitProductReview` mutation allows customers to submit a review for a product, including a rating, summary, body, author name, and location. The response includes the ID and state of the review.

## User Operations

### Get Current User

Use the `getCurrentUser` query to retrieve the details of the currently logged-in user.

```graphql
query getCurrentUser {
  getCurrentUser {
    id
    phone
    fullName
    roles
  }
}
```

### Switch Account Role

Use the `switchAccount` mutation to switch the current user's role to a different role (e.g., RIDER).

```graphql
mutation switchAccount {
  switchAccount(newRole: RIDER)
}
```

![setuppassword](images/switch.png)

### Usage Notes

- **Get Current User**: The `getCurrentUser` query retrieves the details of the currently logged-in user. The response includes:

  - **ID (`id`)**: The unique identifier of the user.
  - **Phone (`phone`)**: The user's phone number.
  - **Full Name (`fullName`)**: The user's full name.
  - **Roles (`roles`)**: The list of roles assigned to the user.

- **Switch Account Role**: The `switchAccount` mutation allows the current user to switch their role to a specified new role. In this example, the role is switched to `RIDER`. The mutation does not return any fields, but typically, a successful mutation would update the user's session or permissions to reflect the new role.

# Stay Tuned for More!

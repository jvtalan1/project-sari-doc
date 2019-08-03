# API Documentation for Project Sari

Project Sari is a platform that allows mom-and-pop retailers (Sari Sari Stores) to order groceries goods from vendors ( wholesellers) such as supermarkets and distributors directly. This document explains how client application can connect to the platform, access vendor product list and submit orders.

- [My Profile](/my_profile.md)
- [Mobile Authentication](/mobile.auth.md)

Additonal Documents

- [Vendor API, Device Keep Alive](/vendor_api.md)
- [Vendor API, Product Upload](/products_upload.md)

## API End Point

- The API is developed using REST approach.
- Current API end point: https://project-sari/herokuapp.com/c/api
- Example: To get list of available vendors https://project-sari/heroku.com/c/api/vendors/

## Security

To secure the API, user needs to signup and login. Please see next section. Upon login, the API will return a token. You shuold include the token in the header section of your API call.

Example:

```javascript
header: {
  Authentication: "Bearer {token}";
}
```

## Signup

To sign up using API.

**POST** /auth/customer/signup

```javacript
{ "email": "sample-email@test.com",
  "password": "password"
}
```

The complete API URL looks like this: https://project-sari.herokuapp.com/auth/customer/signup

Here's a sample result:

```javascript
{
    "id": "5d01aa1f2bbdf00004833253",
    "email": "sample-email@test.com",
    "user_type": "customer",
    "customer_id": "5d01aa1f2bbdf00004833252",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVkMDFhYTFmMmJiZGYwMDAwNDgzMzI1MyIsImVtYWlsIjoic2FtcGxlLWVtYWlsQHRlc3QuY29tIiwiaWF0IjoxNTYwMzkwMTc1LCJleHAiOjE1NjA0NzY1NzV9.QBmLO7TUYfyj-rnNj9FBlh23-kz0M6n4d1SnobQZWL4"
}
```

## Login

**POST** /auth/customer/login

```javascript
{ "email": "sample-email@test.com",
  "password": "password"
}
```

Sample results:

```javascript
{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVkMDFhYTFmMmJiZGYwMDAwNDgzMzI1MyIsImVtYWlsIjoic2FtcGxlLWVtYWlsQHRlc3QuY29tIiwiaWF0IjoxNTYwMzkwMjc0LCJleHAiOjE1NjA0NzY2NzR9.IhY5Tlk6raQ40MAMRQD3ztjcjeUsAd1ed701PHQIkqI"
}
```

## Vendors List

To get a list of vendors.

**GET** /vendors

Sample result:

```javascript
{
  "vendors":
  [ {"_id":"5cfe18478d08da99bfcae7a5","name":"Super Market 1","legal_name":"Super8 Inc","contact":"3","mobile":"4","telephone":"2"},
    {"_id":"5d00b234e9e6c400045c6c4b","name":"Audrey's company","contact":"","legal_name":"","mobile":"","telephone":""},{"_id":"5d00e2ac4395d10004d25213","name":"My Company"}
    ],
  "total_count":2
}
```

Take note of the vendor id. You will need to supply it in your subsequent calls when you wants to retrieve a list of products.

## Product List

To get list of products from a particular vendor.

**GET** /products?vendor_id=xxx

**Sample call**

GET https://project-sari.herokuapp.com/c/api/products?vendor_id=5cfe18478d08da99bfcae7a5

Results:

```javascript
{"products":[
  { "price":0,"_id":"5cfe185b8d08da99bfcae7aa","barcode":"8998666001726",
    "name":"KOPIKO COFFEE CAFE BLANCA TWIN   52G","category":"#COFFEE (SC & PWD)","price_list_id":"5cfe18478d08da99bfcae7a9","created_at":"2019-06-10T08:44:11.845Z","updated_at":"2019-06-10T08:44:11.845Z","__v":0
  },
  { "price":0,"_id":"5cfe185b8d08da99bfcae7ab","barcode":"4800016021497",
    "name":"GREAT TASTE 3IN1 WHITE TWIN PACK 50G","category":"#COFFEE (SC & PWD)","price_list_id":"5cfe18478d08da99bfcae7a9","created_at":"2019-06-10T08:44:11.845Z","updated_at":"2019-06-10T08:44:11.845Z","__v":0
  },
  { "price":0,"_id":"5cfe185b8d08da99bfcae7ac","barcode":"4800361381024","name":"BEAR BRAND MILK 33G","category":"#POWDERED MILKS (SC&PWD)","price_list_id":"5cfe18478d08da99bfcae7a9","created_at":"2019-06-10T08:44:11.845Z","updated_at":"2019-06-10T08:44:11.845Z","__v":0
  },
  { "price":0,"_id":"5cfe185b8d08da99bfcae7d8","barcode":"4804888889711","name":"BIG 250 JUICE ORANGE 250ML","category":"JUICES","price_list_id":"5cfe18478d08da99bfcae7a9","created_at":"2019-06-10T08:44:11.846Z","updated_at":"2019-06-10T08:44:11.846Z","__v":0}

    // ... additional entries deleted ...
],

"total_count":1518
}

```

## Order Submission

To send an order to the platform

**POST /orders** - Create a new order document

Sample Call:
POST https://project-sari.herokuapp.com/c/api/orders?vendor_id=5cfe18478d08da99bfcae7a5

```javascript

{ "reference": "1",
  "lines": [
    { "product_id": "5d008a41402bc90004131323",
      "quantity": 1,
      "price": 100
    },
    { "product_id": "5d008a41402bc9000413131d",
      "quantity": 2,
      "price": 99
    }
 ]
}
```

Sample results:

```javascript
{
    "_id": "5d01affe2bbdf00004833255",
    "reference": "1",
    "lines": [
        {
            "_id": "5d01affe2bbdf00004833257",
            "product_id": "5d008a41402bc90004131323",
            "quantity": 1,
            "price": 100
        },
        {
            "_id": "5d01affe2bbdf00004833256",
            "product_id": "5d008a41402bc9000413131d",
            "quantity": 2,
            "price": 99
        }
    ],
    "vendor_id": "5cfe18478d08da99bfcae7a5",
    "vendor_name": "Super8",
    "branch_id": "5cfe18478d08da99bfcae7a8",
    "branch_name": "My First Branch",
    "customer_id": "5d00b713e9e6c400045c6c50",
    "customer_name": "My Store",
    "created_at": "2019-06-13T02:07:58.656Z",
    "updated_at": "2019-06-13T02:07:58.656Z",
    "__v": 0
}
```

**GET /orders** - Retrieve list of orders.

Example:

```
GET https://project-sari.herokuapp.com/c/api/orders
```

Results returns the first 50 orders sorted using 'created_at' in descending order.

```json
{
    "orders": [
        {
            "total_quantity": 12,
            "total_amount": 1200,
            "status": "new",
            "_id": "5d08cb49c5caff6e2535d908",
            "reference": "1",
            "lines": [
                {
                    "_id": "5d08cb49c5caff6e2535d909",
                    "product_id": "5d089fd934528b702ec15766",
                    "quantity": 12,
                    "price": 100,
                    "name": "UFC BANANA CATSUP 100G",
                    "barcode": "14285002789"
                }
            ],
            "vendor_id": "5d089fd134528b702ec156f7",
            "vendor_name": "My Company",
            "branch_id": "5d089fd134528b702ec156fa",
            "branch_name": "My First Branch",
            "customer_id": "5d08c15c02273817630bb502",
            "customer_name": "Alexander's Store",
            "created_at": "2019-06-18T11:30:17.846Z",
            "updated_at": "2019-06-18T11:30:17.846Z",
            "document_no": 4,
            "__v": 0
        },
        ...
        ...
],
    "total_count": 4
}
```

**GET /orders/:id** - Retrieve one order.

Retrieve an individual order.

Example:

```
GET https://project-sari.herokuapp.com/c/api/orders/5d08cb49c5caff6e2535d908
```

Sample Result:

```json
{
  "total_quantity": 12,
  "total_amount": 1200,
  "status": "new",
  "_id": "5d08cb49c5caff6e2535d908",
  "reference": "1",
  "lines": [
    {
      "_id": "5d08cb49c5caff6e2535d909",
      "product_id": "5d089fd934528b702ec15766",
      "quantity": 12,
      "price": 100,
      "name": "UFC BANANA CATSUP 100G",
      "barcode": "14285002789"
    }
  ],
  "vendor_id": "5d089fd134528b702ec156f7",
  "vendor_name": "My Company",
  "branch_id": "5d089fd134528b702ec156fa",
  "branch_name": "My First Branch",
  "customer_id": "5d08c15c02273817630bb502",
  "customer_name": "Alexander's Store",
  "created_at": "2019-06-18T11:30:17.846Z",
  "updated_at": "2019-06-18T11:30:17.846Z",
  "document_no": 4,
  "__v": 0
}
```

## Current User

You an use this API to get information about current user and modify following fields: firstname, lastname, mobile and telephone. Email, id and other fields cannot be modified.

**GET /current_user**

Example:

```
GET https://project-sari.herokuapp.com/c/api/current_user
```

Results:

```json
{
  "id": "5d08c15c02273817630bb503",
  "email": "customer1@test.com",
  "user_type": "customer",
  "customer_id": "5d08c15c02273817630bb502"
}
```

**PUT /current_user**

Example:

```
PUT https://project-sari.herokuapp.com/c/api/current_user
```

Body

```json
{
  "firstname": "Alexander",
  "lastname": "Great",
  "mobile": "999-999",
  "telephone": "888-8888"
}
```

Results:

```json
{
  "id": "5d08c15c02273817630bb503",
  "email": "customer1@test.com",
  "firstname": "Alexander",
  "lastname": "Great",
  "telephone": "888-8888",
  "mobile": "999-999",
  "user_type": "customer",
  "customer_id": "5d08c15c02273817630bb502"
}
```

## Current Customer

You an use this API to get information about current customer, which refers to your company. You can modify following fields: firstname, lastname, mobile and telephone. Email, and contact.

**GET /current_user**

The default store name "My Store".

Example:

```
GET https://project-sari.herokuapp.com/c/api/current_customer
```

Results:

```json
{
  "_id": "5d08c15c02273817630bb502",
  "name": "My Store",
  "created_at": "2019-06-18T10:47:56.736Z",
  "updated_at": "2019-06-18T11:11:18.288Z",
  "__v": 0
}
```

**PUT /current_customer**

Example:

Change the store name to Alexander's Store as well as other fields.

```
PUT https://project-sari.herokuapp.com/c/api/current_customer
```

Body

````json
{
    "name": "Alexander's Store" ,
    "mobile": "999-999",
    "telephone": "888-8888",
    "address": "1st Street, BGC",
    "contact": "Mr Handsome"
}```

Results:

```json
{
  "id": "5d08c15c02273817630bb503",
  "email": "customer1@test.com",
  "firstname": "Alexander",
  "lastname": "Great",
  "telephone": "888-8888",
  "mobile": "999-999",
  "user_type": "customer",
  "customer_id": "5d08c15c02273817630bb502"
}
````

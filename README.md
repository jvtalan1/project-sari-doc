# API Documentation for Project Sari

Project Sari is a platform that allows mom-and-pop retailers (Sari Sari Stores) to order groceries goods from vendors ( wholesellers) like supermarkets and distributors directly.  This document explains how client application can connect to the platform, access vendor product list and submit orders.

## API End Point

* Current API end point is located at **https://project-sari.herokuapp.com/c/api/**.  We recomment that you use Postman to try out the API.
* The API is development using REST approach.  

All calls should be prefix with the API end point.

https://project-sari/heroku.com/c/api

For example: to get the the list vendors

https://project-sari/heroku.com/c/api/vendors/

## Signup

To sign up using API.

POST https://project-sari/heroku.com/c/api/auth/customer/signup

{ "email": "sample-email@test.com",
  "password": "password"
}

Sample results from success.

{ "id": "123421341234234"
  "email": "sample-email@test.com",
  "token": "xxxx"
}

## Login

POST https://project-sari/heroku.com/c/api/auth/customer/login

{ "email": "sample-email@test.com",
  "password": "password"
}

Sample results from scucess:

{ token: "xxxxx"
}

## Security

All subseqent calls needs to have token in the header.

header: {
  Authentication: "Bearer {token}"
}

## Vendors List

To get a list of vendors.

GET /vendors


## Product List

To get list of products from a particular vendor.

GET /products?vendor_id=XXX


## Order Submission

To submit an order.

POST /orders

``` javascript
{ "reference": "1",
  [ { "product_id": "1111",
      "price: 100.00,
      "quantity", 1
    } 
  ],  
}

```
Above is the minimum information required.








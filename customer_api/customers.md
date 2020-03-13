# Customers API

One user can access another customer if he has been given proxy access. (See [delegation section](delegation.md)).

Proxy access is vendor specific so vendor_id needs to be specified. With the proxy access, it is implied that one user an also change another customer's (target customer) information including store name, address and telephone.

## Get Customer

```
GET /c/api/customers/{id}?vendor_id={vendor_id}
```

## Update Customer

```
PUT /c/api/customers/{id}?vendor_id={vendor_id}
```

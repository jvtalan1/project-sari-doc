# Delegation of Order

This delegation feature of Suki permit one customer to delegate an ability to another customer. For example: a customer may allow another customer to place an order his behalf. We shall call it `proxy order`.

## Introduction to Delegation

- Ability name: `proxy_order`
- Description: Permits one party (proxy) to order on behalf of anotehr party (customer).

Parties

- Proxy - the party who would like to order on behalf of customer
- Customer - the real customer the order is intended for

Steps:

1. Proxy requests for authorization providing mobile number of Customer
2. Customer receives an SMS with code
3. Customer informs Proxy of the code
4. Proxy verifies the code with Suki Server
5. Authorization completed

## Requesting for Delegation (for Proxy)

### 1. Request for Delegation of a 'order' Ability

```
POST /c/api/delegations/proxy-request?mobile={mobile-no-of-customer}&ability=order&vendor_id={id}
```

- `mobile` - mobile number of the customer you would like place order on behalf
- `ability` - must be 'order'
- `vendor_id` - for which vendor

Sample Returns 200 if Successful:

```json5
{
  _id: "5e69f107ee11c0f51e7c19d1",  // we need to validate this verification with OTP
  proxy_user_id: "5e69967056fd6a301a89d11f"
  user_mobile: "639178602222",
  user_id: "5e69eff2b66286ec18a2f076",
  customer_id: "5e69eff2b66286ec18a2f077",
  vendor_id: "5d78d7c85bffd900041d88b4",
  ability: "order",
  verified: false,
}
```

`_id` is the verification_id you need to use in the subsequent calls to validate.

### 2. Validating the Delegation

```
POST /c/api/delegations/proxy-validate?verification_id={verification_id}&otp={otp}
```

Returns 200 if successful

### 3. Cancelation of Ability

This API removes the ability of proxy to order (not yet implemented)

```
POST /c/api/delegations/proxy-cancel?mobile={mobile-no-of-customer}&ability={order}&vendor_id={vendor_id}
```

## Checking Delegations (for Customer)

### Get a list of delegations

```
GET /c/api/delegations
```

### Cancel a deletagion

```
DELETE /c/api/delegations/{deletation-id}
```

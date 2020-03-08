# Delegation of Order

This delegation feature of Suki permit one customer to delegate an ability to another customer. For example: a customer may allow another customer to place an order his behalf. We shall call it `proxy order`.

## Delegation Basics

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

## Delegation API using SMS (Proxy Side)

### 1. Request for Delegation of a specific Ability

```
POST /c/api/delegations/proxy-request?mobile={mobile-no-of-customer}&ability=proxy_order
```

### 2. Verification of Code

```
POST /c/api/delegations/proxy-verify?mobile={mobile-no-of-customer}&code={sms-code}&ability={proxy_order}
```

### 3. Cancelation of Ability

This API removes the ability of proxy to order

```
POST /c/api/delegations/proxy-cancel?mobile={mobile-no-of-customer}&ability={proxy_order}
```

## Delegation API (customer side)

### Get a list of delegations

```
GET /c/api/delegations
```

### Cancel a deletagion

```
DELETE /c/api/delegations/{deletation-id}
```

### Cancel all deletagion

```
DELETE /c/api/delegations/
```

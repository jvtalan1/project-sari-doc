# Payment Types

Suki has an API for creation and management of payment types. Examples of payment types are "cash", "credit_card", "paymaya", "banktobank".

# Update payment types of a vendor

`PUT /api/current_vendor/payment_types`

Example Contents put be submitted

```json
[
  {
    "type": "cash",
    "name": "Cash"
  },
  {
    "type": "paymaya",
    "name": "Credit Card"
  },
  {
    "type": "manual",
    "name": "Online Remittance",
    "message": "Bank to bank remittance"
  }
]
```

For the payment type with code "cash", "paynamics", "paymaya", My Suki and Suki hub has specially ability to handle.

# Get payment types of current vendor

`GET /api/current_vendor/payment_types`

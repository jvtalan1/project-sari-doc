# Paymaya Credit Card Support

Suki Commerce Platform supports paymaya credit card payments. For it to communicate with Paymaya, it requires the public key from vendor's Paymaya account.

In order to provide live feedback on the payment status, the secret key is required for one time only to configure the web-hooks. Currently, this configuration is done manually.

# Vendor Portal

## 1. Add "paymaya" public key

`PUT /api/vendor_secrets`

Save the payama public key.

```json5
{
  paymaya: {
    public_key: "xxxxxxx",
  },
}
```

**Security Note**: Take note this API is only accessible to admin users.

## 2. Add 'paymaya' Payment Type

Add paymaya to list of our supported payment types and status of "A".

`PUT /api/current_vendor/payment_types`

```json
[
  {
    "type": "cash",
    "name": "Cash"
  },
  {
    "type": "paymaya",
    "name": "Credit Card",
    "status": "A"
  }
]
```

**Important Note**:

This API replaces all the payment types. The payment type of cash should always be there.

Mobile App should detect presence of `payment_types` in the vendor settings. If so, it can safely ignore the earlier `payment_methods` field.

`payment_types` is an array object while `payment_methods` is an array os String, which contains less information.

### 3. Order Status

When an order with payama payment method is received, the initial payment status is "U" (Unpaid).

```json5
{
  payment_method: "paymaya",
  payment_status: "U",
  payment_amount: 0,
}
```

When payment is completed the by user. The payment status of the order will changed to "F" (Finished), and the payment amount will be filled up. (In the example below, it's P1000.)

```json5
{
  payment_method: "paymaya",
  payment_status: "F",
  payment_amount: 1000,
}
```

It is up the Vendor Portal to display this payment status information correctly for the backend users.

### 4. Resending Checkout URL

In case of error, there may be a need to resend the checkout URL. Use the API below to request a checkout URL to be resend to the user.

`POST /api/orders/xxxx/paymaya`

An SMS will be send to the user containing the checkout URL.

# Mobile App

## 1. Submitting Order

To submit an order, provide "paymaya" as the payment_method, instead of "cash".

```json5
{
  lines: [
    {barcode: '111', quantity: 1},
    {barcode: '222', quantity: 1}
  ]
  payment_method: "paymaya",
}
```

After the order is created, user will receive an SMS containing a link and instructions on how to checkout. When payment is completed. Paymaya provides real-time feedback to suki server through web-hook.

## 2. Payment Completed

When payment is completed, payment status will be changed to "F" (Finished) from "U" (Unpaid).

Sample contents of order json:

```json5
{
    payment_status: "F"
    payment_amount: 999
}
```

## 3. Handling Payment Error

When there is an error, the payment status may or may not be updated. If Paymaya provides feedback. It will be reflected in the following fields.

```json5
{
    payment_status: "E"
    payment_error: "Error message"
}
```

In this case, mobile should be able request for another SMS containing a checkout URL.

`POST /c/api/orders/{order_id}/paymaya`

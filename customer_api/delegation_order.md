## Order Submission

To send an order to the platform

### Submitting a New Order

Sample Call:

```
POST /c/api/orders?vendor_id=5cfe18478d08da99bfcae7a5
```

```json5
{
  reference: "1",
  // Specify a different other than default customer
  target_customer_id: "",
  lines: [
    { product_id: "5d008a41402bc90004131323", quantity: 1, price: 100 },
    { product_id: "5d008a41402bc9000413131d", quantity: 2, price: 99 }
  ]
}
```

# Coupons

Suki supports use of coupons as a form of promotions. Coupon are created by the
marketing department and requires approval by the finance department.

### Coupon Creation

Coupon can be created from Coupons Manager. Only Marketing department has access to
coupon creation and coupon upload. While only Finance manager has the ability to approve
the final use of the coupons.

As of the moment (March 2020), Suki only supports gift certicate with face values (example 1),
free shipping (example 2) and bundle offer coupons (example 4).

### Cases

Example 1. Gift Certicate

```json5
{
  code: "FREE100",
  name: "100 Peso Gift Certificate",
  value: 100,
  min_amount: 5000
}
```

Example 2. Free shipping

```json5
{
  code: "SHIPFREE",
  name: "Free Shipping",
  shipping: "-100%",
  min_amount: 5000
}
```

Example 3. Discount on Shipping

```json5
{
  code: "SHIP50OFF",
  name: "50 Pesos Off",
  shipping: "-50",
  min_amount: 2000
}
```

Example 4. Bundle Offer

```json5
{
  code: "SPO1",
  name: "Special Offer: Less P72 for 2 Cases of Coke and 1 Case of Sprite",
  bundle: [
    { barcode: "111", quantity: 48 },
    { barcode: "222", quantity: 24 }
  ],
  price: "-72",
  quantity: 5, // maximum 5 quantity can be used
  expires: "2020-03-30" // expiry date
}
```

Example 5. Special Item offer

```json5
{
  code: "SP02",
  name: "Free: Uniqlo Umbrella",
  barcode: "111", // barcode of umbrella
  expires: "2020-03-30" // expiry date
}
```

Example 6. Special Item discount

```json5
{
  code: "SP03",
  name: "50% for Umbrella",
  barcode: "111", // barcode of umbrella
  price: "50%",
  expires: "2020-03-30" // expiry date
}
```

### CSV Upload

`mobile_no,coupon_code,quantity`

# Bundles

(DRAFT --- FOR Phase II Implementation)

Suki Vendors can sell items in bundles.

## Defining a bundle

You can defined the bundle through the interface or by using upload tools.

## CSV Format

`bundle_code, barcode, bundle_name, price, points, start, end, status, visible`
`barcode1, quantity1, barcode2, quantity2, barcode3, quantity3, barcode5, quantity5`

## Bundle Works like Promotions

Bundle works like a promotion, it can have an start date and an end date. If the
bundle is visible, all the users in Suki can see the bundle when he searches for
any of the items included in the bundle. Bundle can earn points if the `points` field is specfied.

### Example Bundle

Coke (333) is P10 x 24 x 2 = 480
Sprite (444) is P8 x 24 = 192
Total regular price = 672

```json5
{
  name: "2 Cases of Coke and 1 Case of Sprite",
  code: "333+444", // bundle uniquely identifies the bundle in uploads
  items: [
    { barcode: "333", quantity: 48 }, // item 1
    { barcode: "444", quanitty: 24 } // item 2
  ],
  price: "600", // less 72 pesos
  start: "03-01-2020",
  end: "03-07-20202"
}
```

## Bundle Visibility

Invisible bundle are useful in conjunction with coupons.

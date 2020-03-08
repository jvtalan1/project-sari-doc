# Promotion Language

(DRAFT - WORK IN PRGORESS)

### Simple Discount

<!--
  description: Specified new or discounted price
  old_price: 20
  barcode: 1234
  new price: 19.50
 -->

```json
{
  "code": "DISCOUNT-PRICE",
  "name": "Discounted Price",
  "items": [{ "barcode": "1234", "price": 19.5 }]
}
```

### Simple Discount with Quantity

<!-- For example,
Scenario: Buy 10KG for price of 9
barcode: 111
unit price: P20,
 -->

```json
{
  "name": "Buy 10KG for the price of 9KG",
  "code": "10FOR9",
  "items": [
    {
      "barcode": "111",
      "quantity": 10,
      "price": 180,
      "message": "Buy 10KG for the price of 9KG"
    }
  ]
}
```

### Simple Percent Discount

<!--
  description: Less 10% for every item included in the promo
  old_price: 20
  barcode: 111, 222, 333
  discount: 10%
 -->

```json
{
  "name": "P&G Discount for Summer",
  "code": "PERCENT",
  "message": "Less 10%",
  "discount": "10%",
  "items": [{ "barcode": "111" }, { "barcode": "222" }, { "barcode": "333" }]
}
```

### Less Peso Value

<!--
  description: Less 1 pesos for every item
  old_price: 20
  barcode: 111, 222, 333
  discount: -1 (less 1 peso)
 -->

```json
{
  "name": "Discount 10%",
  "code": "PERCENT",
  "discount": "-1",
  "items": [{ "barcode": "111" }, { "barcode": "222" }, { "barcode": "333" }]
}
```

<!-- For example,
Scenario: Buy 1 Case for get 7% off
    barcode: 111
    unit price: P20,
    case quantity: 24
 -->

```json
{
  "name": "Buy 1 case get 7% off",
  "code": "1CASE7OFF",
  "items": [{ "barcode": "111", "quantity": 24, "price": "7%" }]
}
```

<!-- For example,
Scenario: Buy 2 Case of X and 1 case y, get peso off
    item 1: alaka milk
    barcode: 111
    unit price: P20,
    case quantity: 24

    item 2: alaska evaporada
    barcode: 222,
    unit_price: P30,
    case_quantity: 12,

    discount: 506
 -->

```json
{
  "name": "Buy this bundle (2 Case + 1 Case), get 506 pesos off",
  "code": "1CASE7OFF",
  "items": [
    {
      "bundle": [
        { "barcode": "111", "quantity": 24 },
        { "barcode": "222", "quanitty": 12 }
      ],
      "price": "-506"
    }
  ]
}
```

# Points Discount

<!-- buy 1 item, get 78 points
  barcode: 111
  points: 78
 -->

```json
{
  "name": "Buy 1 Nissin Minicup, get 78 points",
  "code": "NISSIN",
  "items": [{ "barcode": "111", "points": 78 }]
}
```

# Applicable to All

```json
{
  "name": "60 points for every 4000",
  "code": "4000",
  "scope": "all",
  "trigger": { "amount": 4000, "points": 60 }
}
```

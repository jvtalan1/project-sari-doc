# Suki Promotion Language

(DRAFT - WORK IN PRGORESS)

## A. Item Promotion

Each item is given its own discount. Actual Price is calculated based on the value of `discount`. The value is string which can interpretted as a discounted price, percent discount, or amount discount.

As many as 1000 items can be included in single promotion.

Let's illustrate with an example. Our fictitious March 2020 promotion has 3 participating items. Item 111 is given 10% off, item 222 has discounted price of 25 pesos, and item 333 is offered less 5 pesos. Below is the syntax for above scenario.

Example: Price Off on Selected Items

```json5
{
  name: "Price off on selected items",
  code: "PRICEOFF2020-03",
  started: "2020-03-01",
  ended: "2020-03-30",
  type: "items",
  items: [
    {
      barcode: "111",
      discount: "10%"
    },
    {
      barcode: "222",
      discount: "25"
    },
    {
      barcode: "333",
      discount: "-5"
    }
  ]
}
```

Format:

```json5
{
  name: "promotion-name",
  code: "identification-code",
  message: "display mssage for user",
  start: "start-date-time",
  end: "end-date-time",
  type: "items",
  items: [
    {
      barcode: "barcode1",
      quantity: "1",
      discount: "discount",
      points: "points"
    },
    {
      barcode: "barcode2",
      quantity: "1",
      discount: "discount",
      points: "points"
    }
  ]
}
```

More examples can be found in the Sample Section below.

## B. Overall Promotion

Promotion is applicable to the entire transaction. It is trigger when certain amount is reached.
Promotion type is determined with the keyword `all`.

Format:

```json5
/* Overall Promotion */
{
  name: "Promotion name",
  code: "promo identification code",
  start: "start-date-time",
  end: "end-date-time",
  messaage: "display mssage for user",
  type: "all" /* applicable to all items */,
  triggers: { amount: "" },
  /* rewards to be given when trigger is reached */
  rewards: {
    discount: "" /* can be amount, less percentage, less amount */,
    points: "" /* can be points */
  },
  repeat: "once|every" /* default to once, reward is only given once, every: reward is given for every amount-trigger */
}
```

## C. Pool Promotion

Format:

```json5
{
  name: "Promotion name",
  code: "promo identification code",
  message: "display mssage for user",
  type: "pool",
  start: "start-date-time",
  end: "end-date-time",
  items: ["barcode1", "barcode2", "barcode3"],
  triggers: { amount: "" },
  rewards: {
    discount: "discount",
    points: "points"
  },
  repeat: "once|every"
}
```

# Samples

## 1. Simple Discount

Example 1: Special Price

```json5
{
  code: "001",
  name: "Special Price",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", discount: 19.5 }]
}
```

Example 2: Percent Off

```json5
{
  code: "002",
  name: "Ten Perent Off",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", discount: "10%" }]
}
```

Example 3: Less Amount

```json5
{
  code: "003",
  name: "Less 1 Peso For every item",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [
    { barcode: "111", discount: "-1" },
    { barcode: "222", discount: "-1" }
  ]
}
```

## 2. Simple Discount with Quantity

For the examples below, we assume item `111` has unit price of P20.

Example 4: Discounted for Given Quantity

```json5
{
  code: "004",
  name: "Buy 10 for price of 9",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", quantity: 10, discount: "180" }]
}
```

Example 5: Less % for Given Quantity

```json5
{
  code: "005",
  name: "Less 10% if you buy 10 units",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", quantity: 10, discount: "10%" }]
}
```

Example 6: Less value for Given Quantity

```json5
{
  code: "006",
  name: "Less P15 if you buy 10 units",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", quantity: 10, discount: "-15" }]
}
```

## 3. Earning Points

Example 7: Earn 5 points for every item purchase

```json5
{
  code: "007",
  name: "Earn 5 points for every unit bought",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", points: 5 }]
}
```

Example 8: Earn 20 points if you buy 10 units (One-time only)

```json5
{
  code: "008",
  name: "Earn 10 points when you buy 10 units (one-time-only)",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", quantity: 10, points: 20, repeat: "once" }]
}
```

Example 9: Earn 20 points for every 10 units purchase

```json5
{
  code: "009",
  name: "Earn 20 points for every 10 units",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", quantity: 10, points: 20, repeat: "every" }]
}
```

## 4. Pool Promotions

Example 10: Get 50 pesos off on purchase of 1000 selected Nestle Items

Following are the barcodes of participating items: 111, 222 & 333.

```json5
{
  name: "Nestle Promotion 1",
  code: "NESTLE1",
  message: "Get 50 off on purchase of 1000 worth of Nestle products",
  type: "pool",
  start: "2020-03-01",
  end: "2020-03-07",
  items: ["111", "222", "333"],
  triggers: { amount: 1000 },
  rewards: { discount: 50 },
  repeat: "every"
}
```

Example 11: Earn extra 50 points on minimum purchase of 2000 worth of Nestle products

Following are the barcodes of participating items: 111, 222 & 333.

```json5
{
  name: "Nestle Promotion 2",
  code: "NESTLE2",
  message: "Earn extra 50 points on min purchase of 2000 Nestle products",
  type: "pool",
  start: "2020-03-01",
  end: "2020-03-07",
  items: ["111", "222", "333"],
  triggers: { amount: 2000 },
  rewards: { points: 50 },
  repeat: "once"
}
```

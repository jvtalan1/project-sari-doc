# Suki Promotion Language

(DRAFT - WORK IN PRGORESS)

## A. Item Promotion

Each item has its own defined promotion. Price is re-calculated based on the price field which can be
a discounted price, percent discount, or less amount. Promotion type is determined with the presence
of the field `items`.

```json5
/* Item Promotion */
{
  name: "Promotion name",
  code: "promo identification code",
  message: "display mssage for user",
  start: "start-date-time",
  end: "end-date-time",
  type: "items",
  /* items included in the promotion */
  items: [
    {
      barcode: "item-barcode",
      quantity: "1" /*  quantity to trigger the promotion, optional default to 1 */,
      price: "discounted price" /* optional promotion price, can be a number, %, or -number */,
      points: "points earn" /* optional points earn for every quantity purchase */
    },
    /* -- another item -- */
    {
      barcode: "item-barcode",
      quantity: "1",
      price: "discounted price",
      points: "points earn"
    }
  ],
  /* quantity, price, points if specified at the root level can be used as default values
   in case individual items does not indicate */
  quantity: "",
  price: "",
  points: ""
}
```

## B. Overall Promotion

Promotion is applicable to the entire transaction. It is trigger when certain amount is reached.
Promotion type is determined with the presence of the keyword `scope` = `all`.

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
    amount: "" /* can be amount, less percentage, less amount */,
    points: "" /* can be points */
  },
  repeat: "once|every" /* default to once, reward is only given once, every: reward is given for every amount-trigger */
}
```

## C. Pool Promotion

```json5
/* Item Promotion */
{
  name: "Promotion name",
  code: "promo identification code",
  message: "display mssage for user",
  type: "pool",
  start: "start-date-time",
  end: "end-date-time",
  /* items included in the promotion, when any of these items are purchased */
  items: ["barcode", "barcode", "barcode"],
  triggers: {
    amount: "" /* can be amount, when amount is reached */,
    quantity: "" /* can be quantity, when quantity is reached */
  },
  rewards: {
    amount: "" /* can be amount, less percentage, less amount */,
    points: "" /* can be points */
  },
  repeat: "once|every"
}
```

# Sample Promotions

## 1. Simple Discount

Example 1: Special Price

```json5
{
  code: "001",
  name: "Special Price",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", price: 19.5 }]
}
```

Example 2: Percent Off

```json5
{
  code: "002",
  name: "Ten Perent Off",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", price: "10%" }]
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
    { barcode: "111", price: "-1" },
    { barcode: "222", price: "-1" }
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
  items: [{ barcode: "111", quantity: 10, price: "180" }]
}
```

Example 5: Less % for Given Quantity

```json5
{
  code: "005",
  name: "Less 10% if you buy 10 units",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", quantity: 10, price: "10%" }]
}
```

Example 6: Less value for Given Quantity

```json5
{
  code: "006",
  name: "Less P15 if you buy 10 units",
  start: "2020-03-01",
  end: "2020-03-07",
  items: [{ barcode: "111", quantity: 10, price: "-15" }]
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

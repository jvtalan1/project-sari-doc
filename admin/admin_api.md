# Copying Products

This API allow administrator to copy products from one account to another

POST http://sukihub.com/a/api/products/copy

```json
{
  "source": "CODE1",
  "target": "CODE2",
  "filter": "\"luckyme\"",
  "options": {
    "mode": "basic",
    "set_default_price": 1
  }
}
```

Options:

- mode: basic or all
  basic: copy only basic fields
  all: copy all fields including wholesle packages and price

- set_default_price: 0 or 1
  if 1 or true, set the default price to 0.01
  if 0 or false, original price will be copied

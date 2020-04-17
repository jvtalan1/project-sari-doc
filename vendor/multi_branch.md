# Multi-Branch Capability

(DRAFT)

Suki platform is designed for enterprise operation therefore, it supports multiple branches, multiple-prices lists and inventory tracking for each branch.

## Branch

A branch is location where business can use as a 'distribution-hub' to stock inventories to be sold for a certain area.

## Price List

A price list is list of items with barcode, name and price information. Each branch needs to be associated with exactly one price list.

## Inventory

Suki tracks inventory by branch. There are 3 fields associated with each inventory entry, `quantity`, `reserved` and `average`. Quantity is the quantity on hand of the particular item in that branch. `Reserved` field is used to track items ordered by customers but not yet delivered. `Average` field is used to store the average daily sales of the store. Together, we can used these 3 fields to calculate the available quantity to the Suki users.

## Managing Branch List, Price List and Inventory from Suki-Hub

Suki Hub allows administrator to create multiple branches and multiple price lists. Each branch is associated with a price list.

## Internal Design

### products

These are the basic fields in `products` collection

```
_id,price_list_id,barcode, name, price
```

### favorite_products

```
branch_id, product_id,alt_category,alt_subcategory
```

### price_lists

The price_list contains all the items that are available for a one or more branches including their prices.

```
_id, price_list_id,product_id,price + barcode,name, etc..
```

# Interim Migration Strategy

###

# POS printing API

When the picker finished processing the order, the order with final quantities is sent to
POS for printing.

# Picker App

### Send to POS

```
PUT /orders/{id}/print
```

# Automated Printing Agent

Automated Printing Agent (APA) is required to perform two API calls. First is to fetch a document for printing; and then after printing, mark the document as printed.

The system authenticate user with access-token which allows it to infer which branch the POS is located, therefore, it is not neccessary to pass branch id or user id.

## Fetch an Order for Printing

Fetch an order from POS print queue.

```
GET /orders?q=get_next_to_print
```

Returns exactly 1 order for printting.

## Mark Order as Printed

```
PUT /orders/{id}/mark_as_printed
```

When the order is printed, the print_count is incremented.

## Check the POS Printing Queue

Check the contents of print queue.

```
GET /orders?q=print_queue
```

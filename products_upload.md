# Product Upload

**POST** /products/upload

### CSV fields

Following fields are expected in the CSV file. The only required fields are barcode and name.

- barcode\* (unique, use as key to identify the item)
- name\*
- price
- category
- volume
- status: A - active, D - deleted, default is 'A'

### Status

To delete an product, simply set the status to 'D'.

### Volume

The volume fields indicates the total quantity sold within a period. Volume is used to sort the return result. Higher volume first and lower volume last.

### Options **_reset_volmume_**

- 1: all other items not included in the CSV file shall be set to 0. use in complete upload
- 0: don't reset the volume back zero, use in incremental upload (default)

Example:

Using the following url will reset the volume of entire product list to zero except for items in the

```
/products/upload?reset_volume=1
```

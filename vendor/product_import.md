# Product Importation Behavior

## Turn on Description Matching

When description matching is turned on, Suki uses the description of the master product database. Suki Team shall provide the `master_account_id` of master database if available.

During importation, if an item has a matching `barcode`, the description of the item from the master database shall always be used. If there is none, the description from the imported CSV file shall be used.

## Description Override

When modification is made locally from the Vendor portal, `name_override` flag is set (turned on), the description of the item can no longer be override in CSV import or product upload.

## Priority

1. master description matching ON - uses name from master database
2. override_name ON (per product) - use name from locally modified
3. CSV name - uses name from CSV

After we turn-ff description matching, the names override will remain on. To turn it off, we need explicity import the field override_name= false

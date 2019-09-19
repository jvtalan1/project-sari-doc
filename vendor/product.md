# Product API

Base URL: https://project-sari.herokuapp.com/

## LIST

```
GET /api/products/?vendor_id={vendor_id}
```

Example:

```
https://project-sari.herokuapp.com/api/products/5d72ff031d4c2ed009ca4bc5?vendor_id=5d089fd134528b702ec156f7
```

## SEARCH

```
GET /api/products/?vendor_id={vendor_id}&search={search term}
GET /api/products/?vendor_id={vendor_id}&search={barcode}
```

Example:

```
https://project-sari.herokuapp.com/api/products/5d72ff031d4c2ed009ca4bc5?vendor_id=5d089fd134528b702ec156f7&search=Lucky+Me
```

## GET

```
GET /api/products/{id}?vendor_id={vendor_id}
```

Example:

```
http://localhost:5000/api/products/5d72ff031d4c2ed009ca4bc5?vendor_id=5d089fd134528b702ec156f7
```

## UPDATE

```
PUT /api/products/{id}?vendor_id={vendor_id}
```

Example:

```
http://localhost:5000/api/products/5d72ff031d4c2ed009ca4bc5?vendor_id=5d089fd134528b702ec156f7
```

```
{
  "name": "new name"
}
```

## UPLOAD IMAGE

```
POST /api/products/{id}?vendor_id={vendor_id}
```

Pass the image in the "file" as if you are uploading a file from a html FORM.

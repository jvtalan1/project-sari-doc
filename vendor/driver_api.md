# Driver App API

"My Driver" app is used by the driver/rider.

Proposed workflow.

1. Drivers (peson) uses the App to scan the QR code or barcode generated from picking receipt. When camera is not available, driver can enter the document number.
2. The App call server to retrieve the document providing the document number. The server will only return the document if there is a matching document and the document is in the correct state. The state of the document must be **pick/ended**. In the future, server may provide packing information.
3. The document contains delivery information including customer name, mobile number, address, including latitude and longitude, which can be use in navigation. The origin address can be obtain from current vendor.
4. The Driver App opens Waze or Google Map to navigate to customer. When needed, the driver may call or text the customer from the App using phone integration.
5. When driver arrives customer location, my driver asks permission takes a picture of the customer with the items received. if the customer refuses to let the driver take the picture, the app has the option to have customer digitally "sign" the acknowledgement.
6. The App submits the picture to server and the order is considered received by the customer.

## 1. Get Document and Start of Delivery

```
GET /api/orders/{document_no}
```

**Returns:**

- status: 404 -> if document is not found or document not in correct state
- status: 200 -> Successful

Note: Order API now supports retrieving using id or document_no.

## 2. Start of Delivery

```
PUT /api/orders/{id}/start_delivery
```

## 3. Submit Picture and Mark as Received

```
PUT /api/orders/{id}/end_delivery
```

Attached picture and/or signature image using field name "file".

**Returns:**

- status: 404 -> document id not found
- status: 200, successful

Note: The image or file will be saved to AWS S3. The server will return successful without waiting for saving to complete. In case of saving error, the server will fail silently. Upon saving, the order JSON will contain the field `extras.received_image_url` which will point to the image.

## 4. Others

To retrieve information including address and coordinates of the vendor, use the following API.

```
GET /api/current_vendor
```

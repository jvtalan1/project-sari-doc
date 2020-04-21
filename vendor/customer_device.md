# Customer Device API

Customer Device API is used to manage customer devices. We created this API to register the device information of customers as well as to register push notification tokens.

Each device must be associated with a user.

To call the APIs below, you must provide the json-web-token (jwt) of the customer in the header.

```
Authentication: Bearer {jwt}
```

## Register a Customer Device

```
POST c/api/customers/{customer_id}/devices
```

Following fields are required.

```json
{
  "brand": "Samsung",
  "device_id": "device-id-12345",
  "device_token": "ExponentPushToken[abcde12345]",
  "manufacturer": "Samsung Electronics",
  "model_name": "Galaxy S10",
  "os_name": "Android",
  "os_version": "10"
}
```

After the device is created, an object is return containing both the id and the token.

```json
{
  "_id": "5d0c82b13c3212471483b88f",
  "brand": "Samsung",
  "device_id": "device-id-12345",
  "device_token": "ExponentPushToken[abcde12345]",
  "manufacturer": "Samsung Electronics",
  "model_name": "Galaxy S10",
  "os_name": "Android",
  "os_version": "10",
  "created_at": "2019-06-21T07:09:37.489Z",
  "updated_at": "2019-06-21T07:59:07.531Z"
}
```

## List All devices

```
GET c/api/customers/{customer_id}/devices
```

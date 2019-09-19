# Device API

Device API is used to manage devices. We created this API to monitor the software (devices) installed at the client side. An example of which is the "agent" software that extracts the updated prices and submit to the platform daily.

After device is created, the program may call the Ping-API to report its last activities.

Each device must be associated with a vendor and branch. Currently, one default branch is automatically associated with the vendor.

To call the API belows, you must provide the json-web-token (jwt) of the vendor in the header.

```
Authentication: Bearer {jwt}
```

## Create a Device

```
POST /api/devices/
```

Following fiels are required.

```json
{
  "name": "Barter Agent",
  "version": "1.0",
  "admin_name": "Hubert Dy",
  "admin_email": "hdy@gmail.com"
}
```

After the device is created, an object is return containing both the id and the token.

```json
{
  "_id": "5d0c82b13c3212471483b88f",
  "name": "Barter Agent",
  "version": "1.0",
  "admin_email": "hdy@gmail.com",
  "admin_name": "Hubert Dy",
  "vendor_id": "5d089fd134528b702ec156f7",
  "vendor_name": "My Company",
  "branch_id": "5d089fd134528b702ec156fa",
  "branch_name": "My First Branch",
  "last_activities": [],
  "created_at": "2019-06-21T07:09:37.489Z",
  "updated_at": "2019-06-21T07:59:07.531Z",
  "token": "87ab30a752aafedec69cd5d66c881fce6b70be8c93e0f78f"
}
```

## Update a Device

```
PUT /api/devices/{device_id}
```

For example, to change the version number.

```json
{
  "version": "1.1"
}
```

## Delete a Device

```
DELETE /api/devices/{device_id}
```

## List All devices

```
GET /api/devices/
```

# Ping

When the device is created, a token is automatically assigned.

```
POST /api/ping/{device_id}?token={device_token}
```

The server will update the device last_active_at field.

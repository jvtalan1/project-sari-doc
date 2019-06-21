# Vendor API

Follwoing API are provided for the Vendors.

# Device API

Device API is used to manage devices. We created this API to monitor the software (devices) installed at the client side. An example of which the "agent" software which use to automatically extract the updated prices and submit to the platform daily.

After device is created, the program can call the ping API to report its last activities.

Each device must be associated with a vendor and branch. Currently, one default branch is automatically associated with the vendor.

To call the API belows, you must provide the json-web-token (jwt) in the header.

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


# Push Notification

**There are three main steps to setting up push notifications:**
1. getting a user's Expo Push Token
2. calling Expo's Push API with the token when you want to send a notification
3. responding to receiving the notification in your app (maybe upon opening, you want to jump to a particular screen that the notification refers to)

Create user device to store the information of the registered device

**sample request from the mobile app**

```
{
    "brand": "samsung",
    "device_id": "5df2de0c-52f2-4dfd-8a33-2117f45e0c01",
    "device_token": "ExponentPushToken[jjz1aINJ4qTuS_Ea7DtyP1]",
    "manufacturer": "samsung",
    "model_name": "SM-A505GN",
    "os_name": "Android",
    "os_version": "10"
}
```

we want to save the device token and other information of the users device, so create a table `user_device`
and associate the `user_device` table to `UserSchema` to accommodate has many device_devices or multiple devices in one user
```
new Schema (
{
	brand: String,
	device_id: String,
	device_token: String,
	manufacturer: String,
	model_name: String,
	os_name: String,
	os_version: String
})
```


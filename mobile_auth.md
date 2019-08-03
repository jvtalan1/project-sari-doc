# Mobile Sign up and Login

Project Sari offers sign up and login using mobile number and SMS text servce.

## To Signup

### Step 1. Request

```
POST /auth/customer/mobile-request-signup/
```

```json
{ "mobile": "639971733576" }
```

5 digit random number SMS code will be send to the mobile device.Server returns status 200, message = "SMS code send. please complete signup within 10 minutes".

### Step 2. Complete Signup

```
POST /auth/customer/mobile-signup/
```

```json
{ "mobile": "63-997-173-3576", "code": "1234" }
```

if the code matches servers code, then server returns token and refresh token.

## To Login

### Step 1, request SMS code

```
POST /auth/customer/mobile-request-login/
```

```json
{ "mobile": "639971733576" }
```

5 digit random number SMS code will be send to the mobile device.Server returns status 200, message = "SMS code send. please login within 10 minutes".

### Step 2, login using mobile

```
POST /auth/customer/mobile-login/
```

```json
{ "mobile": "63-997-173-3576", "code": "1234" }
```

if the mobile code matches, server returns

```json
{ token, refresh_token }
```

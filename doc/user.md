# User API Spec

## Register User

Endpoint : POST /api/users

Request Body :

```json
{
  "email" : "user@example.com",
  "password" : "yourpassword",
  "name" : "John Doe"
}
```

Response Body (Success) : 

```json
{
  "data" : {
    "email" : "user@example.com",
    "name" : "John Doe",
    "emailVerified": false
  }
}
```

Response Body (Failed) :

```json
{
  "errors" : "Email already registered"
}
```

## Login User

Endpoint : POST /api/users/login

Request Body :

```json
{
  "email" : "user@example.com",
  "password" : "yourpassword"
}
```

Response Body (Success) :

```json
{
  "data" : {
    "email" : "user@example.com",
    "name" : "John Doe",
    "token" : "jwt_token"
  }
}
```

Response Body (Failed) :

```json
{
  "errors" : "Email or password is incorrect"
}
```

## Verify Email

Endpoint : POST /api/users/verify-email

Request Body :

```json
{
  "email" : "user@example.com",
  "verificationCode" : "123456"
}
```

Response Body (Success) :

```json
{
  "data" : {
    "email": "user@example.com",
    "emailVerified": true
  }
}
```

Response Body (Failed) :

```json
{
  "errors" : "Invalid or expired verification code"
}
```

## Reset Password (Request Reset)

Endpoint : POST /api/users/reset-password/request

Request Body :

```json
{
  "email" : "user@example.com"
}
```

Response Body (Success) :

```json
{
  "message" : "Reset password link sent to your email"
}

```

Response Body (Failed) :

```json
{
  "errors" : "Email not found"
}
```

## Reset Password (Confirm Reset)

Endpoint : POST /api/users/reset-password/confirm

Request Body :

```json
{
  "resetToken" : "reset_token",
  "newPassword" : "newpassword"
}
```

Response Body (Success) :

```json
{
  "message" : "Password reset successfully"
}
```

Response Body (Failed) :

```json
{
  "errors" : "Invalid or expired reset token"
}
```

## Get User

Endpoint : GET /api/users/current

Headers :
- Authorization: Bearer jwt_token

Response Body (Success) :

```json
{
  "data" : {
    "email" : "user@example.com",
    "name" : "John Doe",
    "emailVerified": true
  }
}
```

Response Body (Failed) :

```json
{
  "errors" : "Unauthorized"
}
```

## Update User

Endpoint : PATCH /api/users/current

Headers :
- Authorization: Bearer jwt_token

Request Body :

```json
{
  "name" : "John Doe Updated", // optional
  "password" : "newpassword"   // optional
}

```

Response Body (Success) :

```json
{
  "data" : {
    "email" : "user@example.com",
    "name" : "John Doe Updated"
  }
}
```

## Logout User

Endpoint : DELETE /api/users/logout

Headers :
- Authorization: Bearer jwt_token

Response Body (Success) :

```json
{
  "message" : "User logged out successfully"
}
```

Response Body (Failed) :

```json
{
  "errors" : "Unauthorized"
}
```

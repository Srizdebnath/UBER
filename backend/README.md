# User Registration API Documentation

## Register User
Register a new user in the system.

**Endpoint:** `POST /users/register`

### Request Body
```json
{
    "fullname": {
        "firstname": "string", // minimum 3 characters
        "lastname": "string"   // optional, minimum 3 characters if provided
    },
    "email": "string",        // valid email format
    "password": "string"      // minimum 6 characters
}
```

### Validation Rules
- `firstname`: Required, minimum 3 characters
- `email`: Required, must be a valid email format
- `password`: Required, minimum 6 characters
- `lastname`: Optional, minimum 3 characters if provided

### Success Response
**Status Code:** 201 (Created)

```json
{
    "token": "jwt_token_string",
    "user": {
        "fullname": {
            "firstname": "string",
            "lastname": "string"
        },
        "email": "string",
        "_id": "string"
    }
}
```

### Error Responses

**Status Code:** 400 (Bad Request)
```json
{
    "errors": [
        {
            "msg": "Error message",
            "param": "field_name",
            "location": "body"
        }
    ]
}
```

Possible validation errors:
- Invalid Email
- First name must be at least 3 characters long
- Password must be at least 6 characters long
- All fields are required

### Notes
- The password is automatically hashed before storing in the database
- A JWT token is generated and returned upon successful registration
- The response includes both the authentication token and the user details 
## Login User
Authenticate a user and receive a JWT token.

**Endpoint:** `POST /users/login`

### Request Body
```json
{
    "email": "string",    // valid email format
    "password": "string"  // minimum 6 characters
}
```

### Validation Rules
- `email`: Required, must be a valid email format
- `password`: Required, minimum 6 characters

### Success Response
**Status Code:** 200 (OK)

```json
{
    "token": "jwt_token_string",
    "user": {
        "fullname": {
            "firstname": "string",
            "lastname": "string"
        },
        "email": "string",
        "_id": "string"
    }
}
```

### Error Responses

**Status Code:** 400 (Bad Request)
```json
{
    "errors": [
        {
            "msg": "Error message",
            "param": "field_name",
            "location": "body"
        }
    ]
}
```

**Status Code:** 401 (Unauthorized)
```json
{
    "message": "Invalid email or password"
}
```

Possible validation errors:
- Invalid Email
- Password must be at least 6 characters long

### Notes
- The JWT token is set as an HTTP-only cookie
- The response includes both the authentication token and the user details 

## Get User Profile
Retrieve the profile information of the authenticated user.

**Endpoint:** `GET /users/profile`

### Authentication
Requires a valid JWT token in the request header or cookie.

### Success Response
**Status Code:** 200 (OK)

```json
{
    "fullname": {
        "firstname": "string",
        "lastname": "string"
    },
    "email": "string",
    "_id": "string"
}
```

### Error Responses
**Status Code:** 401 (Unauthorized)
```json
{
    "message": "Authentication required"
}
```

## Logout User
Logout the currently authenticated user and invalidate their token.

**Endpoint:** `GET /users/logout`

### Authentication
Requires a valid JWT token in the request header or cookie.

### Success Response
**Status Code:** 200 (OK)
```json
{
    "message": "Logged out"
}
```

### Error Responses
**Status Code:** 401 (Unauthorized)
```json
{
    "message": "Authentication required"
}
```

### Notes
- Clears the authentication cookie
- Adds the token to a blacklist to prevent reuse

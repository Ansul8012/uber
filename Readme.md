# API Documentation

## Endpoint: `/users/register`

### Description
This endpoint is used to register a new user. It validates the input data, checks if the user already exists, hashes the password, and creates a new user in the database. Upon successful registration, it returns a JSON Web Token (JWT) and the user details.

### Method
`POST`

### Request Body
The request body should be in JSON format and include the following fields:

| Field               | Type   | Required | Description                                      |
|---------------------|--------|----------|--------------------------------------------------|
| `fullname.firstname`| String | Yes      | The first name of the user (minimum 3 characters). |
| `fullname.lastname` | String | No       | The last name of the user (minimum 3 characters). |
| `email`             | String | Yes      | The email address of the user (must be valid).    |
| `password`          | String | Yes      | The password of the user (minimum 6 characters). |

### Example Request
```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "password123"
}
```

### Responses

#### Success (201 Created)
- **Description**: User successfully registered.
- **Response Body**:
```json
{
  "token": "jwt-token-here",
  "user": {
    "_id": "user-id-here",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com",
    "socketId": null
  }
}
```

#### Error (400 Bad Request)
- **Description**: Validation errors or user already exists.
- **Response Body** (Validation Errors):
```json
{
  "errors": [
    {
      "msg": "Invalid Email",
      "param": "email",
      "location": "body"
    },
    {
      "msg": "First name must be at least 3 characters long",
      "param": "fullname.firstname",
      "location": "body"
    },
    {
      "msg": "Password must be at least 6 characters long",
      "param": "password",
      "location": "body"
    }
  ]
}
```

- **Response Body** (User Already Exists):
```json
{
  "message": "User already exist"
}
```

### Notes
- Ensure the `Content-Type` header is set to `application/json` in the request.
- The `token` returned in the response can be used for authentication in subsequent requests.
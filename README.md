# ntfy api docs
A simple document with documentation of the ntfy api

## Authentication
The API knows 2 different ways of authenticating.
1. Basic auth: `Basic base64(<username>:<password>)`
2. Bearer token: `Bearer <token>`

Either of these tokens are placed in the `Authorization` header

## Explanation
All endpoints described in this document should be prefixed with `http(s)://<domain>/v1`.
This is because it makes the document easier to read.

## Admin endpoints
These endpoints are only accessible for users with the admin role.

---

### GET /users
Gets all users including their ACL's.
#### Request body
```json
```
#### Response body (200 OK)
```json
[
  {
    "username": "string", 
    "role": "string",
    "grants": [
      {
        "topic": "string",
        "permission": "string"
      }
    ]
  }
]
```

### PUT /users
Creates a new user with assigned username, password and optionally tier.
#### Request body
```json
{
  "username": "string",
  "password": "string",
  "tier": "string"
}
```
#### Response body (200 OK)
```json
{
  "success": "bool"
}
```

### DELETE /users
Deletes the given user.
#### Request body
```json
{
  "username": "string"
}
```
#### Response body (200 OK)
```json
{
  "success": "bool"
}
```

---

### PUT | POST /users/access
Creates/updates ACL's for the given user.
#### Request body
```json
{
  "username": "string",
  "topic": "string",
  "permission": "string"
}
```
#### Response body (200 OK)
```json
{
  "success": "bool"
}
```

### DELETE /users/access
Deletes the given ACL for the given topic from the user.
This will also return a 200 even if the user is no longer has an ACL for that topic.
#### Request body
```json
{
  "username": "string",
  "topic": "string"
}
```
#### Response body (200 OK)
```json
{
  "success": "bool"
}
```

---

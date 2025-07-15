# API Testing Assignmen with CRUD Operations

*For each endpoint: name & method, request details, expected response, and status code. Two test cases per endpoint (positive + negative).*

---

## 1. List Users

**Endpoint:** `GET /api/users?page=2`

### Positive Test

* **Request**

  ```
  GET https://reqres.in/api/users?page=2
  ```
* **Expected Response (200 OK)**

  ```json
  {
    "page": 2,
    "per_page": 6,
    "total": 12,
    "total_pages": 2,
    "data": [ /* 6 user objects */ ],
    "support": { /* … */ }
  }
  ```
* **Status Code:** `200`

### Negative Test: Invalid Page Parameter

* **Request**

  ```
  GET https://reqres.in/api/users?page=abc
  ```
* **Expected Response (400 Bad Request)**

  ```json
  {
    "error": "Page must be a number"
  }
  ```
* **Status Code:** `400`

---

## 2. Single User

**Endpoint:** `GET /api/users/2`

### Positive Test

* **Request**

  ```
  GET https://reqres.in/api/users/2
  ```
* **Expected Response (200 OK)**

  ```json
  {
    "data": {
      "id": 2,
      "email": "janet.weaver@reqres.in",
      "first_name": "Janet",
      "last_name": "Weaver",
      "avatar": "https://..."
    },
    "support": { /* … */ }
  }
  ```
* **Status Code:** `200`

### Negative Test: User Not Found

* **Request**

  ```
  GET https://reqres.in/api/users/23
  ```
* **Expected Response (404 Not Found)**

  ```json
  {}
  ```
* **Status Code:** `404`

---

## 3. Create User

**Endpoint:** `POST /api/users`

### Positive Test

* **Request**

  ```
  POST https://reqres.in/api/users
  Content-Type: application/json

  {
    "name": "morpheus",
    "job": "leader"
  }
  ```
* **Expected Response (201 Created)**

  ```json
  {
    "name": "morpheus",
    "job": "leader",
    "id": "496",
    "createdAt": "2025-07-15T11:00:00.000Z"
  }
  ```
* **Status Code:** `201`

### Negative Test: Missing Field

* **Request**

  ```
  POST https://reqres.in/api/users
  Content-Type: application/json

  {
    "name": "morpheus"
  }
  ```
* **Expected Response (400 Bad Request)**

  ```json
  {
    "error": "Missing job field"
  }
  ```
* **Status Code:** `400`

---

## 4. Update User

**Endpoint:** `PUT /api/users/2`

### Positive Test

* **Request**

  ```
  PUT https://reqres.in/api/users/2
  Content-Type: application/json

  {
    "name": "neo",
    "job": "the one"
  }
  ```
* **Expected Response (200 OK)**

  ```json
  {
    "name": "neo",
    "job": "the one",
    "updatedAt": "2025-07-15T11:05:00.000Z"
  }
  ```
* **Status Code:** `200`

### Negative Test: Invalid ID Format

* **Request**

  ```
  PUT https://reqres.in/api/users/abc
  Content-Type: application/json

  {
    "name": "neo",
    "job": "the one"
  }
  ```
* **Expected Response (400 Bad Request)**

  ```json
  {
    "error": "User ID must be numeric"
  }
  ```
* **Status Code:** `400`

---

## 5. Delete User

**Endpoint:** `DELETE /api/users/2`

### Positive Test

* **Request**

  ```
  DELETE https://reqres.in/api/users/2
  ```
* **Expected Response:** *No body*
* **Status Code:** `204`

### Negative Test: Wrong Method

* **Request**

  ```
  GET https://reqres.in/api/users/2
  ```
* **Expected Response (405 Method Not Allowed)**

  ```json
  {
    "error": "DELETE method required"
  }
  ```
* **Status Code:** `405`

---

## 6. Register

**Endpoint:** `POST /api/register`

### Positive Test

* **Request**

  ```
  POST https://reqres.in/api/register
  Content-Type: application/json

  {
    "email": "eve.holt@reqres.in",
    "password": "pistol"
  }
  ```
* **Expected Response (200 OK)**

  ```json
  {
    "id": 4,
    "token": "QpwL5tke4Pnpja7X4"
  }
  ```
* **Status Code:** `200`

### Negative Test: Missing Password

* **Request**

  ```
  POST https://reqres.in/api/register
  Content-Type: application/json

  {
    "email": "sydney@fife"
  }
  ```
* **Expected Response (400 Bad Request)**

  ```json
  {
    "error": "Missing password"
  }
  ```
* **Status Code:** `400`

---

## 7. Login

**Endpoint:** `POST /api/login`

### Positive Test

* **Request**

  ```
  POST https://reqres.in/api/login
  Content-Type: application/json

  {
    "email": "eve.holt@reqres.in",
    "password": "cityslicka"
  }
  ```
* **Expected Response (200 OK)**

  ```json
  {
    "token": "QpwL5tke4Pnpja7X4"
  }
  ```
* **Status Code:** `200`

### Negative Test: Missing Email

* **Request**

  ```
  POST https://reqres.in/api/login
  Content-Type: application/json

  {
    "password": "cityslicka"
  }
  ```
* **Expected Response (400 Bad Request)**

  ```json
  {
    "error": "Missing email or username"
  }
  ```
* **Status Code:** `400`

---

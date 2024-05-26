# SKYGOALTECH API Server Guide

Welcome to the  SKYGOALTECH API Server guide! This README file will help you get started with running the server and testing its endpoints using Postman and cURL.

## Starting the Server

First, ensure the server is running by starting it from the terminal:

```sh
node app.js
```

## Using Postman to Test API Server

### Signup API Test

**Endpoint:** `POST /signup`

**URL:** `http://localhost:3000/signup`

**Headers:**

- `Content-Type: application/json`

**Body (raw JSON):**

```json
{
    "username": "teja",
    "password": "teja123"
}
```

**Steps:**

1. Create a new POST request.
2. Set the URL to `http://localhost:3000/signup`.
3. Under the **Headers** tab, set `Content-Type` to `application/json`.
4. In the **Body** tab, select `raw` and `JSON`, then paste the JSON body above.
5. Click **Send**.

**Expected Response:**

- **Status 200 OK:** `"User registered successfully"`
- **Status 500 Internal Server Error:** `"Error registering user"` (if there's an issue)

### Login API Test

**Endpoint:** `POST /login`

**URL:** `http://localhost:3000/login`

**Headers:**

- `Content-Type: application/json`

**Body (raw JSON):**

```json
{
    "username": "teja",
    "password": "teja123"
}
```

**Steps:**

1. Create a new POST request.
2. Set the URL to `http://localhost:3000/login`.
3. Under the **Headers** tab, set `Content-Type` to `application/json`.
4. In the **Body** tab, select `raw` and `JSON`, then paste the JSON body above.
5. Click **Send**.

**Expected Response:**

- **Status 200 OK:** `{ auth: true, token: <JWT token> }`
- **Status 404 Not Found:** `"User not found"`
- **Status 401 Unauthorized:** `"Invalid password"`
- **Status 500 Internal Server Error:** `"Error logging in"`

### User Details API Test

**Endpoint:** `GET /user`

**URL:** `http://localhost:3000/user`

**Headers:**

- `x-access-token: <JWT token from login response>`

**Steps:**

1. Create a new GET request.
2. Set the URL to `http://localhost:3000/user`.
3. Under the **Headers** tab, add a header `x-access-token` with the value set to the JWT token received from the login response.
4. Click **Send**.

**Expected Response:**

- **Status 200 OK:** user details
- **Status 403 Forbidden:** `"No token provided"`
- **Status 500 Internal Server Error:** `"Failed to authenticate token"`

## Using cURL

### Signup API Test

```sh
curl -X POST http://localhost:3000/signup \
-H "Content-Type: application/json" \
-d '{"username": "teja", "password": "teja123"}'
```

### Login API Test

```sh
curl -X POST http://localhost:3000/login \
-H "Content-Type: application/json" \
-d '{"username": "teja", "password": "teja123"}'
```

Note the JWT token received in the response.

### User Details API Test

```sh
curl -X GET http://localhost:3000/user \
-H "x-access-token: <JWT token from login response>"
```

## Summary of Steps

1. **Run Your Server:** Start the server with `node app.js`.
2. **Test Signup Endpoint:** Use Postman or cURL to send a POST request to `/signup` with the required payload.
3. **Test Login Endpoint:** Send a POST request to `/login` and capture the JWT token from the response.
4. **Test User Details Endpoint:** Send a GET request to `/user` with the `x-access-token` header set to the JWT token obtained from the login response.

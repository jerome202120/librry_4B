## API Documentation 

#### The Library API is designed for users to view and library administrators to manage books and authors. It provides endpoints for registering and authenticating users, as well as viewing, adding and modifying book information.

## ENDPOINTS
### 1. Register a New User
- **Method:** `POST`
- **Endpoint:** `/user/register`
- **Description:** Registers a new user by checking if the username is available and, if so, adds the user to the database.
- **Request Headers:** 
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `username` (string): Desired username for the new account.
  - `password` (string): Password for the new account.
- **Responses:**
  - **Success:** 
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "data": null }`
  - **Failure: Username Taken:** 
    - **Status:** `200 OK`
    - **Body:** `{ "status": "fail", "data": { "title": "Username already taken" } }`
  - **Failure: Database Error:** 
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "data": { "title": "<error message>" } }`


# API Documentation: User Authentication

## Endpoint Summary

### 2. Authenticate User
- **Method:** `POST`
- **Endpoint:** `/user/auth`
- **Description:** Authenticates a user by verifying their username and password. If authentication is successful, returns an access token.
- **Request Headers:** 
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `username` (string): The username of the user attempting to authenticate.
  - `password` (string): The password associated with the username.
- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<token>", "data": null }`
  - **Failure: Authentication Failed:** 
    - **Status:** `200 OK`
    - **Body:** `{ "status": "fail", "data": { "title": "Authentication Failed" } }`
  - **Failure: Database Error:** 
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "data": { "title": "<error message>" } }`


      # API Documentation: Show Users

## Endpoint Summary

### 3. Show Users
- **Method:** `GET`
- **Endpoint:** `/user/show`
- **Description:** Retrieves a list of all users. Requires an authorization token for access.
- **Request Headers:** 
  - `Authorization: Bearer <token>`
  - `Content-Type: application/json`
- **Request Body Parameters:** None

- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<new_token>", "data": [ { "user_id": "<user_id>", "username": "<username>" }, ... ] }`
  - **Failure: Missing Authorization Header:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Authorization header missing" } }`
  - **Failure: Invalid or Expired Token:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **Failure: Database Error:** 
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "message": "<error message>" }`


      # API Documentation: Update User

## Endpoint Summary

### 4. Update User
- **Method:** `PUT`
- **Endpoint:** `/user/update`
- **Description:** Updates the user's information, including username and password. Requires a valid authorization token, and the user can only update their own information.
- **Request Headers:** 
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token for the user.
  - `user_id` (integer): The ID of the user to be updated.
  - `username` (string): New username for the user.
  - `password` (string): New password for the user.

- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **Failure: Missing Token:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **Failure: Missing User ID:** 
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "User ID missing in payload" } }`
  - **Failure: Invalid or Expired Token:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **Failure: Unauthorized Action:** 
    - **Status:** `403 Forbidden`
    - **Body:** `{ "status": "fail", "data": { "title": "Unauthorized action" } }`
  - **Failure: Database Error:** 
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "data": { "title": "<error message>" } }`



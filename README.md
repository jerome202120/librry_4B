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


      # API Documentation: Delete User

## Endpoint Summary

### 5. Delete User
- **Method:** `DELETE`
- **Endpoint:** `/user/delete`
- **Description:** Deletes a user account. Requires a valid authorization token, and the user can only delete their own account.
- **Request Headers:** 
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token for the user.
  - `user_id` (integer): The ID of the user to be deleted.

- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "data": null }`
  - **Failure: Invalid JSON Payload:** 
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid JSON payload" } }`
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


      # API Documentation: Register Author

## Endpoint Summary

### 6. Register a New Author
- **Method:** `POST`
- **Endpoint:** `/author/register`
- **Description:** Registers a new author by checking if the author's name is unique and, if so, adds the author to the database. Requires a valid authorization token.
- **Request Headers:** 
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token for the user.
  - `name` (string): Name of the author to be registered.

- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **Failure: Missing Token:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **Failure: Missing Author Name:** 
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Name missing in payload" } }`
  - **Failure: Invalid or Expired Token:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **Failure: Author Name Already Taken:** 
    - **Status:** `200 OK`
    - **Body:** `{ "status": "fail", "data": { "title": "Author name already taken" } }`
  - **Failure: Database Error:** 
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "data": { "title": "<error message>" } }`


      # API Documentation: Show Authors

## Endpoint Summary

### 7. Show All Authors
- **Method:** `GET`
- **Endpoint:** `/author/show`
- **Description:** Retrieves a list of all registered authors. Requires a valid authorization token.
- **Request Headers:** 
  - `Authorization`: Bearer token required for access.

- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<new_token>", "data": [ { "author_id": "<id>", "name": "<name>" }, ... ] }`
  - **Failure: Missing Authorization Header:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Authorization header missing" } }`
  - **Failure: Invalid or Expired Token:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **Failure: No Authors Found:** 
    - **Status:** `200 OK`
    - **Body:** `{ "status": "fail", "message": "No authors found" }`
  - **Failure: Database Error:** 
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "message": "<error message>" }`


      # API Documentation: Update Author

## Endpoint Summary

### 8. Update Author
- **Method:** `PUT`
- **Endpoint:** `/author/update`
- **Description:** Updates an author’s name based on the provided author ID. Requires a valid authorization token.
- **Request Headers:** 
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token for the user.
  - `author_id` (integer): ID of the author to update.
  - `name` (string): New name of the author.

- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **Failure: Missing Token:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **Failure: Missing Author ID:** 
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Author ID missing in payload" } }`
  - **Failure: Invalid or Expired Token:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **Failure: Database Error:** 
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "data": { "title": "<error message>" } }`


      # API Documentation: Delete Author

## Endpoint Summary

### 9. Delete Author
- **Method:** `DELETE`
- **Endpoint:** `/author/delete`
- **Description:** Deletes an author based on the provided author ID. Requires a valid authorization token.
- **Request Headers:**
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token for the user.
  - `author_id` (integer): ID of the author to delete.

- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **Failure: Invalid JSON Payload:**
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid JSON payload" } }`
  - **Failure: Missing Token:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **Failure: Missing Author ID:** 
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Author ID missing in payload" } }`
  - **Failure: Invalid or Expired Token:** 
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **Failure: Database Error:** 
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "data": { "title": "<error message>" } }`


    # API Documentation: Register Book

## Endpoint Summary

### 10. Register Book
- **Method:** `POST`
- **Endpoint:** `/book/register`
- **Description:** Registers a new book in the database, linking it to a specified author. Requires a valid authorization token.
- **Request Headers:**
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token for the user.
  - `title` (string): Title of the book.
  - `author_id` (integer): ID of the author of the book.

- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **Failure: Token Missing:**
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **Failure: Title or Author ID Missing:**
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Title or Author ID missing in payload" } }`
  - **Failure: Invalid or Expired Token:**
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **Failure: Book Already Exists:**
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Book already exists" } }`
  - **Failure: Database Error:**
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "data": { "title": "<error message>" } }`


    # API Documentation: Show Books

## Endpoint Summary

### 11. Show Books
- **Method:** `GET`
- **Endpoint:** `/book/show`
- **Description:** Fetches a list of all books from the database. Requires a valid authorization token.
- **Request Headers:**
  - `Authorization: Bearer <token>` (Authorization header containing the bearer token)
- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<new_token>", "data": [{ "book_id": 1, "title": "Book Title", "author_id": 2 }, ...] }`
  - **Failure: Authorization Header Missing:**
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Authorization header missing" } }`
  - **Failure: Invalid or Expired Token:**
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **Failure: No Books Found:**
    - **Status:** `404 Not Found`
    - **Body:** `{ "status": "fail", "message": "No books found" }`
  - **Failure: Database Error:**
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "message": "<error message>" }`


    # API Documentation: Update Book

## Endpoint Summary

### 12. Update Book
- **Method:** `PUT`
- **Endpoint:** `/book/update`
- **Description:** Updates an existing book's title and author. Requires a valid authorization token and the book ID in the payload.
- **Request Payload:**
  - JSON body containing:
    - `token`: The authorization token (required)
    - `book_id`: The ID of the book to update (required)
    - `title`: The new title for the book (required)
    - `author_id`: The new author ID for the book (required)
- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **Failure: Token Missing in Payload:**
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **Failure: Book ID Missing in Payload:**
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Book ID missing in payload" } }`
  - **Failure: Invalid or Expired Token:**
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **Failure: Database Error:**
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "data": { "title": "<error message>" } }`


    # API Documentation: Delete Book

## Endpoint Summary

### 13. Delete Book
- **Method:** `DELETE`
- **Endpoint:** `/book/delete`
- **Description:** Deletes an existing book by its ID. Requires a valid authorization token and the book ID in the payload.
- **Request Payload:**
  - JSON body containing:
    - `token`: The authorization token (required)
    - `book_id`: The ID of the book to delete (required)
- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **Failure: Invalid JSON Payload:**
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid JSON payload" } }`
  - **Failure: Token Missing in Payload:**
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **Failure: Book ID Missing in Payload:**
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Book ID missing in payload" } }`
  - **Failure: Invalid or Expired Token:**
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **Failure: Database Error:**
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "data": { "title": "<error message>" } }`


    # API Documentation: Register Book Author Relationship

## Endpoint Summary

### 14. Register Book-Author Relationship
- **Method:** `POST`
- **Endpoint:** `/book_author/register`
- **Description:** Registers a relationship between a book and an author. The payload must include the book ID, author ID, and a valid authorization token.
- **Request Payload:**
  - JSON body containing:
    - `token`: The authorization token (required)
    - `book_id`: The ID of the book (required)
    - `author_id`: The ID of the author (required)
- **Responses:**
  - **Success:**
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **Failure: Token Missing in Payload:**
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **Failure: Book ID or Author ID Missing in Payload:**
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Book ID or Author ID missing in payload" } }`
  - **Failure: Invalid or Expired Token:**
    - **Status:** `401 Unauthorized`
    - **Body:** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **Failure: Book Author Relationship Already Exists:**
    - **Status:** `400 Bad Request`
    - **Body:** `{ "status": "fail", "data": { "title": "Book author relationship already exists" } }`
  - **Failure: Database Error:**
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "data": { "title": "<error message>" } }`
   

    ### 15. Update Book-Author Relationship
- **Method:** PUT
- **Endpoint:** /book_author/update
- **Description:** Updates a book-author relationship in the database based on the provided `collection_id`. The payload must include the `collection_id`, `book_id`, `author_id`, and a valid authorization token.
- **Request Payload:**
  - JSON body containing:
    - `token`: The authorization token (required)
    - `collection_id`: The ID of the book-author relationship to update (required)
    - `book_id`: The ID of the book (required)
    - `author_id`: The ID of the author (required)

- **Responses:**
  - **Success:**
    - **Status:** 200 OK
    - **Body:**
      ```json
      { 
        "status": "success", 
        "token": "<new_token>", 
        "data": null 
      }
      ```

  - **Failure: Token Missing in Payload:**
    - **Status:** 401 Unauthorized
    - **Body:**
      ```json
      {
        "status": "fail",
        "data": { "title": "Token missing in payload" }
      }
      ```

  - **Failure: Collection ID Missing in Payload:**
    - **Status:** 400 Bad Request
    - **Body:**
      ```json
      {
        "status": "fail",
        "data": { "title": "Collection ID missing in payload" }
      }
      ```

  - **Failure: Invalid or Expired Token:**
    - **Status:** 401 Unauthorized
    - **Body:**
      ```json
      {
        "status": "fail",
        "data": { "title": "Invalid or expired token" }
      }
      ```

  - **Failure: Database Error:**
    - **Status:** 500 Internal Server Error
    - **Body:**
      ```json
      {
        "status": "fail",
        "data": { "title": "<error message>" }
      }
      ```


      ### 16. Delete Book-Author Relationship
- **Method:** DELETE
- **Endpoint:** /book_author/delete
- **Description:** Deletes a book-author relationship from the database based on the provided `collection_id`. The payload must include the `collection_id` and a valid authorization token.
- **Request Payload:**
  - JSON body containing:
    - `token`: The authorization token (required)
    - `collection_id`: The ID of the book-author relationship to delete (required)

- **Responses:**
  - **Success:**
    - **Status:** 200 OK
    - **Body:**
      ```json
      { 
        "status": "success", 
        "token": "<new_token>", 
        "data": null 
      }
      ```

  - **Failure: Token Missing in Payload:**
    - **Status:** 401 Unauthorized
    - **Body:**
      ```json
      {
        "status": "fail",
        "data": { "title": "Token missing in payload" }
      }
      ```

  - **Failure: Collection ID Missing in Payload:**
    - **Status:** 400 Bad Request
    - **Body:**
      ```json
      {
        "status": "fail",
        "data": { "title": "Collection ID missing in payload" }
      }
      ```

  - **Failure: Invalid or Expired Token:**
    - **Status:** 401 Unauthorized
    - **Body:**
      ```json
      {
        "status": "fail",
        "data": { "title": "Invalid or expired token" }
      }
      ```

  - **Failure: Database Error:**
    - **Status:** 500 Internal Server Error
    - **Body:**
      ```json
      {
        "status": "fail",
        "data": { "title": "<error message>" }
      }
      ```

















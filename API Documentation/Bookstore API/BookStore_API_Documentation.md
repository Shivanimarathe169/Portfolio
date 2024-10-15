# BookStore API Documentation

## Base URL: https://api.bookstore.com/v1

## Authentication:

This API uses API Key for authentication. You can include the API key in the request header:

### Authorization: Bearer YOUR_API_KEY

## Endpoints

### 1. Books

#### Get All Books

- **URL:** /books
  
- **Method:** GET
  
- **Description:** Retrieve a list of all available books.
  
- **Query Parameters:**
  - page: (optional) Page number for pagination (default: 1)
  - limit: (optional) Number of books per page (default: 10)
  - genre: (optional) Filter by book genre (e.g., fiction, non-fiction, mystery)
  - author: (optional) Filter by author name
  
- **Response:**

    ```json
    {
    "page": 1,
    "limit": 10,
    "total_books": 100,
    "books": [
        {
        "id": 1,
        "title": "The Great Gatsby",
        "author": "F. Scott Fitzgerald",
        "genre": "Fiction",
        "price": 10.99,
        "stock": 20,
        "description": "A novel set in the 1920s about the mysterious Jay Gatsby.",
        "cover_image": "https://example.com/images/gatsby.jpg"
        },
        {
        "id": 2,
        "title": "1984",
        "author": "George Orwell",
        "genre": "Dystopian",
        "price": 12.99,
        "stock": 15,
        "description": "A dystopian novel about a totalitarian regime.",
        "cover_image": "https://example.com/images/1984.jpg"
        }
    ]
    }
    ```
#### Get Single Book by ID

- **URL:** /books/{book_id}
  
- **Method:** GET
  
- **Description:** Retrieve details of a specific book.
  
- **URL Parameters:**

  - book_id: The ID of the book to retrieve.

- **Response:**

    ```json
    {
    "id": 1,
    "title": "The Great Gatsby",
    "author": "F. Scott Fitzgerald",
    "genre": "Fiction",
    "price": 10.99,
    "stock": 20,
    "description": "A novel set in the 1920s about the mysterious Jay Gatsby.",
    "cover_image": "https://example.com/images/gatsby.jpg",
    "reviews": [
        {
        "user": "john_doe",
        "rating": 5,
        "comment": "One of the greatest books of all time."
        },
        {
        "user": "jane_doe",
        "rating": 4,
        "comment": "Great story, but the ending was a bit abrupt."
        }
    ]
    }
    ```

#### Create a New Book
  
- **URL:** /books
  
- **Method:** POST

- **Description:** Add a new book to the store.

- **Request Body:**

    ```json
    {
    "title": "The Catcher in the Rye",
    "author": "J.D. Salinger",
    "genre": "Fiction",
    "price": 8.99,
    "stock": 25,
    "description": "A story about a young man’s journey of self-discovery.",
    "cover_image": "https://example.com/images/catcher.jpg"
    }
    ```

- **Response:**

    ```json
    {
    "id": 3,
    "title": "The Catcher in the Rye",
    "author": "J.D. Salinger",
    "genre": "Fiction",
    "price": 8.99,
    "stock": 25,
    "description": "A story about a young man’s journey of self-discovery.",
    "cover_image": "https://example.com/images/catcher.jpg"
    }
    ```

#### Update a Book

**URL:**/books/{book_id}

**Method:** PUT

**Description:** Update the details of an existing book.

**URL Parameters:**
  - book_id: The ID of the book to update.

- **Request Body:**
  
    ```json
    {
    "price": 9.99,
    "stock": 30,
    "description": "Updated description of the book."
    }
    ```

- **Response:**

    ```json
    {
    "id": 1,
    "title": "The Great Gatsby",
    "author": "F. Scott Fitzgerald",
    "genre": "Fiction",
    "price": 9.99,
    "stock": 30,
    "description": "Updated description of the book.",
    "cover_image": "https://example.com/images/gatsby.jpg"
    }
    ```

#### Delete a Book

- **URL:** /books/{book_id}

- **Method:** DELETE

- **Description:** Remove a book from the store.

- **URL Parameters:**
  - book_id: The ID of the book to delete.

- **Response:**

    ```json
    {
    "message": "Book deleted successfully."
    }
    ```

### 2. Shopping Cart

#### Get Cart

- **URL:** /cart

- **Method:** GET

- **Description:** Retrieve the current user's shopping cart.

- **Response:**

    ```json
    {
    "cart": [
        {
        "book_id": 1,
        "title": "The Great Gatsby",
        "quantity": 1,
        "price": 10.99
        },
        {
        "book_id": 2,
        "title": "1984",
        "quantity": 2,
        "price": 12.99
        }
    ],
    "total": 36.97
    }
    ```

#### Add Book to Cart

- **URL:** /cart

- **Method:** POST
  
- **Description:** Add a book to the shopping cart.
  
- **Request Body:**

    ```json
    {
    "book_id": 3,
    "quantity": 1
    }
    ```

- **Response:**

    ```json
    {
    "message": "Book added to cart successfully."
    }
    ```

#### Update Cart

- **URL:** /cart/{book_id}
  
- **Method:** PUT

- **Description:** Update the quantity of a book in the shopping cart.

- **URL Parameters:**
  - book_id: The ID of the book to update.

- **Request Body:**

    ```json
    {
    "quantity": 3
    }
    ```

- **Response:**

    ```json
    {
    "message": "Cart updated successfully."
    }
    ```

#### Delete Book from Cart

- **URL:** /cart/{book_id}
  
- **Method: **DELETE
  
- **Description:** Remove a book from the shopping cart.
  
- **URL Parameters:**
  - book_id: The ID of the book to remove.

- **Response:**

    ```json
    {
    "message": "Book removed from cart successfully."
    }
    ```

### 3. Checkout

#### Checkout

- **URL:** /checkout

- **Method:** POST

- **Description:** Complete the purchase of items in the shopping cart.

- **Request Body:**

    ```json
    {
    "payment_method": "credit_card",
    "address": {
        "line1": "123 Main St",
        "city": "Springfield",
        "state": "IL",
        "postal_code": "62701"
    }
    }
    ```

- **Response:**

    ```json
    {
    "message": "Purchase completed successfully.",
    "order_id": 12345,
    "total_amount": 36.97
    }
    ```

### Error Responses
All error responses have the following structure:

- **Example Error Response:**

    ```json
    {
    "error": {
        "code": 400,
        "message": "Invalid request. Please check the request body or parameters."
    }
    }
    ```

- **Error Codes:**
  
  - **400:** Bad Request
  - **401:** Unauthorized (invalid API key)
  - **404:** Not Found
  - **500:** Internal Server Error

### Rate Limiting:

  - Max Requests per Minute: 1000 requests.

  - Response on Rate Limit Exceeded:
  
    ```json
    {
    "error": {
        "code": 429,
        "message": "Too many requests. Please try again later."
    }
    }
    ```

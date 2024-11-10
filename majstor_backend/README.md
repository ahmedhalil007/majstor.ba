# Majstor.ba Backend

This is a backend part of Majstor.ba application built with **Node.js**, **Express**, and **PostgreSQL**. The application provides a **RESTful API** for managing users, posts, comments, requests, contact information, and administrative tasks. The API is designed to handle HTTP requests from a frontend interface, performing **CRUD** operations and communicating with a PostgreSQL database to store and retrieve data. The backend is also configured with CORS to allow cross-origin requests.

**Table of Contents**

- Technologies
- Repository Structure
- Installation
- Database Setup
- Environment Configuration
- API Endpoints

**Technologies**

- Node.js - Server runtime
- Express.js - Web framework for handling HTTP requests
- PostgreSQL - Relational database management
- body-parser - Middleware to parse JSON request bodies
- CORS - Cross-Origin Resource Sharing configuration
- Additional Dependencies
- bcrypt - Library for hashing passwords securely.
- dotenv - Loads environment variables from a .env file for secure configuration management.
- jsonwebtoken - Used to create and verify JSON Web Tokens (JWT) for secure authentication.
- multer - Middleware for handling file uploads in the application.
- nodemailer - Module for sending emails, often used for notifications and account verification.
- nodemon - Development tool that automatically restarts the server on code changes.
- pg - PostgreSQL client for Node.js, used to interact with the PostgreSQL database.

**Repository Structure**
Here’s a breakdown of the main folders and files:

**app.js** is the main server file that configures middleware, routes, and static file directories, setting up the Express application to handle API requests. It also starts the server on port 8080 and manages all core functionalities for the backend.

**database.js** defines the database setup and table creation logic for a PostgreSQL database, including tables for users, posts, comments, requests, and login sessions, with checks to prevent recreating existing tables. It also exports a database connection pool to be used across the application.

**verifyToken.js** implements a middleware function, for authenticating JSON Web Tokens (JWT) in incoming requests. It checks for the presence of a token in the Authorization header, verifies it against a secret key, and ensures it hasn’t expired. If valid, the token's decoded payload is attached to the request object; otherwise, it responds with a 401 Unauthorized error.

**users** repositroy contains all the user-related functionalities and endpoints for handling actions such as registration, login, and profile management. The available endpoints include:

- POST /register: Registers a new user, saves their profile picture if provided, and sends a verification email.
- GET /verify: Verifies the user account with a token.
- POST /login: Logs in a user and generates a JWT token.
- GET /: Retrieves a list of all users.
- GET /by-token: Retrieves user data based on a JWT token (authorization required).
- PUT /: Updates user profile details, including their profile picture (authorization required).
- DELETE /: Deletes the user’s account (authorization required).
- POST /forgot-password: Initiates a password reset process.
- POST /change-password: Changes the user's password (authorization required).
- GET / : Retrieves a user by their ID.
  When a user registers, a verification email with a token is sent to confirm their account. Authorization, using JWT, is required for sensitive operations such as viewing user data by token, updating the profile, deleting the account and changing the password.

**posts** repository contains all the post-related functionalities and endpoints for managing posts, such as creating, updating, deleting, and retrieving posts. The available endpoints include:

- POST /create-post: Allows an authenticated user with the type "craftsman" to create a new post. This includes providing a title, service, content, price, and optional images of work. JWT authentication is required.
- GET /: Retrieves all posts from the database. No authentication is required for this endpoint,as it is publicly accessible. `Pagination`: The endpoint supports pagination via the `page` and `pageSize` query parameters as well as filtering by `service` and `location`. By default, page is set to 1, and pageSize is set to 10. The results are returned with a limit and offset based on these parameters, allowing clients to fetch posts in smaller, manageable chunks.
- PUT /update-post/ : Allows an authenticated user with the type "craftsman" to update an existing post by specifying the post ID. Only the "craftsman" who created the post is authorized to update it. This includes the option to upload new images. JWT authentication is required.
- DELETE /delete-post/ : Allows an authenticated user with the type "craftsman" to delete a post by specifying the post ID. Only the "craftsman" who created the post is authorized to delete it. JWT authentication is required.

The authentication and authorization system ensures that:

- Only users with a valid JWT token can perform actions such as creating, updating, or deleting posts.
- Only users with the type "craftsman" are authorized to create posts.
- Only the "craftsman" who created a specific post can update or delete that post.

**requests** folder handles all the functionality related to sending and managing requests for posts. Users can send requests, view their requests, and update the status of requests they’ve received. This system requires user authentication via JWT, with different permissions for clients and craftsmen. The available endpoints are:

Available Endpoints:

- POST /: Allows a client to send a request for a post. The client must be authenticated, and the post ID must be valid. Only users with the client user type can send requests.
- GET /userRequests: Retrieves all requests made by the authenticated user. For a client, it returns requests they have sent for posts. For a craftsman, it returns requests made by clients for their posts. This operation requires authentication.
- PUT /update-request-status: Allows a craftsman to update the status of a request (e.g., approve or deny a request) for their posts. Only the craftsman who created the post can update the request status for it. This operation requires authentication and authorization.
- GET /user-post: Retrieves a request by user ID and post ID. This allows a user to check if they have sent a request for a specific post. It requires authentication.

Authentication & Authorization:

- JWT Token: All endpoints require the user to be authenticated via a JWT token, passed in the request headers.
- User Types: The system distinguishes between clients (who can send requests) and craftsmen (who can manage and respond to requests for their posts). Only craftsmen can update request statuses and view requests related to their own posts.

**comments** folder manages the logic and routes for interacting with comments on posts. It allows users to leave comments, view comments for a specific post, and delete comments they have authored or that an admin has permission to delete.

Available Endpoints:

- POST /: Allows a client to leave a comment on a post. The comment must be related to a post the user has previously requested and has been approved. Additionally, a rating is provided alongside the comment. After posting, the request is deleted. This endpoint requires authentication.
- GET / : Retrieves all comments for a specific post, identified by its postId. The response includes the comment, user details (name, surname, profile picture), and the rating. No authentication is required for this endpoint.
- DELETE / : Allows a user to delete a comment they have authored. Admins can delete any comment, while regular users can only delete their own comments. This endpoint requires authentication.

Authentication & Authorization:

- JWT Token: All endpoints (except GET /:postId) require authentication via a JWT token passed in the request headers.
- User Types:
  Client: Can leave comments only on posts they have requested and been approved for. After posting the comment, the request is removed.
  Admin: Can delete any comment, regardless of ownership.
  User Ownership: A user can only delete their own comments unless they are an admin.

**customerSupport** folder is responsible for handling customer inquiries through a contact form. It uses Nodemailer to send messages to the support email when users submit their details (name, email, phone number, and message). This is a simple email-based communication flow for customer support.

Available Endpoints:

- POST /: This endpoint allows users to send a customer support message by providing their name, email, phone number, and a message. Upon submitting, an email is sent to the designated support email, and the user receives a success or error message.

**Installation**

- Clone the repository:
  `git clone <repository_url>`
  `cd <repository_folder>`

- Install dependencies:
  `npm install`

**Database Setup**
The application requires a PostgreSQL database. Follow these steps to set up the database:

- Create a PostgreSQL database and update the **config.js** file with your database connection details.
- The database schema includes tables for users, posts, ratings/comments, requests, and login sessions. The schema is automatically checked and created if not existing in the database.

**Environment Configuration**
Before running the application, create a **.env** file in the root directory and add the following environment variables:
`JWT_SECRET`: Secret key used for JSON Web Token (JWT) authentication.
`EMAIL_USER`: The email address used for sending support messages.
`EMAIL_PASS`: The password or application-specific password for the email address. Create 2-Step Versification password on your email acc and use it for `EMAIL_PASS`.

**Usage**
To start the application locally, run:
`npm start`

**API Endpoints**
All API Endpoints are avaliable within `Majstor.ba Copy.postman_collection`, import that file in your Postman application.

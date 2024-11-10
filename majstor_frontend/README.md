# Majstor.ba Frontend

This is the frontend application for the Majstor.ba, built with **React** and styled with **NextUI** and **Tailwind CSS**. It includes routing with `react-router-dom` and various pages for user and admin interfaces. The project is built with **Vite**, a fast and modern build tool that enhances development speed and optimizes performance.

**Installation**

1. Clone the Repository
   Clone the repository to your local machine:
   `git clone <repository_url>`
   `cd <repository_folder>`

2. Install Dependencies
   To install all required dependencies for the project, run:
   `npm install`

3. Start the Development Server
   Before you start Frontend application, make sure you have done all setup configuration for Backend application.
   To start the application locally, run the following command:
   `npm run dev`

**Key Features of the Frontend Application and Their Implementation**

**1. Communication with the Backend**
The frontend application communicates with the backend by sending HTTP requests using the Axios library. Axios simplifies sending GET, POST, PUT, and DELETE requests to the backend, and handles the responses that come back from the server.

**2. Craftsman Search**
The search component works by sending a request to the backend every time the user types a new letter. This process is known as "debouncing", which helps prevent sending too many requests in a short period and improves performance by only sending requests when necessary.

**3. Pagination**
Pagination is implemented by sending requests with page parameters (e.g., page=1) along with optional **filters such as service and location** to the backend. This allows the frontend to request data specific to a given page, service, and location, optimizing the results returned by the backend. The backend then returns only the relevant data for that particular page and filter combination, improving loading times and the overall performance of the application.

**User Authentication and Authorization**
When a user logs in successfully, the backend sends a **JWT token**, which is saved in the **localStorage** of the browser. This token is used for verifying the user during subsequent requests, allowing access to protected areas of the application based on the user's role (e.g., user, admin or craftsman).

**Repository Structure**
Here is a breakdown of the key folders and files in the project:

`src/`
`components/` - Contains reusable components like CustomNavbar, CustomFooter, etc.
`homePage/` - Contains the homepage components and logic.
`signup-login/` - Contains the signup, login, and reset password pages.
`userDetails/` - Contains the user details page.
`postDetails/` - Contains the post details page.
`admin/` - Contains the admin-related components like HomeAdmin, LoginAdmin, etc.
`aboutusPage/` - Contains information about the team as well as a contact form.
`App.jsx` - Main application component containing routes.
`index.css` - Global CSS styles.
`App.css` - Specific styles for the App component.

**Routing**
The application uses React Router (react-router-dom) for routing. Below are the key routes:

**Public Routes**:

- / - Home page
- /aboutUs - About us page
- /login - Login page
- /signUp - Signup page
- /resetPassword - Reset password page
- /userId/:userId - User details page
- /post/:postId - Post details page

**Admin Routes**:

- /loginadmin - Admin login page
- /homeadmin - Admin home page
- /admin/userId/:userId - Admin view of user details
- /admin/post/:postId - Admin view of post details

**Dependencies**
The application uses the following key libraries:

`react`: A JavaScript library for building user interfaces.
`@nextui-org/react`: A React UI kit that provides prebuilt components with a modern design.
`react-router-dom`: A library for handling routing in React applications.
`react-dom`: Provides DOM-specific methods for React, including the entry point for rendering the application.
`@fortawesome/fontawesome-free and @fortawesome/react-fontawesome`: Provides access to FontAwesome icons for React.
`axios`: Promise-based HTTP client used for making API requests.
`framer-motion`: Library for animations in React.
`jsonwebtoken`: Used for creating and verifying JSON Web Tokens, commonly used for authentication.
`react-router-dom`: For routing in React applications.
`sonner`: Used for creating notifications or toast messages.
`tailwindcss and postcss`: CSS utilities and preprocessors for styling.
`vite`: A modern build tool for fast development and bundling.
`eslint`: A tool for identifying and reporting on patterns in JavaScript, ensuring code quality.
`cypress`: End-to-end testing framework.

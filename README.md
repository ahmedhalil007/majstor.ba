# Majstor.ba

The "Majstor.ba" web application is designed to connect clients in need of craftsmen's services with skilled craftsmen who offer their expertise. The platform will provide a user-friendly
experience, offering a space for craftsmen to showcase their work and clients to easily find
the right professional for their needs as well as the rating system.

This project is done using React for frontend, Node.js for backend and PostgreSQL database. It implements a RESTful API, allowing the user interface to send requests to the server side of the application, which communicates with the database.

**Tech Stack**

- Frontend: React, Vite, NextUI, Tailwind CSS
- Backend: Node.js, Express.js
- Database: PostgreSQL
- Database Management: DBeaver Community
- Authentication: JSON Web Tokens (JWT)
- Testing: Cypress

**User Classes and Characteristics**

- Client: The client is a person or company that uses the Majstor.ba website to find and engage skilled professionals.
- Craftsmen: A craftsman is a specialist who offers services on the Majstor.ba platform.
- Admin: The admin has responsibility for managing the Majstor.ba platform.

**Requirements**

- User Profile Creation: Registration for two types of user profiles: craftsman and client.
- Authentication System: Log in to the website using a username and password.
- Authorization:Craftsman profile required for creating post, client profile required for to request a service and leave a review and admin profile for managing application.
- Customer Support: Based on sending email using Majstor.ba web application.
- Search System (pagination on server side): Searching(by name) and filtering (by profession and location) in order to find craftsmen.
- Reviews and Ratings System: After the craftsman completes the work required of him, the user has the option to rewiev and rate the craftsman by awarding him 1 to 5 stars. The system should calculate the rating of the craftsmen according to the number of stars. The user can see the average rating (from other users) of the craftsman on craftsman’s profile.
- Admin Panel: Management of the complete system (deleting profiles, posts or comments).

The complete setup and more details about requirements and ipmlementation can be found in the README files within both the backend and frontend repositories.

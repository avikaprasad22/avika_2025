---
layout: page
title: My 5 Accomplishments + Cart Feature  
permalink: /final/
---

<h3>Five Accomplishments Over 12 Weeks:</h3>

<b>1. Frontend Development & UI Design</b> - Built an interactive book store interface using HTML, CSS, and JavaScript, ensuring a smooth shopping experience with book tiles, a shopping cart, and quantity controls.

<b>2. Backend API Implementation</b> - Created RESTful API endpoints using Flask to handle CRUD operations for the shopping cart, ensuring users could add, update, and delete cart items.

<b>3. Database Integration & Management</b> - Developed a relational database with SQLAlchemy, setting up proper table relationships between books, users, and cart items.

<b>4. User Authentication & Security</b> - Implemented JWT-based authentication to restrict access to cart operations, ensuring only authenticated users could modify their carts.

<b>5. Team Collaboration & Strategic Designing</b> - To get rid of isolated features and mismatched style themes, full team collaboration and idea-sharing was an essential skill acquired. This allowed the team to create a cohesive and user-friendly interface using strateized CSS for a more put-together UI.

<h3>Issues Encountered:</h3>

Frontend-Backend Integration Challenges: Faced difficulties in ensuring API calls properly fetched and updated data between the frontend and backend.

Database Integrity Errors: Encountered foreign key constraints when linking cart items to books and users, requiring debugging and better data handling.

Authentication Issues: JWT authorization initially failed due to misconfigured request headers, which required debugging authentication middleware.

<h2>Building an Interactive Book Store: A Full-Stack Development Journey</h2>

<h4> In this project, I developed an online bookstore where users can browse books, add them to a cart, and manage their purchases. This involved building a responsive frontend, a secure backend API, and integrating a relational database to store cart data efficiently. </h4>

<b>Key Features</b>

- <b>Book Display & Shopping Cart:</b> Users can view book covers, adjust quantities, and add items to a cart dynamically.

- <b>Secure Transactions:</b> Using JWT authentication, users can safely add and remove items from their carts.

- <b>Database-Backed Operations:</b> A relational database maintains user purchases, ensuring data persistence.

- <b>Real-Time Updates:</b> The frontend dynamically fetches and updates the cart contents without requiring page reloads.

<b>Technical Implementation</b>

The backend, built using Flask, provides RESTful API endpoints for cart operations, handling requests using proper HTTP methods (GET, POST, PUT, DELETE). The database, managed with SQLAlchemy, establishes relationships between books, users, and cart items, ensuring data integrity.
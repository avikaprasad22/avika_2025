---
layout: page
title: My 5 Accomplishments + Cart Feature  
permalink: /final/
---

<h3>Five Accomplishments Over 12 Weeks:</h3>

<b>1. Frontend Development & UI Design</b> - I built an interactive book store interface using HTML, CSS, and JavaScript, ensuring a smooth shopping experience with book tiles, a shopping cart, and quantity controls.

<b>2. Backend API Implementation</b> - I created RESTful API endpoints using Flask to handle CRUD operations for the shopping cart, ensuring users could add, update, and delete cart items.

<b>3. Database Integration & Management</b> - Developed a relational database with SQLAlchemy, setting up proper table relationships between books, users, and cart items.

<b>4. User Authentication & Security</b> - Implemented JWT-based authentication to restrict access to cart operations, ensuring only authenticated users could modify their carts.

<b>5. Team Collaboration & Strategic Designing</b> - To get rid of isolated features and mismatched style themes, full team collaboration and idea-sharing was an essential skill acquired. This allowed the team to create a cohesive and user-friendly interface using strategized CSS for a more put-together UI.

<h3>Issues Encountered:</h3>

<b>Frontend-Backend Integration Challenges:</b> Faced difficulties in ensuring API calls properly fetched and updated data between the frontend and backend.

<b>Database Integrity Errors:</b> Encountered foreign key constraints when linking cart items to books and users, requiring debugging and better data handling.

<b>Authentication Issues:</b> JWT authorization initially failed due to misconfigured request headers, which required debugging authentication middleware.

<h2>Building an Interactive Book Store: A Full-Stack Development Journey</h2>

<h4> In this project, I developed an online bookstore where users can browse books, add them to a cart, and manage their purchases. This involved building a responsive frontend, a secure backend API, and integrating a relational database to store cart data efficiently. </h4>

<b>Key Features</b>

- <b>Book Display & Shopping Cart:</b> Users can view book covers, adjust quantities, and add items to a cart dynamically.

- <b>Secure Operating:</b> Using JWT authentication, users can safely add and remove items from their carts.

- <b>Database-Backed Operations:</b> A relational database maintains user purchases, ensuring data persistence.

Examples:

<code> 
    # 1. Get all items in the cart (R)

    @bookpurchase_api.route('/cart', methods=['GET'])

    @token_required()

    def get_cart():
        """Fetch all items in the cart along with total price and quantity."""
        items = CartItem.query.all()
        total_items = sum(item.quantity for item in items)
        total_price = sum(item.price * item.quantity for item in items)

    return jsonify({
        "items": [item.read() for item in items],  # Use read method from CartItem
        "total_items": total_items,
        "total_price": round(total_price, 2)
    })
</code>

<code>
    # 2. Add an item to the cart (C)

    @bookpurchase_api.route('/cart', methods=['POST'])

    @token_required()

    def add_to_cart():
        """Add a new item to the cart or update the quantity if it already exists."""
        data = request.get_json()

    # Validate input data
    if not all(k in data for k in ('id', 'title', 'price', 'quantity', '_name')):
        return jsonify({"error": "All fields (id, title, price, quantity, _name) are required."}), 400

    # Check if item already exists in the cart
    item = CartItem.query.get(data['id'])
    if item:
        # If item exists, update quantity
        item.quantity += data['quantity']
    else:
        # Create a new cart item
        item = CartItem(
            id=data['id'],
            title=data['title'],
            price=data['price'],
            quantity=data['quantity'],
            username=data['_name']
        )
        db.session.add(item)

    # Save changes to the database
    db.session.commit()
    return jsonify({"message": "Item added to cart successfully."}), 201
</code>

- <b>Real-Time Updates:</b> The frontend dynamically fetches and updates the cart contents without requiring page reloads.

<b>Technical Implementation</b>

The backend, built using Flask, provides RESTful API endpoints for cart operations, handling requests using proper HTTP methods (GET, POST, PUT, DELETE). The database, managed with SQLAlchemy, establishes relationships between books, users, and cart items, ensuring data integrity.

## N@tM
<img src="{{site.baseurl}}/images/n@tm.png">

## 2020 AP CSP MC - Test Corrections

Here are some questions from the MC that I reflected back on:

## Question 9
<img src="{{site.baseurl}}/images/mc1.png">
<b>Mistake:</b> The binary RGB triplet for vivid yellow is (11111111, 11111111, 00001110).
<br>
<b>Correct Answer: A</b> The binary number 11111111 is equal to, or 255. The binary number 11110000 is equal to, or 240. Therefore, the given binary triplet represents the color ivory.

<br>

## Question 20
<img src="{{site.baseurl}}/images/mc2.png">
<b>Mistake:</b> Incorrect. The two line graphs are roughly the same shape, indicating that the average amount of data stored per user remained about the same across all eight years.The answer choice I selected, gives an equal chance of selection to all three colors even though red is 4x larger.
<br>
<b>Correct Answer: A</b> The two line graphs are roughly the same shape. Each value on the right line graph is about 10 times the corresponding value on the left line graph. Therefore, the average amount of data stored per user is about 10 GB.

<br>

## Question 23
<img src="{{site.baseurl}}/images/mc3.png">
<b>Mistake:</b> Incorrect. Statement I is false. The Internet is not controlled from a central device.
<br>
<b>Correct Answer:</b> Correct. Statement I is false. The Internet is not controlled from a central device. Statements II and III are true. The Internet uses redundant routing to support fault tolerance. The Internet uses protocols so that data is transmitted in a standard format.

<br>

## Question 27
<img src="{{site.baseurl}}/images/mc4.png">
<b>Mistake:</b> The answer choice I selected, proposes two ways to get from P to S. For example, P to R to S and P to Q to S. This makes redundancy possible.
<br>
<b>Correct Answer:</b> The correct answer is B as redundant routing is impossible if there is only one possible path from one device to another. There is only one possible path from P to S (P to R to Q to S).

<br>

## Assessment of Performance
<img src="{{site.baseurl}}/images/assess.png">

## What I learned
Through this collegeboard MC, I learned many new concepts such as internet protocols and many cryptography methods and its applications. I thought those questions were interesting.

## What I need to improve on
After taking the collegeboard MC, I need to improve on the time I spend on each question, and therefore I have to get faster the questions that require you to test out the logic. These were like moving the robot kind of questions. They had tricky things hidden in the code that I sometimes missed as I was trying to not take too long on any question.

## Self Grade:

<img src="{{site.baseurl}}/images/grades.png">

| Category | Grade | Points | Explanation |
|---|---|---|---|
| 5 things in 12 weeks | 5 | 5 | I believe I earned a full score in this category because of my hard work over the course of the trimester. Not only did I learn a lot over the course of these weeks about APIs, frontend to backend integration, collaboration, and deployment, I also achieved a significant amount of what I set out to do, set and met reasonable goals, and asked for help when needed. |
| Full Stack Project Demo (CPT Requirements, N@tM) | 1.95 | 2 | I know my code very well and can explain it using proper vocabulary, so I can give an in-depth demo of my feature. My code also fulfills all of the CPT requirements thoroughly and in a solid manner, often fulfilling requirements multiple times over. I  find that my code demonstrates a solid knowledge of CollegeBoard’s cirriculum. My N@tM experience was also very positive, and I was able to talk to several people about my project and receive feedback from them. However, I find there is always room for improvement, and if I were to do this project over, I would find more and more inventive ways to implement CB requirements. |
| Project Feature blog Write-up | 1 | 1 | My write-up is thorough and explains both how my feature fulfills CPT requirements and is useful to my group’s project overall. |
| MCQ | 0.95 | 1 | Although I did not earn a full score in my MCQ, I performed better than my last MCQ test and overall felt like I understood more. I also took the time afterward to take a look at my analytics and take note on what questions I missed, and I wrote a detailed reflection afterward. |
| Total | 8.9 | 9 | |


For our website, I had a strong start on the frontend, but I was lacking integration with backend which is reflected in the 2nd plan, 1st code grade. After accomplishing a cohesive frotend, I shifted my focus a lot more toward backend First, I accomplished CRUD functionalities (GET, POST, DELTE, and UPDATE). After many successful entries through postman, I was able to integrate the CRUD with a UI and some javascript. Greater advancements were made to the UI more a more user-friendly interpreation of a shopping cart, and I implemnted authentication, which prevented anyone of the site from being able to access cart items or add/remoeve them. There is always more improvements to make, but through my progress on my feature, my collborative efforts, and learning from each live review and implementing the lessons learned, I believe that I should get an overall grade of <b>9.3 out of 10 on this final</b>. 

10th Point: <b>(0.4/1)</b>
- I reviewed other's projects at N@tM.
- I talked about my individual strengths and weaknesses over the 12 weeks.
- I had a retrspective on my project next steps plans and burn downs based on strengths and weaknesses.
- Included a summary of honest self grade.
---
layout: page
title: Sprint 5 - CRUD + more! 
permalink: /sprint5/
---

<h3> <b> Purpose of Bookworms: </b> </h3>
<h4> Bookworms is a platform for book lovers where they can use a variety of features such as a random book recommender, provide comments on their favorite books, post their book thoughts, access a book store, and more! </h4>

<h3> <b>  Individual Purpose: </b>  </h3>
<h4> The purpose of my feature is to provide the user with an interface where they can keep track of the books they want to shop for in a shopping cart. To make my feature possible, I employ CRUD methods to post items added to the cart and give the user an option to clear their cart once they’ve purchased all the ones they wanted.
 </h4>

<h3> <b>  Input/Output Requests:  </b> </h3>
<h4> My frontend sends a fetch request to my API to grab the books that have been statically put into the cart and display them on the frontend:
 </h4>

<code> 
const pythonURI = 'http://127.0.0.1:8887/api'; // Replace with your actual API URL

        // Fetch and display cart items
        function fetchCartItems() {
            fetch(`${pythonURI}/cart`)
            .then(response => response.json())
            .then(data => {
       const cartItemsContainer = document.getElementById('cartItems');
       cartItemsContainer.innerHTML = ''; // Clear current items


       if (data.items && data.items.length > 0) {
         data.items.forEach(item => {
           const cartItemDiv = document.createElement('div');
           cartItemDiv.classList.add('cart-item');
           cartItemDiv.innerHTML = `
             <span>${item.title} (by ${item.author || 'Unknown'})</span>
             <span>Price: $${item.price} | Quantity: ${item.quantity}</span>
           `;
           cartItemsContainer.appendChild(cartItemDiv);
         });
       } else {
         cartItemsContainer.innerHTML = '<p>Your cart is empty.</p>';
       }
     })
     .catch(error => {
       console.error('Error fetching cart items:', error);
     });
 }


<h3> <b>  CRUD Methods on Postman:  </b> </h3>

<h4> <b>  GET:  </b> </h4>
<img src="{{site.baseurl}}/images/get.png">

<code> 
    # 1. Get all items in the cart (R)
    
    @bookpurchase_api.route('/cart', methods=['GET'])
    def get_cart():
        """Fetch all items in the cart along with total price and quantity."""
        items = CartItem.query.all()
        total_items = sum(item.quantity for item in items)
        total_price = sum(item.price * item.quantity for item in items)

        return jsonify({
            "items": [item.read() for item in items],  # Use `read` method from CartItem
            "total_items": total_items,
            "total_price": round(total_price, 2)
    })


<h4> <b>  POST:  </b> </h4>
<img src="{{site.baseurl}}/images/post.png">
<img src="{{site.baseurl}}/images/postdb.png">

<code> 
    # 2. Add an item to the cart (C)

    @bookpurchase_api.route('/cart', methods=['POST'])
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


<h4> <b>  UPDATE:  </b> </h4>
<img src="{{site.baseurl}}/images/update.png">
<img src="{{site.baseurl}}/images/updatedb.png">

<code> 
    # 3. Update an item's quantity in the cart (U)

    @bookpurchase_api.route('/cart/<int:item_id>', methods=['PUT'])
    def update_cart_item(item_id):

    """Update the quantity of a specific item in the cart."""
    data = request.get_json()

    # Ensure quantity is provided
    if 'quantity' not in data:
        return jsonify({"error": "Quantity is required."}), 400

    # Fetch the item from the cart
    item = CartItem.query.get(item_id)
    if not item:
        return jsonify({"error": "Item not found in the cart."}), 404

    # Ensure the quantity is valid
    if data['quantity'] <= 0:
        return jsonify({"error": "Quantity must be greater than zero."}), 400

    # Update the quantity
    item.quantity = data['quantity']
    db.session.commit()
    return jsonify({"message": "Item quantity updated successfully."})


<h4> <b>  DELETE (can do individual and all):  </b> </h4>
<h4> <b>  Individual:  </b> </h4>
<img src="{{site.baseurl}}/images/ind_delete.png">
<img src="{{site.baseurl}}/images/ind_deletedb.png">

<code>
    # 4. Remove an item from the cart (D)
    @bookpurchase_api.route('/cart/<int:item_id>', methods=['DELETE'])

    def delete_cart_item(item_id):
        """Remove a specific item from the cart."""
    # Fetch the item by ID
        item = CartItem.query.get(item_id)
    if not item:
        return jsonify({"error": "Item not found in the cart."}), 404

    # Delete the item
    db.session.delete(item)
    db.session.commit()
    return jsonify({"message": "Item removed from cart successfully."})


<h4> <b>  All:  </b> </h4>
<img src="{{site.baseurl}}/images/delete.png">
<img src="{{site.baseurl}}/images/deletedb.png">

<code>
    # 5. Clear the entire cart

    @bookpurchase_api.route('/cart', methods=['DELETE'])

    def clear_cart():
        """Clear all items from the cart."""
    # Delete all rows in the CartItem table
        CartItem.query.delete()
        db.session.commit()
        return jsonify({"message": "Cart cleared successfully."})


<h3> <b>  Lists, Dictionaries, and Database  </b> </h3>

<h4> <b>Formatting response data (JSON) from API into DOM: </b> </h4>

<code>
// Fetch and display cart items
  
    function fetchCartItems() {
        fetch(`${pythonURI}/cart`)
        .then(response => response.json()) #convert response to JSON
        .then(data => { 
        const cartItemsContainer = document.getElementById('cartItems');
        cartItemsContainer.innerHTML = ''; // Clear current items

        if (data.items && data.items.length > 0) {
          data.items.forEach(item => {
            const cartItemDiv = document.createElement('div');
            cartItemDiv.classList.add('cart-item');
            cartItemDiv.innerHTML = `
              <span>${item.title} (by ${item.author || 'Unknown'})</span>
              <span>Price: $${item.price} | Quantity: ${item.quantity}</span>
            `;
            cartItemsContainer.appendChild(cartItemDiv);
          });
        } else {
          cartItemsContainer.innerHTML = '<p>Your cart is empty.</p>';
        }
      })
      .catch(error => {
        console.error('Error fetching cart items:', error);
      });
  }


✅ Fetch JSON from API
<br>
✅ Convert JSON to JavaScript objects
<br>
✅ Loop through data & create HTML elements
<br>
✅ Insert formatted data into the DOM dynamically
<br>
✅ Handle empty cart & errors gracefully

<h4> <b>Extracting A Python List </b> </h4>
<code>
@bookpurchase_api.route('/cart', methods=['GET'])

    def get_cart():
        """Fetch all items in the cart along with total price and quantity."""
        items = CartItem.query.all()
        total_items = sum(item.quantity for item in items)
        total_price = sum(item.price * item.quantity for item in items)

    return jsonify({
        "items": [item.read() for item in items],  # Use `read` method from CartItem
        "total_items": total_items,
        "total_price": round(total_price, 2)
    })


✅ Here, <b>cart_items</b> is a python <b>list</b> of <b>dictionaries</b>
<br>
✅ The <b>jsonify()</b> function converts it into a JSON response.

<h3> <b>  Algorithmic Code Request  </b> </h3>

<code>
    # Blueprint setup for the book purchase API

    bookpurchase_api = Blueprint('bookpurchase_api', __name__, url_prefix='/api')
    api = Api(bookpurchase_api)

    # 1. Get all items in the cart (R)
    @bookpurchase_api.route('/cart', methods=['GET'])
    def get_cart():
        """Fetch all items in the cart along with total price and quantity."""
        items = CartItem.query.all()
        total_items = sum(item.quantity for item in items)
        total_price = sum(item.price * item.quantity for item in items)

    return jsonify({
        "items": [item.read() for item in items],  # Use `read` method from CartItem
        "total_items": total_items,
        "total_price": round(total_price, 2)
    })


    # 2. Add an item to the cart (C)
    
    @bookpurchase_api.route('/cart', methods=['POST'])
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


    # 3. Update an item's quantity in the cart (U)

    @bookpurchase_api.route('/cart/<int:item_id>', methods=['PUT'])
        def update_cart_item(item_id):
        """Update the quantity of a specific item in the cart."""
            data = request.get_json()

    # Ensure quantity is provided
    if 'quantity' not in data:
        return jsonify({"error": "Quantity is required."}), 400

    # Fetch the item from the cart
    item = CartItem.query.get(item_id)
    if not item:
        return jsonify({"error": "Item not found in the cart."}), 404

    # Ensure the quantity is valid
    if data['quantity'] <= 0:
        return jsonify({"error": "Quantity must be greater than zero."}), 400

    # Update the quantity
    item.quantity = data['quantity']
    db.session.commit()
    return jsonify({"message": "Item quantity updated successfully."})


    # 4. Remove an item from the cart (D)
    @bookpurchase_api.route('/cart/<int:item_id>', methods=['DELETE'])
    def delete_cart_item(item_id):
        """Remove a specific item from the cart."""
        # Fetch the item by ID
        item = CartItem.query.get(item_id)
    if not item:
        return jsonify({"error": "Item not found in the cart."}), 404

    # Delete the item
    db.session.delete(item)
    db.session.commit()
    return jsonify({"message": "Item removed from cart successfully."})

    # 5. Clear the entire cart
    @bookpurchase_api.route('/cart', methods=['DELETE'])
    def clear_cart():
        """Clear all items from the cart."""
     # Delete all rows in the CartItem table
        CartItem.query.delete()
        db.session.commit()
        return jsonify({"message": "Cart cleared successfully."})


✅ The API is defined using <b>Flask’s Blueprint</b>
<br>
✅ <b>Sequencing:</b> Step-by-step execution of <code>query.all()</code>, calculations, and jsonify() response.
<br>
✅ <b>Iteration:</b> Uses list comprehensions (<code>sum(), [item.read() for item in items])</code> to iterate over items.
<br>
✅ <b>Selection:</b> <code>CartItem.query.all()</code> and <code>CartItem.query.get(item_id)</code> retreive specific data from the database.
<br>
✅ Formats and returns data as <b>JSON</b> using <code>josonify()</code>

<h3> <b> Call To Algorithm Request  </b> </h3>

<code> 
const pythonURI = 'http://127.0.0.1:8887/api';

    fetch(`${pythonURI}/cart`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data)
      })
        .then(response => response.json())
        .then(data => {
          alert(data.message || 'Book added to cart!');
          fetchCartItems(); // Refresh cart items
        })
        .catch(error => {
          console.error('Error adding book to cart:', error);
        });
    } else {
      alert('Please fill out all fields before adding the book to the cart.');
    }
  }

<h4> <b>Call/Request (fetching an endpoint) </b> </h4>

The given <code>fetch()</code> request is used to send a POST request to the Flask API endpoint <code>${pythonURI}/cart</code> to add a book to the cart.

<h4> <b>Response/Error Handling</b> </h4>
After sending the request, the API processes the data and sends a response back. The response is handled in the <code>.then(response => response.json())</code> block.
<br>
Missing Fields (400 Bad Request): <code>{ "error": "All fields (id, title, price, quantity, _name) are required." }</code>

<center>
<img src="{{site.baseurl}}/images/thanks_for_reading.gif">
</center>
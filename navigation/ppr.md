---
layout: page
title: Avika's Personalized Project Reference 
permalink: /ppr/
---
## A code segment procedure that:
- Defines the procedure's name and return type (if necessary)
- Contains and uses one or more parameters that have an effect on the functionality of the procedure
- Implements an algorithm that includes sequencing, selection and iteration

<img src="{{site.baseurl}}/images/ppr1.png">

The function <code>delete_cart_item</code> defines its name and takes an <code>item_id</code> parameter and returns a JSON response.

It uses <code>item_id</code> as a parameter to fetch a specific cart item, affecting functionality by determining which item to delete. 

- <b>Sequencing:</b> Follows an order of fetching, checking, deleting, and committing changes
<br>
- <b>Selection:</b> Checking if the item exists before deleting
<br>
- <b>Iteration:</b> Looping through the cart items to find the item to delete.

Another prominent example of iteration using a for loop:

<img src="{{site.baseurl}}/images/for_loop_ex.png">

## A code segment where the procedure is being called in my program:
<img src="{{site.baseurl}}/images/ppr2.png">

The JavaScript function <code>deleteCartItem</code> calls the <code>delete_cart_item</code> function from the Python backend by making a <code>DELETE</code> request to the appropriate API endpoint <code>(/api/cart/${itemId})</code>.

## A code segment must showing how data has been stored in the list:
<img src="{{site.baseurl}}/images/ppr3.png">

<code>init_books_in_cart() </code> function is called to initialize the cart with a list of books.

## A code segment must showing how data has been stored in the list:

An example of data being stored in a list is in the <code>get_cart function</code>. Here, <code>items</code> in the list are used to fulfill many feature purposes using <b>list comprehension</b>.

<img src="{{site.baseurl}}/images/ppr4.png"> 

First, using the items defined in the list above, <code>total_items = sum(item.quantity for item in items)</code> calculates the total quantity of items.

Second, using the same list, it calculates the total price: <code>total_price = sum(item.price * item.quantity for item in items)</code>

Here, <code>CartItem.query.all()</code> retrieves all cart items from the database, and the list comprehension <code>[item.read() for item in items]</code> stores each item's data (processed through the read() method) in a list before returning it as a JSON response.

<script src="https://utteranc.es/client.js"
        repo="nighthawkcoders/portfolio_2025"
        issue-term="title"
        label="blogpost-comment"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
# Step 6 Order Submission and Processing

## Overview
Now that our order modal forms are filled with data, our next step is to work on saving this data. In the process, the `orders` and `order_items` tables will be used to save or submit the customer's order details.

## Code for Saving Orders

### Update `routes.py`
Navigate to your `routes.py` file and add the following function to handle order submissions.

```python
# Orders
@app.route('/submit_order', methods=['POST'])
def submit_order():
    cursor = mysql.connection.cursor()
    
    try:
        # Extract data from the form
        product_id = int(request.form['productId'])
        quantity = float(request.form['quantity'])
        total_price = float(request.form['totalPrice'])
        mobile_number = request.form['mobileNumber']
        
        # Insert into orders table
        order_query = "INSERT INTO orders (total_price, customer_contact) VALUES (%s, %s)"
        cursor.execute(order_query, (total_price, mobile_number))
        order_id = cursor.connection.insert_id()  # Get the last inserted id
        
        # Insert into order_items table
        order_items_query = "INSERT INTO order_items (order_id, product_id, quantity, price) VALUES (%s, %s, %s, %s)"
        cursor.execute(order_items_query, (order_id, product_id, quantity, total_price))

        # Commit the transaction
        mysql.connection.commit()

        return jsonify(success=True), 200
    except Exception as e:
        # Rollback in case of error
        mysql.connection.rollback()
        return jsonify(success=False, error=str(e)), 500
    finally:
        # Close the cursor
        cursor.close()
```

Save the changes and test the functionality by applying for an order.

## Displaying Orders Data

### Add Route and Function
Next, provide a route and function to display the data from this route. Add the following to your `routes.py`:

```python
# Display orders
@app.route('/orders')
def orders():
    cursor = mysql.connection.cursor()
    sql = """
    SELECT 
        o.order_id, 
        o.date_time as order_date, 
        o.customer_contact, 
        o.total_price as order_total_price,
        p.name as product_name, 
        p.price_per_unit, 
        p.unit, 
        p.image_url, 
        oi.quantity, 
        oi.price as item_price
    FROM orders o
    JOIN order_items oi ON o.order_id = oi.order_id
    JOIN products p ON oi.product_id = p.product_id
    """
    cursor.execute(sql)
    orders_data = cursor.fetchall()
    cursor.close()
    return render_template('orders.html', orders_data=orders_data)
```

### Create `orders.html` in Templates
Now, create a new HTML file in the `templates` directory named `orders.html`. Add the following code:

```html
{% extends 'layout.html' %} {% block content %}
<div class="container mt-4">
  <h1 class="mb-4">Orders List</h1>
  <table class="table table-striped">
    <thead>
      <tr>
        <th scope="col">Order ID</th>
        <th scope="col">Order Date</th>
        <th scope="col">Customer Contact</th>
        <th scope="col">Order Total Price</th>
        <th scope="col">Product Name</th>
        <th scope="col">Quantity</th>
        <th scope="col">Item Price</th>
        <th scope="col">Price Per Unit</th>
        <th scope="col">Unit</th>
        <th scope="col">Product Image</th>
      </tr>
    </thead>
    <tbody>
      {% for order in orders_data %}
      <tr>
        <td>{{ order[0] }}</td>
        <td>{{ order[1] }}</td>
        <td>{{ order[2] }}</td>
        <td>{{ order[3] }}</td>
        <td>{{ order[4] }}</td>
        <td>{{ order[8] }}</td>
        <td>{{ order[9] }}</td>
        <td>{{ order[5] }}</td>
        <td>{{ order[6] }}</td>
        <td>
          <img
            src="{{ order[7] }}"
            alt="Product Image"
            class="img-fluid"
            style="max-width: 100px"
          />
        </td>
      </tr>
      {% endfor %}
    </tbody>
  </table>
</div>
{% endblock %}
```

Save and test all the functionalities of the project to ensure everything is working as expected.

---


# Step 4: Interactive Product Selection and Order Building

## 4.1 Designing the Product Catalog Interface

### Update `layout.html` with Navigation Links

1. **Enhance `layout.html` for Navigation**:
   - Add navigation links for product catalog and placeholder for future orders page.

```html
<!-- Inside layout.html -->
<header>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container-fluid">
            <a class="navbar-brand" href="/">MKNR Palengke Kiosk</a>
            <div class="navbar-nav">
                <a class="nav-link" href="/">Home</a>
                <a class="nav-link" href="/orders">Orders</a> <!-- Placeholder -->
            </div>
        </div>
    </nav>
</header>
```

### Implement Product Display in `index.html`

2. **Set Up Product Grid in `index.html`**:
   - Use Bootstrap's grid system to layout products.

```html
<!-- Inside index.html -->
{% extends 'layout.html' %}

{% block content %}
    <div class="row">
        {% for product in products %}
            <div class="col-md-3 col-sm-6 mb-4">
                <div class="card h-100">
                    <img src="{{ product.image_url }}" class="card-img-top" alt="{{ product.name }}">
                    <div class="card-body">
                        <h5 class="card-title">{{ product.name }}</h5>
                        <p class="card-text">{{ product.price_per_unit }} per {{ product.unit }}</p>
                        <!-- Quantity Adjustment Buttons -->
                        <div class="btn-group" role="group">
                            <button type="button" class="btn btn-sm btn-outline-secondary decrease">-</button>
                            <span class="quantity">1</span>
                            <button type="button" class="btn btn-sm btn-outline-secondary increase">+</button>
                        </div>
                        <!-- Add Item Button -->
                        <button type="button" class="btn btn-primary add-item">Add Item</button>
                    </div>
                </div>
            </div>
        {% endfor %}
    </div>
    <!-- Order Now Button -->
    <button id="orderNowButton" class="btn btn-success mt-3">Order Now</button>
{% endblock %}
```

## 4.2 Implementing "+/-" Buttons for Quantity Adjustment

### Create and Link `script.js` for Interactivity

1. **Write `script.js`**:
   - Implement JavaScript to handle the "+/-" buttons for quantity adjustment.

```javascript
// Inside script.js
document.addEventListener("DOMContentLoaded", function() {
    document.querySelectorAll('.decrease, .increase').forEach(button => {
        button.addEventListener('click', function() {
            let quantityElement = this.parentNode.querySelector('.quantity');
            let quantity = parseInt(quantityElement.innerText);
            if (this.classList.contains('increase')) {
                quantity++;
            } else if (quantity > 1) {
                quantity--;
            }
            quantityElement.innerText = quantity;
        });
    });

    document.querySelectorAll('.add-item').forEach(button => {
        button.addEventListener('click', function() {
            // Logic to add item to cart (to be implemented)
            console.log('Item added to cart');
        });
    });

    document.querySelector('#orderNowButton').addEventListener('click', function() {
        // Logic to show order summary modal (to be implemented)
        console.log('Show order summary');
    });
});
```

2. **Include `script.js` in `index.html`**:
   - Reference the JavaScript file at the end of the body tag.

```html
<!-- At the end of index.html -->
<script src="{{ url_for('static', filename='js/script.js') }}"></script>
```


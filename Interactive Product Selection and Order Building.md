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
<div class="container mt-4">
    <div class="row">
        {% for product in products %}
        <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 mb-4">
            <div class="card h-100">
                <img src="{{url_for('static',filename = product[4])}}" class="card-img-top product-image" alt="{{ product.name }}">
                <div class="card-body">
                    <h5 class="card-title">{{ product[1]}}</h5>
                    <p class="card-text">Price: {{ product[3] }} per {{ product.unit }}</p>
                    <button type="button" class="btn btn-primary add-item" onclick="addItemToCart('{{ product[3] }}')">Add Item</button>
                    <button type="button" class="btn btn-secondary order-item" data-bs-toggle="modal" data-bs-target="#orderModal"
                        data-name="{{ product[1] }}" data-price="{{ product[3] }}" data-unit="{{ product[2] }}"
                        onclick="setupModal(this)">Order Item</button>

                </div>
            </div>
        </div>
        {% endfor %}
    </div>
    <!-- Total Cost Display -->
    <div class="text-end mt-4">
        <h3>Total Cost: <span id="totalCost">0</span> Pesos</h3>
    </div>
</div>
{% endblock %}
```
## 4.2 Implementing the Add Item Functionality

### Create and Link `script.js` for Interactivity

1. **Write `script.js`**:
   - Implement JavaScript to handle the Add Item buttons for the total accumulated price.

```javascript
// Inside script.js
let totalCost = 0;

function updateTotalCostDisplay() {
    const totalCostDisplay = document.getElementById('totalCost');
    totalCostDisplay.innerText = totalCost.toFixed(2);
}

function addItemToCart(price) {
    totalCost += parseFloat(price);
    updateTotalCostDisplay();
}

```

2. **Include `script.js` in `index.html`**:
   - Reference the JavaScript file at the end of the body tag.

```html
<!-- At the end of index.html -->
<script src="{{ url_for('static', filename='js/script.js') }}"></script>
```


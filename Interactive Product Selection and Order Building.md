# Step 4: Interactive Product Selection and Order Building

## 4.1 Designing the Product Catalog Interface

### Implement Product Display and Image Modal in `index.html`

2. **Set Up Product Grid in `index.html`**:
   - Use Bootstrap's grid system to layout products.
   - Create a folder named `modals` in the `templates` directory.
   - Inside the `modals` folder, create a file named `image_modal.html`.

```html
<!-- Inside modals/image_modal.html -->
<div class="modal fade" id="imageModal" tabindex="-1" aria-labelledby="imageModalLabel" aria-hidden="true">
    <div class="modal-dialog modal-lg">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="imageModalLabel">Product Image</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <img id="modalImage" src="" class="img-fluid" alt="Product Image">
            </div>
        </div>
    </div>
</div>
```

```html
<!-- Inside index.html -->
{% extends 'layout.html' %}

{% block content %}
<div class="container mt-4">
    <div class="row">
        {% for product in products %}
        <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 mb-4">
            <div class="card h-100">
                 <img src="{{url_for('static',filename = product[4])}}" class="card-img-top product-image" alt="{{ product.name }}" data-bs-toggle="modal" data-bs-target="#imageModal" onclick="showImageinModal(this.src)">
                <div class="card-body">
                    <h5 class="card-title">{{ product[1]}}</h5>
                    <p class="card-text">Price: {{ product[3] }} per {{ product.unit }}</p>
                    <button type="button" class="btn btn-primary add-item" onclick="addItemToCart('{{ product[3] }}')">Add Item</button>
                    <!-- Other button elements -->
                </div>
            </div>
        </div>
        {% endfor %}
    </div>
    {% include 'modals/image_modal.html' %}
    <!-- Total Cost Display -->
    <div class="text-end mt-4">
        <h3>Total Cost: <span id="totalCost">0</span> Pesos</h3>
    </div>
</div>
{% endblock %}
```
### Code for displaying products
```html
   @app.route('/')
   def index():
       cursor = mysql.connection.cursor()
       cursor.execute("SELECT * FROM products")  # Assuming 'products' is your table name
       products = cursor.fetchall()
       print(products)
       cursor.close()
       return render_template('index.html', products=products)
```
### Implement JavaScript for Modal and Add Item Functionality

3. **Update `script.js` for Modal and Add Item Functionality**:
   - Implement JavaScript to handle both the image modal display and the Add Item functionality.

```javascript
// Inside script.js
// add item functionality
let totalCost = 0;

function updateTotalCostDisplay() {
    const totalCostDisplay = document.getElementById('totalCost');
    totalCostDisplay.innerText = totalCost.toFixed(2);
}

function addItemToCart(price) {
    totalCost += parseFloat(price);
    updateTotalCostDisplay();
}
// modal for image
function showImageinModal(imageUrl) {
    document.getElementById('modalImage').src = imageUrl;
}
```

4. **Include `script.js` in `layout.html`**:
   - Ensure the JavaScript file is referenced at the end of `index.html`.

```html
<!-- At the end of index.html -->
<script src="{{ url_for('static', filename='js/script.js') }}"></script>
```

This updated documentation includes the JavaScript code necessary for both the Add Item functionality and the image modal display. The Add Item functionality updates the total cost display when items are added, and the modal functionality allows for product images to be displayed in a larger format when clicked.

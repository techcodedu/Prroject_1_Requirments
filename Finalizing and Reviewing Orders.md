# Step 5: Finalizing and Reviewing Orders

Enhancing the user interface by adding an "Order Now" button after displaying the list of products.

## Step 1: Update the `index.html`

1. Navigate to `index.html`.
2. Locate the "Add Item" button.
3. Directly below it, insert the following HTML code for the "Order Now" button:
   ```html
   <button
            type="button"
            class="btn btn-secondary order-item"
            data-bs-toggle="modal"
            data-bs-target="#orderModal"
            data-id="{{ product[0]}}"
            data-name="{{ product[1] }}"
            data-price="{{ product[3] }}"
            data-unit="{{ product[2] }}"
            data-image="{{ url_for('static', filename=product[4]) }}"
            onclick="setupModal(this)"
          >
            Order Item
          </button>
   ```
4. Save the changes.
5. Run the project to see the changes in the index or product page.

## Step 2: Create the Order Modal

1. Create a new file in the `modals/` directory.
2. Name it `order_modal.html`.
3. Add the following code to create the modal:
   ```html
   <div class="modal fade" id="orderModal" tabindex="-1" aria-labelledby="orderModalLabel" aria-hidden="true">
   <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="orderModalLabel">Your Order</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <img id="productImage" src="" class="card-img-top product-image" alt="Product Image"/>
        <form id="orderForm" action="/submit_order" method="post">
          <input type="hidden" id="productId" name="productId"/>
          <div class="mb-3">
            <label for="productName" class="form-label">Product</label>
            <input type="text" class="form-control" id="productName" readonly/>
          </div>
          <div class="mb-3">
            <label for="quantity" class="form-label">Quantity</label>
            <input type="number" class="form-control" id="quantity" min="1" step="1" value="1" name="quantity"/>
          </div>
          <div class="mb-3">
            <label for="totalPrice" class="form-label">Total Price</label>
            <input type="text" class="form-control" id="totalPrice" name="totalPrice" readonly/>
          </div>
          <div class="mb-3">
            <label for="mobileNumber" class="form-label">Mobile Number</label>
            <input type="tel" class="form-control" id="mobileNumber" name="mobileNumber" pattern="\d*"/>
          </div>
          <button type="submit" class="btn btn-primary">Add to Order</button>
        </form>
      </div>
    </div>
  </div>
</div>
   ```
4. Save the file.
5. Make sure to include the modal in your `index.html`.
6. Test the "Order Now" button. At this point, the modal should appear, but it won't have pre-populated data.

## Step 3: Update the `script.js` File

1. Open the `script.js` file located in `static/js/`.
2. Update it with the following JavaScript code for modal setup:
   ```javascript
   // modal for order
   function setupModal(button) {
       const orderModal = document.getElementById('orderModal');
       const productIdInput = orderModal.querySelector("#productId");
       const productNameInput = orderModal.querySelector('#productName');
       const quantityInput = orderModal.querySelector('#quantity');
       const totalPriceInput = orderModal.querySelector('#totalPrice');
       const productImage = orderModal.querySelector('#productImage');

       productNameInput.value = button.dataset.name;
       productImage.src = button.dataset.image;
       productIdInput.value = button.dataset.id;
       const price = parseFloat(button.dataset.price);
       const unit = button.dataset.unit;
       quantityInput.value = "1"; // Default value for both kg and pc
       quantityInput.min = unit === "kg" ? "0.01" : "1"; // Minimum value based on unit
       quantityInput.step = unit === "kg" ? "0.01" : "1"; // Step value based on unit
       totalPriceInput.value = price.toFixed(2);

       quantityInput.oninput = () => {
           totalPriceInput.value = (parseFloat(quantityInput.value) * price).toFixed(2);
       };
   }
   ```
3. Save the changes.
4. Run the project again.
5. Test the functionality by changing the quantity in the modal and observing if the total price

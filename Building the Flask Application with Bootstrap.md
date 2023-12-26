# Step 3: Building the Flask Application with Bootstrap

## 3.1 Opening and Preparing the Project in VSCode

1. **Open Project in VSCode**:
   - Open your terminal.
   - Navigate to the root of your project folder.
   - Type `code .` to open the project in Visual Studio Code.

2. **Create `flaskapp` Directory and Subdirectories**:
   - Inside VSCode, create a new directory named `flaskapp`.
   - Inside `flaskapp`, create three subdirectories: `templates`, `static`, and within `static`, create `css`, `js`, and `images`.

## 3.2 Establishing Database Connections

### Creating `__init__.py`

1. **Initialize Flask App and Database Connection**:
   - In the `flaskapp` directory, create an `__init__.py` file.
   - Set up your Flask app with MySQL configuration.

   ```python
   from flask import Flask
   from flask_mysqldb import MySQL

   app = Flask(__name__)

   # Database Configuration
   app.config['MYSQL_HOST'] = 'localhost'
   app.config['MYSQL_USER'] = 'root'
   app.config['MYSQL_PASSWORD'] = ''
   app.config['MYSQL_DB'] = 'yourname_kiosk'

   mysql = MySQL(app)
   ```

### Creating `routes.py`

2. **Test Database Connection**:
   - In the `flaskapp` directory, create a `routes.py` file.
   - Write a test route to check the database connection.

   ```python
   from app import app, mysql
   from flask import jsonify

   @app.route('/testconnection')
   def test_connection():
       try:
           cursor = mysql.connection.cursor()
           cursor.execute("SELECT 1")
           return jsonify({"status": "Connected to the database"})
       except Exception as e:
           return jsonify({"status": "Connection failed", "error": str(e)})
   ```

3. **Run the App to Test Connection**:
   - Run your Flask app and navigate to `/testconnection` to check the database connection.
   - Once confirmed, you can remove the test route.

## 3.3 Implementing Routes and Views for Product Display

1. **Creating `layout.html`**:
   - In the `templates` directory of `flaskapp`, create a `layout.html` file.
   - This file will include the basic HTML structure with links to Bootstrap CSS and JS.

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>MKNR Palengke Kiosk</title>
       <!-- Bootstrap CSS Link -->
       <link rel="stylesheet" href="{{ url_for('static', filename='css/bootstrap.min.css') }}">
       <!-- Other Meta Tags and CSS Links -->
   </head>
   <body>
       <header>
           <!-- Header Content Here -->
       </header>

       <main class="container">
           {% block content %}{% endblock %}
       </main>

       <footer>
           <!-- Footer Content Here -->
       </footer>

       <!-- Bootstrap JS Link -->
       <script src="{{ url_for('static', filename='js/bootstrap.bundle.min.js') }}"></script>
       <!-- Other JS Scripts -->
   </body>
   </html>
   ```

2. **Creating `index.html`**:
   - Extend `layout.html` in `index.html` to display the products.

   ```html
   {% extends 'layout.html' %}

   {% block content %}
       <h1>Welcome to MKNR Palengke Kiosk</h1>
       <!-- Product display will go here -->
   {% endblock %}
   ```

3. **Implementing the Index Route**:
   - Update `routes.py` in `flaskapp` to include the route for the main page.

   ```python
   from app import app
   from flask import render_template

   @app.route('/')
   def index():
       return render_template('index.html')
   ```

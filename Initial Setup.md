# Initial Setup Guide 

Ensure you have an internet connection for this setup, as you'll need to download software and dependencies.

## Step 1: Installing Python
Python is essential for our project. Let's get it set up:

1. **Download Python and XAMPP server**:
   - Go to [python.org](https://www.python.org/downloads/) and download the version appropriate for your OS.
   - Go to [xampp](https://www.apachefriends.org/) and download the version appropriate for your OS.
   - Choose the installer specific to your operating system (Windows).

2. **Install Python**:
   - Run the downloaded installer.
   - Follow the on-screen instructions to complete the installation.

## Step 2: Creating the Project Structure
We'll organize our project in a dedicated directory.

1. **Create Project Directory**:
   - Open your terminal or command prompt.
   - Run the following command to create a new directory:
     ```
     mkdir yourname_kiosk
     ```

2. **Navigate to Your Project Directory**:
   - Change to the newly created directory with:
     ```
     cd yourname_kiosk
     ```

## Step 3: Setting Up a Virtual Environment
Isolating our project dependencies is crucial.

1. **Create a Virtual Environment**:
   - In your project directory, run:
     ```
     python -m venv appvenv
     ```

2. **Activate the Virtual Environment** (for Windows):
   - Use this command:
     ```
     appvenv\Scripts\activate
     ```

## Step 4: Installing Flask and MySQL Dependencies
Now, we'll install the necessary packages for our Flask app.

1. **Install Flask and MySQL Connector**:
   - Flask for our web framework:
     ```
     pip install Flask
     ```
   - MySQL connector for database interactions:
     ```
     pip install mysql-connector-python
     ```

## Step 5: Creating a `requirements.txt` File
Keep track of all dependencies in one place.

1. **Generate `requirements.txt`**:
   - This file will list all installed packages.
   - Run:
     ```
     pip freeze > requirements.txt
     ```

---

[🎥 **Watch the Initial Setup Video Tutorial Here**](https://www.example.com/video-tutorial)


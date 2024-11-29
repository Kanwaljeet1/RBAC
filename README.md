# RBAC
I  have created a Role based access system (user can register , login , logout ). Used Flask ,JWT and OAuth. User is  assigned either admin or user .



This application is a Flask-based web app that implements JWT authentication and Role-Based Access Control (RBAC). The application allows users to register, log in, and access protected routes based on their roles (admin or user).

Below is a step-by-step guide for running and testing this application.

Prerequisites
Before running the application, ensure that you have the following installed on your machine:

Python 3.6+ (Recommended: Python 3.7 or higher)
pip (Python's package installer)
Install Required Packages
To install the required Python libraries, use the following command:

bash
Copy code
pip install flask flask-jwt-extended bcrypt
This will install the following packages:

flask: The web framework for Python.
flask-jwt-extended: For handling JWT authentication in Flask.
bcrypt: For securely hashing passwords.
Project Structure
Your project folder should look like this:

bash
Copy code
flask-jwt-rbac/
│
├── app.py             # Main Flask app file (contains routes, templates, and logic)
└── README.md          # This readme file
Running the Flask Application
Create a Secret Key:

In the code, the Flask app uses a secret key for signing cookies and session data. Make sure to replace 'your_secret_key' and 'your_jwt_secret_key' with a strong secret key. You can generate a secret key using:

python
Copy code
import os
os.urandom(24)
Run the Flask App:

Navigate to the project folder in your terminal, and then run the following command:

bash
Copy code
python app.py
Access the Application:

The application will be running on http://localhost:5000/. You can visit the following URLs:

Home Page: http://localhost:5000/ - This will redirect you to the registration page.
Registration Page: http://localhost:5000/auth/register - Register a new user.
Login Page: http://localhost:5000/auth/login - Log in with your registered credentials.
Available Routes
The following routes are available in the app:

1. Home (/)
This route redirects to the registration page by default.
2. Registration (/auth/register)
Allows users to register with a username, password, and a role (admin or user).
Users are saved in the in-memory database (users_db).
After registration, you will be redirected to the login page.
3. Login (/auth/login)
Allows registered users to log in by providing their username and password.
If the credentials are correct, a JWT token is generated and returned.
A successful login redirects the user to their respective dashboard based on the role (admin or user).
4. Dashboard (/auth/dashboard)
After login, users will be redirected to their respective dashboard.
The dashboard page is accessible only if the user is logged in with a valid JWT token.
5. Admin Dashboard (/admin_dashboard)
A protected route for users with the admin role.
Accessible only with a valid JWT token and if the user’s role is admin.
6. User Dashboard (/user_dashboard)
A protected route for users with the user role.
Accessible only with a valid JWT token and if the user’s role is user.
7. Logout (/logout)
Logs the user out by redirecting them to the login page.
How Authentication Works
JWT Tokens:

After successful login, a JWT token is generated using the create_access_token function from flask_jwt_extended.
The token is sent to the client and can be used for future requests to access protected routes.
Protected Routes:

The routes /admin_dashboard and /user_dashboard are protected. You need to provide a valid JWT token in the Authorization header to access them.
The @jwt_required() decorator ensures the user is authenticated.
The role_required helper function checks the role of the current user before granting access to the respective dashboard.
HTML Templates
The application includes embedded HTML templates that render the following:

Home Template: A welcoming page that redirects users to the registration page.
Registration Template: A form to create a new user.
Login Template: A form to log in with an existing user account.
Dashboard Template: Displays the logged-in user's dashboard.
Admin Dashboard Template: Displays the admin’s dashboard with full access.
User Dashboard Template: Displays the regular user’s dashboard with limited access.
Each template uses Bootstrap 5 for styling and layout.

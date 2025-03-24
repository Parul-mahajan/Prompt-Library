# Writing Secure Code

## Prompt 1: Implementing Authentication Securely
```
Intent: To help developers implement secure authentication mechanisms.

Context: You are implementing authentication for an application. The application details are as follows:

Application_type: {application_type}
Authentication_requirements: {authentication_requirements}

Generate code for a secure authentication system, including:
- Secure password handling.
- Proper session management.
- Protection against common attacks.

Example:
Application_type: "Web Application"
Authentication_requirements: "User login with email and password, remember me functionality"

Secure Authentication Implementation:
```python
import hashlib
import os
from flask import Flask, request, session
import re
from datetime import timedelta

app = Flask(__name__)
app.secret_key = os.urandom(24)  # Generate a secure random key

# Store users (in production, use a database)
users_db = {}

def hash_password(password, salt=None):
    """Hash a password with a random salt."""
    if salt is None:
        salt = os.urandom(32)  # 32 bytes of random data
    
    # Use a strong hashing algorithm (in production, use bcrypt, Argon2, etc.)
    hash_obj = hashlib.pbkdf2_hmac('sha256', password.encode('utf-8'), salt, 100000)
    return {"salt": salt, "hash": hash_obj}

def validate_password_strength(password):
    """Ensure the password meets security requirements."""
    if len(password) < 12:
        return False
    if not re.search(r"[A-Z]", password):
        return False
    if not re.search(r"[a-z]", password):
        return False
    if not re.search(r"[0-9]", password):
        return False
    if not re.search(r"[^A-Za-z0-9]", password):
        return False
    return True

@app.route('/register', methods=['POST'])
def register():
    email = request.form.get('email')
    password = request.form.get('password')
    
    # Validate email format
    if not re.match(r"[^@]+@[^@]+\.[^@]+", email):
        return "Invalid email format", 400
    
    # Validate password strength
    if not validate_password_strength(password):
        return "Password does not meet security requirements", 400
    
    # Check if user already exists
    if email in users_db:
        return "User already exists", 400
    
    # Hash the password and store user
    password_data = hash_password(password)
    users_db[email] = {
        "salt": password_data["salt"],
        "hash": password_data["hash"]
    }
    
    return "User registered successfully", 201

@app.route('/login', methods=['POST'])
def login():
    email = request.form.get('email')
    password = request.form.get('password')
    remember = request.form.get('remember') == 'true'
    
    # Check if user exists
    if email not in users_db:
        # Use a generic error message to prevent user enumeration
        return "Invalid email or password", 401
    
    # Verify password
    user = users_db[email]
    password_data = hash_password(password, user["salt"])
    
    if password_data["hash"] != user["hash"]:
        # Use a generic error message
        return "Invalid email or password", 401
    
    # Regenerate session to prevent session fixation
    session.clear()
    session.regenerate()
    
    # Set session data
    session['user_id'] = email
    
    # Set session expiration for "remember me"
    if remember:
        session.permanent = True
        app.permanent_session_lifetime = timedelta(days=30)
    
    return "Login successful", 200

@app.route('/logout', methods=['POST'])
def logout():
    # Clear the session
    session.clear()
    return "Logged out successfully", 200

if __name__ == '__main__':
    app.run(ssl_context='adhoc')  # Use HTTPS in development
```

Security Features Implemented:
1. Strong password hashing with salt
2. Password strength validation
3. HTTPS for secure communication
4. Protection against session fixation
5. Remember me functionality with secure implementation
6. Generic error messages to prevent user enumeration
7. Input validation for email
```
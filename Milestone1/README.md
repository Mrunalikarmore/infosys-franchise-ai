
**⚡ Milestone 1 — User Authentication Module**

What is Milestone 1?
⚡ Infosys Portal — Milestone 1: User Authentication Module

Infosys Springboard Internship 7.0 · Batch 4 · Milestone 1 Stack: Streamlit · JWT · SQLite · bcrypt · ngrok · Gmail OTP · Google Colab

📌 About this milestone

Milestone 1 builds the login and security layer of the Infosys Portal. It is a Streamlit web app that runs inside a Google Colab notebook and is made reachable from any browser through an ngrok public URL.
A user can sign up, log in, recover a forgotten password (using a security question or an email OTP) and land on a personal dashboard. Sessions are managed with JWT tokens, passwords are never stored in plain text, and every secret (JWT key, ngrok token, email credentials) is kept in Colab Secrets instead of the code.


**🎯 Objectives**

Implement user registration and login functionality.
Validate usernames, email addresses, and passwords.
Generate JWT tokens after successful login.
Provide a Forgot Password feature using security questions or email OTP.
Implement OTP expiration after 5 minutes.
Display a personalized dashboard after login.
Provide a logout feature to clear the user session.
Ensure common access for all registered users without a separate admin login.

**🛠️ Technologies Used** : Python – Application logic
                       Streamlit – User interface
                       JWT (JSON Web Token) – Authentication token management
                       Email SMTP – Email OTP functionality
                       Regular Expressions (Regex) – Input validation
                       Google Colab – Development and testing
                       GitHub – Version control and project submission


**✨ Key Features**

1. User Signup

Register using the required user details.
Validate email format.
Enforce password complexity requirements.
Confirm the password before registration.
Prevent duplicate usernames and email addresses.

2. User Login

Authenticate users using their credentials.
Generate a JWT token after successful authentication.
Display a generic error message for invalid credentials.

3. Forgot Password

Recover access using a security question or email OTP.
Validate the new password.
Expire OTPs after 5 minutes.

4. User Dashboard

Display the logged-in user's information.
Maintain the authenticated session.
Provide a logout option.

5. Common User Access

All registered users use the same login and dashboard flow.
No separate admin login or admin-only access is provided.


.

**##📂 Project Structure**
Milestone1/
├── README.md
├── app.py
├── Milestone1.ipynb
└── screenshots/
    ├── login.png
    ├── signup.png
    ├── forgot_password.png
    └── dashboard.png

## 🔑 Secret Key Generation and Configuration

This project uses secret keys and email credentials to support authentication and password recovery. These values are configured separately from the application code to avoid exposing sensitive information in the GitHub repository.

### 1. JWT Secret Key Generation

A JWT (JSON Web Token) is used to maintain authentication after a user successfully logs in.

**Steps followed:**

1. Generate a strong, random secret key using Python.
2. Store the generated key in Google Colab Secrets under the name `JWT_SECRET`.
3. Load the secret into the Python application through an environment variable.
4. Use the secret to sign and verify JWT tokens.

Example of generating a secure key:

```python
import secrets

jwt_secret = secrets.token_urlsafe(32)
print(jwt_secret)
```

Copy the generated value into Google Colab Secrets. Do not publish the value in your README or GitHub repository.

### 2. Google Colab Secrets Configuration

Google Colab Secrets allows sensitive configuration values to be stored separately from the notebook's source code.

**Configuration steps:**

1. Open the project notebook in Google Colab.
2. Open the **Secrets** panel using the key icon.
3. Add a secret named `JWT_SECRET` and paste the generated JWT key as its value.
4. Add `EMAIL_ADDRESS` with the Gmail address used to send OTPs.
5. Add `EMAIL_PASSWORD` with the Gmail App Password.
6. Enable notebook access to each secret that the project needs.

The application then reads these values without hardcoding them into the source code.

Example:

```python
import os

JWT_SECRET = os.environ.get("JWT_SECRET", "")
EMAIL_ADDRESS = os.environ.get("EMAIL_ADDRESS", "")
EMAIL_PASSWORD = os.environ.get("EMAIL_PASSWORD", "")
```

*Note: The notebook must explicitly retrieve the values from Colab Secrets and expose them to the environment if the application uses `os.environ`. Reading environment variables alone does not automatically retrieve Colab Secrets.*

### 3. Gmail App Password for OTP Delivery

The Forgot Password feature can send a One-Time Password (OTP) to the user's email address.

**Steps followed:**

1. Enable 2-Step Verification on the Google account used for sending emails.
2. Generate an App Password through the Google Account security settings, if available.
3. Store the App Password in Colab Secrets as `EMAIL_PASSWORD`.
4. Store the sender's email address as `EMAIL_ADDRESS`.
5. Use the email credentials in the application's SMTP configuration to send OTP messages.

The Gmail App Password is different from the normal Google account password and should never be committed to GitHub.

### 4. JWT Authentication Implementation

JWT authentication is implemented in the following workflow:

1. The user enters their username or email and password.
2. The application validates the credentials against the registered user's information.
3. If authentication succeeds, the application generates a JWT token signed using `JWT_SECRET`.
4. The token contains the required identity information and expiration details.
5. The application verifies the token before allowing access to protected dashboard features.
6. On logout, the application clears the authentication session.

Invalid credentials should produce a generic error message rather than revealing whether a particular username or email exists.

### 5. Email OTP Implementation

The OTP-based password recovery workflow follows these steps:

1. The user requests password recovery.
2. The application generates a one-time verification code.
3. The code is sent to the user's registered email address using SMTP.
4. The user enters the received OTP.
5. The application checks whether the OTP is correct and has expired.
6. The OTP becomes invalid after five minutes.
7. After successful verification, the user can set a new password that meets the application's password requirements.
8. After the password reset, the user returns to the Login page and logs in using the new password.

### 6. Security Practices

- Keep JWT secrets and email credentials out of source code and GitHub.
- Use a cryptographically secure random generator for secret keys and OTPs.
- Store passwords using a suitable salted password-hashing algorithm.
- Apply expiration and verification checks to JWT tokens and OTPs.
- Avoid logging secrets, passwords, or OTP values.
- Clear the authenticated session during logout.

**▶️ How to Run**

Clone or download the repository.

Install the required Python packages.

Configure the environment variables.

Run the Streamlit application.

Install Streamlit: pip install streamlit

Install other dependencies required by your implementation, such as : pip install PyJWT

**Run the application:**

streamlit run app.py

If running through Google Colab, use the notebook's configured launch process instead.

**🧪 Testing**

Test the following scenarios:

Successful signup with valid information.

Rejection of duplicate usernames or email addresses.

Login with valid and invalid credentials.

Password validation and confirmation.

Forgot Password using the configured recovery method.

OTP expiration after 5 minutes.

Successful password reset.

Dashboard access after login.

Logout and session clearing.




                       

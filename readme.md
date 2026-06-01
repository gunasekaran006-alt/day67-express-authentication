# Simple Express.js Authentication System

A lightweight Node.js and Express backend application implementing user registration and secure two-step login using an automated 4-digit PIN system.

## 📁 Project Structure

```text
├── config/
│   └── .env
├── models/
│   └── users.models.js
├── routes/
│   └── auth.routes.js
├── security/
│   └── authentication.security.js
├── .gitignore
├── main.js
├── package.json
└── README.md
```

## 🛠️ Backend Folder Creation Steps

### Step 1: Create a New Folder
Create a dedicated workspace folder on your machine for the backend project.

### Step 2: Initialize the Project
Initialize a default `package.json` file.
```bash
npm init -y
```

### Step 3: Configure Entry Point
Open `package.json` and change the entry file name from `"index.js"` to `"main.js"`:
```json
"main": "main.js"
```

### Step 4: Create Main File
Create a new file named `main.js` in the root directory.

### Step 5: Install Production Dependencies
Install Express to handle server routing.
```bash
npm i express dotenv
```

### Step 6: Configure Environment & Git
Create a `.env` file in your root folder and define your server port:
```env
SERVERPORT=8080
```
Create a `.gitignore` file and include the following paths to hide heavy dependencies and credentials:
```text
node_modules
.env
```

### Step 7: Create the Express Server
Add this baseline server code to your `main.js`:
```javascript
require('dotenv').config();
const express = require("express");
const authRoutes = require("./routes/auth.routes");

const app = express();
const PORT = process.env.SERVERPORT || 8080;

app.use(express.json());

// Routes
app.use("/auth", authRoutes);

app.listen(PORT, () => {
    console.log(`Server running smoothly on port ${PORT}`);
});
```

### Step 8: Install Development Dependencies
Install Nodemon to auto-restart the local server during file changes.
```bash
npm i -D nodemon
```

### Step 9: Add Development Script
Update the `"scripts"` section in your `package.json` file:
```json
"scripts": {
    "dev": "nodemon main.js"
}
```

### Step 10: Launch the Application
Start your backend server in development mode.
```bash
npm run dev
```

## 🚀 API Endpoints Documentation

### 1. User Registration
* **URL:** `http://localhost:8080/auth/register`
* **Method:** `POST`
* **Headers:** `Content-Type: application/json`
* **Request Body:**
  ```json
  {
    "username": "JohnDoe",
    "email": "john@example.com",
    "password": "securepassword123"
  }
  ```
* **Success Response (201):**
  ```json
  {
    "message": "User Registration Successful, Check console for your login pin"
  }
  ```
  *(Note: Check your server terminal/console logs to find your generated 4-digit temporary login PIN)*

### 2. User Login
* **URL:** `http://localhost:8080/auth/login`
* **Method:** `POST`
* **Headers:** 
  * `Content-Type: application/json`
  * `pin: <4-digit-pin-from-console>`
* **Request Body:**
  ```json
  {
    "email": "john@example.com",
    "password": "securepassword123"
  }
  ```
* **Success Response (200):**
  ```json
  {
    "message": "Welcome back",
    "name": "JohnDoe"
  }
  ```

## 🔒 Security Features
* **In-Memory Storage:** Uses temporary arrays for local user tracking.
* **Two-Step Verification:** Generates random 4-digit unique login validation codes.
* **Credential Validation:** Screens out duplicating email registrants instantly.

Here’s a comprehensive `README.md` for your **JWT Authentication API**:

---

# **JWT Authentication API**

This is a RESTful API for user authentication built with **Gin** and secured using **JWT (JSON Web Tokens)**. It provides endpoints for user registration, login, and access to protected routes.

---

## **Features**
- **User Registration**: Register a new user (in-memory for simplicity).
- **User Login**: Authenticate with username and password to receive a JWT token.
- **Protected Routes**: Access routes secured with JWT authentication.
- **Token-Based Authorization**: Protect sensitive resources using JSON Web Tokens.

---

## **Technologies Used**
- **Go**: Programming language.
- **Gin**: Web framework for building APIs.
- **JWT**: Token-based authentication mechanism.

---

## **Project Structure**
```
jwt_auth_api/
├── main.go            # Main application file
├── go.mod             # Go module file
├── go.sum             # Dependency file
```

---

## **API Endpoints**

### **Base URL**
```
http://localhost:8080
```

---

### **1. Register**
- **Endpoint**: `/register`
- **Method**: `POST`
- **Description**: Register a new user (dummy implementation for simplicity).
- **Request Body Example**:
  ```json
  {
    "username": "admin",
    "password": "password"
  }
  ```
- **Response**:
  ```json
  {
    "message": "User registered"
  }
  ```

---

### **2. Login**
- **Endpoint**: `/login`
- **Method**: `POST`
- **Description**: Authenticate with username and password to receive a JWT token.
- **Request Body Example**:
  ```json
  {
    "username": "admin",
    "password": "password"
  }
  ```
- **Response**:
  ```json
  {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
  ```

---

### **3. Protected Route**
- **Endpoint**: `/protected/data`
- **Method**: `GET`
- **Description**: Access a protected route with a valid JWT token.
- **Headers**:
  ```plaintext
  Authorization: Bearer <your-token>
  ```
- **Response**:
  ```json
  {
    "data": "This is protected data"
  }
  ```

If the token is missing or invalid, you’ll get:
```json
{
  "error": "Invalid token"
}
```

---

## **Setup Instructions**

### **1. Prerequisites**
- Install **Go**: [Download and install Go](https://go.dev/dl/).

### **2. Clone the Repository**
```bash
git clone https://github.com/your-username/jwt_auth_api.git
cd jwt_auth_api
```

### **3. Install Dependencies**
Install the required Go packages:
```bash
go mod tidy
```

### **4. Run the Server**
Start the server:
```bash
go run main.go
```

The server will start on `http://localhost:8080`.

---

## **Testing the API**

You can use `curl` or tools like Postman to test the API.

### **Using cURL**
#### **Register a User**
```bash
curl -X POST -H "Content-Type: application/json" -d '{"username":"admin","password":"password"}' http://localhost:8080/register
```

#### **Login to Get a Token**
```bash
curl -X POST -H "Content-Type: application/json" -d '{"username":"admin","password":"password"}' http://localhost:8080/login
```

#### **Access Protected Data**
```bash
curl -X GET -H "Authorization: Bearer <your-token>" http://localhost:8080/protected/data
```
Replace `<your-token>` with the token obtained from the `/login` endpoint.

---

## **How JWT Works**
1. **Login**: A user logs in with their username and password. If valid, the server generates a JWT token and sends it to the user.
2. **Protected Routes**: The client includes the token in the `Authorization` header (`Bearer <token>`) for requests to protected routes.
3. **Validation**: The server validates the token and grants or denies access based on its validity.

---

## **Future Enhancements**
1. **Persistent User Storage**: Use a database to store user credentials securely (hashed).
2. **Password Hashing**: Hash passwords using libraries like `bcrypt`.
3. **Token Expiry Management**: Add a token refresh mechanism for expired tokens.
4. **Role-Based Authorization**: Implement roles (e.g., `admin`, `user`) for more granular access control.
5. **Deploy the API**: Host the application on platforms like AWS, Heroku, or Docker.

---

## **License**
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

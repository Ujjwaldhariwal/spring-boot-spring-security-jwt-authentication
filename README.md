# spring-boot-spring-security-jwt-authentication

To test the authentication and authorization functionality of your Spring Boot application with JWT, you can use Postman to send requests. Here are the steps to test your endpoints:

1. **Register a User**:
   - **Endpoint:** `POST http://localhost:8080/api/auth/signup`
   - **Request Body:**
     ```json
     {
       "username": "testuser",
       "email": "testuser@example.com",
       "password": "password123",
       "role": ["user"]
     }
     ```
   - This will create a new user with the role "USER."

2. **Authenticate User and Get JWT Token**:
   - **Endpoint:** `POST http://localhost:8080/api/auth/signin`
   - **Request Body:**
     ```json
     {
       "username": "testuser",
       "password": "password123"
     }
     ```
   - This will return a response containing the JWT token.

3. **Access Public Content**:
   - **Endpoint:** `GET http://localhost:8080/api/test/all`
   - This should return "Public Content."

4. **Access User Content**:
   - **Endpoint:** `GET http://localhost:8080/api/test/user`
   - Include the JWT token in the Authorization header with the value "Bearer YOUR_JWT_TOKEN."
   - This should return "User Content."

5. **Access Moderator Content**:
   - **Endpoint:** `GET http://localhost:8080/api/test/mod`
   - Include the JWT token in the Authorization header with the value "Bearer YOUR_JWT_TOKEN."
   - This should return "Moderator Board."

6. **Access Admin Content**:
   - **Endpoint:** `GET http://localhost:8080/api/test/admin`
   - Include the JWT token in the Authorization header with the value "Bearer YOUR_JWT_TOKEN."
   - This should return "Admin Board."

Make sure to replace `http://localhost:8080` with the actual base URL of your running Spring Boot application. Also, ensure that the required dependencies are properly configured, and the server is up and running.

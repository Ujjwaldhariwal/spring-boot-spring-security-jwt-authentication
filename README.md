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



The workflow of Our Spring Boot application:

1. **User Registration (`/api/auth/signup`)**:
   - Users can register by sending a POST request to `/api/auth/signup`.
   - The provided information (username, email, password, and role) is validated and used to create a new user in the database.
   - The password is hashed using BCryptPasswordEncoder before saving.

2. **User Authentication (`/api/auth/signin`)**:
   - Users can authenticate by sending a POST request to `/api/auth/signin`.
   - The application uses Spring Security to authenticate the user with the provided username and password.
   - Upon successful authentication, a JWT (JSON Web Token) is generated and returned in the response.

3. **JWT Generation and Validation**:
   - The `JwtUtils` class handles the generation and validation of JWTs.
   - When a user is successfully authenticated, a JWT token is created, including the user's information and roles.
   - The generated JWT is sent to the client.

4. **Accessing Protected Endpoints (`/api/test/**`)**:
   - Certain endpoints (e.g., `/api/test/user`, `/api/test/mod`, `/api/test/admin`) are protected and require a valid JWT for access.
   - The `AuthTokenFilter` intercepts incoming requests and checks for a valid JWT in the `Authorization` header.
   - If a valid JWT is present, the user is authenticated, and Spring Security allows access to the protected resource.

5. **Handling Unauthorized Access**:
   - If a user tries to access a protected resource without a valid JWT or with an invalid JWT, the `AuthEntryPointJwt` class handles the unauthorized request.
   - An error response is returned with information about the unauthorized access.

6. **User Details and Roles**:
   - The `UserDetailsServiceImpl` class implements the `UserDetailsService` interface to load user details during authentication.
   - The `UserDetailsImpl` class represents the authenticated user and includes details like username, password, email, and roles.

7. **Role-Based Authorization**:
   - The `@PreAuthorize` annotation is used to specify role-based access control for certain endpoints.
   - Users must have the required role(s) in their JWT to access these endpoints.

8. **Password Encoding and Security Configuration**:
   - Passwords are securely encoded using BCryptPasswordEncoder.
   - Security configurations, including CORS, CSRF, and session management, are defined in the `WebSecurityConfig` class.

9. **Exception Handling**:
   - Exception handling is implemented in the `AuthEntryPointJwt` class to provide meaningful error responses for unauthorized access.



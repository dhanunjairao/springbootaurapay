# AuraPay

A full-stack banking application built with Spring Boot and React.

---

## Project Structure

```
AuraPay/
  Backend/    Spring Boot REST API
  frontend/   React + TypeScript frontend
```

---

## Backend

**Stack:** Java 21, Spring Boot 3.5.13, Spring Security, JWT, JPA, MySQL

**Package:** `com.example.Micro_Bank` (simplified to AuraPay)

### Setup

1. Create a MySQL database named `microbank`
2. Update `src/main/resources/application.properties` with your DB credentials
3. Run the application

```
cd Backend
mvn spring-boot:run
```

The server starts on `http://localhost:9090`

### Configuration

```
spring.datasource.url=jdbc:mysql://localhost:3306/microbank
spring.datasource.username=<your_username>
spring.datasource.password=<your_password>
jwt.secret=<your_secret>
jwt.expiration=86400000
```

### API Endpoints

**Public**

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /api/user/register | Register a new user |
| POST | /api/user/login | Login and receive JWT token |

**Protected (requires Authorization: Bearer token)**

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /api/account/deposit | Deposit amount |
| POST | /api/account/withdraw | Withdraw amount |
| POST | /api/transaction/transfer | Transfer to another account |
| GET | /api/transaction/history/{accountId} | Get transaction history |

### Request Examples

Register
```json
POST /api/user/register
{
  "name": "John",
  "email": "john@example.com",
  "password": "yourpassword",
  "pin": "1234"
}
```

Deposit
```json
POST /api/account/deposit
Authorization: Bearer <token>
{
  "accountId": 1,
  "amount": 500.0
}
```

Transfer
```json
POST /api/transaction/transfer
Authorization: Bearer <token>
{
  "senderAccountId": 1,
  "receiverAccountId": 2,
  "amount": 200.0,
  "pin": "1234",
  "confirmed": true
}
```

### Security

- Passwords are hashed using BCrypt
- Authentication is handled via JWT tokens
- All endpoints except register and login require a valid token
- Spring Security enforces access control on every request

### Project Layout

```
Backend/src/main/java/com/example/Micro_Bank/
  Controller/       AccountController, TransactionController, UserController
  DTO/              Request and response data transfer objects
  Entity/           User, Account, Transaction
  Exception/        GlobalExceptionHandler and custom exceptions
  Repository/       JPA repositories
  Security/         JwtUtil, JwtFilter, SecurityConfig
  Service/          AccountService, TransactionService, UserService
  AuraPayApplication.java  Main application file
```

---

## Frontend

**Stack:** React 19, TypeScript, Vite

### Setup

```
cd frontend
npm install
npm run dev
```

The app runs on `http://localhost:5173`

### Pages

- Login - email and password login, redirects to dashboard on success
- Register - creates a new user (with a secure 4-digit PIN) and account, redirects to dashboard
- Dashboard - shows current balance with deposit, withdraw, and transfer actions
- History tab - lists all transactions with type, amount, and date

### API Communication

All API calls are in `src/api.ts`. After login or register, the JWT token is stored in `localStorage` and attached as an `Authorization` header on every subsequent request.

### Project Layout

```
frontend/src/
  pages/      Login.tsx, Register.tsx, Dashboard.tsx
  api.ts      All backend API calls
  App.tsx     Page routing and auth state
  index.css   Global styles
```
## Screenshots

### Home Page

<img width="472" height="699" alt="Screenshot 1948-01-16 at 4 36 25 PM" src="https://github.com/user-attachments/assets/b663afac-dbcd-43aa-b5a1-3ca7a8752e1f" />

#account

<img width="554" height="702" alt="Screenshot 1948-01-16 at 4 36 18 PM" src="https://github.com/user-attachments/assets/8e6df118-9a95-4fa1-9d5e-ab4249a6c9ce" />



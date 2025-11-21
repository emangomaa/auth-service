# Authentication Service

A complete authentication service built with NestJS, Prisma, MySQL, and JWT.

## Features

- User registration with email and password
- User login with JWT token generation
- Password hashing using bcrypt
- JWT-based authentication
- Protected routes with JWT guards
- Input validation using class-validator
- MySQL database with Prisma ORM

## Prerequisites

- Node.js (v18 or higher)
- MySQL database
- npm or yarn

## Installation

1. Install dependencies:
```bash
npm install
```

2. Set up your environment variables:
   - Create a `.env` file in the root directory
   - Add the following variables:
   ```
   DATABASE_URL="mysql://user:password@localhost:3306/auth_db"
   JWT_SECRET="your-super-secret-jwt-key-change-this-in-production"
   JWT_EXPIRES_IN="1d"
   ```

3. Set up the database:
```bash
# Generate Prisma Client
npm run prisma:generate

# Run migrations
npm run prisma:migrate
```

## Running the Application

```bash
# Development mode
npm run start:dev

# Production mode
npm run build
npm run start:prod
```

The application will run on `http://localhost:3000`

## API Endpoints

### Register
- **POST** `/auth/register`
- **Body:**
  ```json
  {
    "email": "user@example.com",
    "password": "password123",
    "name": "John Doe"
  }
  ```
- **Response:**
  ```json
  {
    "user": {
      "id": 1,
      "email": "user@example.com",
      "name": "John Doe",
      "createdAt": "2024-01-01T00:00:00.000Z"
    },
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
  ```

### Login
- **POST** `/auth/login`
- **Body:**
  ```json
  {
    "email": "user@example.com",
    "password": "password123"
  }
  ```
- **Response:**
  ```json
  {
    "user": {
      "id": 1,
      "email": "user@example.com",
      "name": "John Doe",
      "createdAt": "2024-01-01T00:00:00.000Z"
    },
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
  ```

### Get Profile (Protected)
- **GET** `/auth/profile`
- **Headers:**
  ```
  Authorization: Bearer <access_token>
  ```
- **Response:**
  ```json
  {
    "id": 1,
    "email": "user@example.com",
    "name": "John Doe",
    "createdAt": "2024-01-01T00:00:00.000Z"
  }
  ```

## Project Structure

```
src/
├── auth/
│   ├── dto/
│   │   ├── login.dto.ts
│   │   └── register.dto.ts
│   ├── auth.controller.ts
│   ├── auth.module.ts
│   ├── auth.service.ts
│   ├── jwt.strategy.ts
│   └── jwt-auth.guard.ts
├── prisma/
│   ├── prisma.module.ts
│   └── prisma.service.ts
├── app.module.ts
└── main.ts
```

## Environment Variables

```env
DATABASE_URL="mysql://user:password@localhost:3306/auth_db"
JWT_SECRET="your-super-secret-jwt-key-change-this-in-production"
JWT_EXPIRES_IN="1d"
```

## Database Schema

The User model includes:
- `id`: Auto-incrementing integer (primary key)
- `email`: Unique string
- `password`: Hashed password string
- `name`: Optional string
- `createdAt`: Timestamp
- `updatedAt`: Timestamp

## Security Features

- Passwords are hashed using bcrypt (10 rounds)
- JWT tokens for stateless authentication
- Input validation on all endpoints
- Protected routes using JWT guards

## Development

```bash
# Generate Prisma Client after schema changes
npm run prisma:generate

# Create a new migration
npm run prisma:migrate

# Open Prisma Studio (database GUI)
npm run prisma:studio
```

## License

MIT


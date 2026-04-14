# Voting App

A secure, scalable voting application built with Node.js, Express, and MongoDB. This application allows users to register, authenticate, and vote for candidates while preventing duplicate votes and restricting admin privileges.

## Features

- **User Authentication**: Secure signup and login using JWT tokens
- **Password Security**: Bcrypt hashing for secure password storage
- **Role-Based Access Control**: Distinguish between voters and admins
- **Vote Prevention**: Users can only vote once
- **Admin Controls**: Only admins can add, update, and delete candidates
- **Vote Counting**: Real-time vote tallying and ranking of candidates
- **Aadhar Validation**: 12-digit Aadhar Card number validation

## Tech Stack

- **Backend**: Node.js, Express.js
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JWT (JSON Web Tokens)
- **Password Hashing**: Bcrypt
- **Body Parser**: For JSON request handling

## Prerequisites

Before running this project, make sure you have:

- Node.js (v14 or higher)
- npm (v6 or higher)
- MongoDB (local or cloud instance)
- Git

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/voting-app.git
   cd voting-app
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Create a `.env` file** in the root directory with the following variables:
   ```env
   PORT=3000
   MONGODB_URL_LOCAL=mongodb://localhost:27017/voting-app
   MONGODB_URL=mongodb+srv://username:password@cluster.mongodb.net/voting-app
   JWT_SECRET=your_jwt_secret_key_here
   ```

4. **Start the server**:
   ```bash
   node server.js
   ```

The server will run on `http://localhost:3000`

## API Endpoints

### User Routes

#### Signup
- **POST** `/user/signup`
- **Body**: 
  ```json
  {
    "name": "John Doe",
    "age": 30,
    "email": "john@example.com",
    "mobile": "9876543210",
    "address": "123 Main Street",
    "aadharCardNumber": "123456789012",
    "password": "securePassword123",
    "role": "voter"
  }
  ```
- **Response**: User data and JWT token

#### Login
- **POST** `/user/login`
- **Body**:
  ```json
  {
    "aadharCardNumber": "123456789012",
    "password": "securePassword123"
  }
  ```
- **Response**: JWT token

#### Get Profile
- **GET** `/user/profile`
- **Headers**: Authorization: Bearer `{token}`
- **Response**: User profile data

#### Change Password
- **PUT** `/user/profile/password`
- **Headers**: Authorization: Bearer `{token}`
- **Body**:
  ```json
  {
    "currentPassword": "oldPassword",
    "newPassword": "newPassword123"
  }
  ```
- **Response**: Success message

### Candidate Routes

#### Get All Candidates
- **GET** `/candidate`
- **Response**: List of candidates (name and party only)

#### Add Candidate (Admin only)
- **POST** `/candidate`
- **Headers**: Authorization: Bearer `{token}`
- **Body**:
  ```json
  {
    "name": "Candidate Name",
    "party": "Party Name",
    "age": 45
  }
  ```
- **Response**: Candidate data

#### Update Candidate (Admin only)
- **PUT** `/candidate/:candidateID`
- **Headers**: Authorization: Bearer `{token}`
- **Body**: Fields to update
- **Response**: Updated candidate data

#### Delete Candidate (Admin only)
- **DELETE** `/candidate/:candidateID`
- **Headers**: Authorization: Bearer `{token}`
- **Response**: Deleted candidate data

#### Cast Vote
- **GET** `/candidate/vote/:candidateID`
- **Headers**: Authorization: Bearer `{token}`
- **Response**: Vote recorded successfully

#### Get Vote Count
- **GET** `/candidate/vote/count`
- **Response**: List of candidates sorted by vote count

## Project Structure

```
voting-app/
├── models/
│   ├── user.js           # User schema and methods
│   └── candidate.js      # Candidate schema
├── routes/
│   ├── userRoutes.js     # User endpoints
│   └── candidateRoutes.js # Candidate endpoints
├── db.js                 # MongoDB connection
├── jwt.js                # JWT authentication middleware
├── server.js             # Express server setup
├── package.json          # Project dependencies
└── README.md             # This file
```

## Security Features

- **Password Hashing**: Passwords are hashed using bcrypt before storage
- **JWT Authentication**: Secure token-based authentication
- **Role-based Access**: Admin-only operations are protected
- **Input Validation**: Aadhar card numbers are validated
- **Duplicate Prevention**: Users can vote only once
- **Unique Constraints**: Aadhar card numbers are unique in the database

## Error Handling

The application includes comprehensive error handling for:
- Invalid credentials
- Unauthorized access
- Database errors
- Validation errors
- Duplicate entries

All errors return appropriate HTTP status codes and error messages.

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the ISC License - see the LICENSE file for details.

## Support

For support, email your-email@example.com or open an issue in the repository.

## Author

Created by Harsh Vardhan Gooboori

---

**Note**: Never commit the `.env` file to version control. Always use environment variables for sensitive information.

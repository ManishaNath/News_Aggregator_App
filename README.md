# News Aggregator Application Documentation
RESTful API using Node.js, Express.js, and NPM packages. The API will allow users to register, log in, and set their news preferences (e.g., categories, sources). The API will then fetch news articles from multiple sources using external news APIs. The fetched articles should be processed and filtered asynchronously on user preference.

## Overview
The News Aggregator Application is a web-based platform that aggregates news articles from various sources based on user preferences. It provides a personalized news feed for users, allowing them to stay informed about topics of interest.

## How To Run The Project

### Clone the Repository

```bash
https://github.com/ManishaNath/News_Aggregator_App/tree/dev

> Navigate to the Project Directory
--  cd News_Aggregator_App

> Install the dependencies, Node modules get generated
--  npm install

> Run the project under dev dependencies
--  npm run dev
```
  
## Dependencies

Install the below dependency packages for different purposes:-

npm install --save express
npm install --save axios    
npm install --save-dev nodemon 
npm install --save body-parser
npm install --save dotenv
npm install --save bcrypt 
npm install --save mongoose 
npm install --save-dev jsonwebtoken 
npm install newsapi --save
npm install --save http-status-codes

# Architecture
## Backend
The backend is built using Node.js with Express.js as the web application framework. MongoDB is used as the database to store user information, preferences, and other relevant data. Mongoose is employed as an ODM (Object Data Modeling) library for MongoDB.

## Controllers
### User Authentication: 
Handles user signup, login, and token generation using bcrypt for password hashing and JWT (JSON Web Token) for authentication.

### User Preferences:
Manages user preferences, allowing users to set their preferred topics for news articles.

### News Aggregation: 
Fetches news articles from external APIs based on user preferences.

## Middleware
### Authentication Middleware:
Verifies user authentication using JWT before processing requests that require authentication.
Helpers
### News Aggregator Promise: 
Provides helper functions for handling promises related to news aggregation.

## Database
MongoDB is chosen as the database for its flexibility and scalability. The database stores user details, including full name, email, role, hashed password, preferences, and timestamps.

## User Authentication
User authentication is implemented using JWT. Upon successful login, a token is generated and sent to the client, which is then included in subsequent requests to authenticate the user.

## User Preferences
Users can set their news preferences, specifying topics of interest. The application uses these preferences to tailor the news feed for each user.

## News Aggregation
News aggregation involves fetching news articles from external APIs. Axios is used as the HTTP client to make requests to the News API. The application dynamically selects a random preference from the user's list to diversify the news feed.

## Testing

open the browser and type in **http://localhost:3000/** and hit enter! Follow the below endpoints for further testing

## Postman

## POST /register
**Request**

{
  "fullName": "John Doe",
  "email": "john.doe@example.com",
  "role": "normal",
  "password": "password123",
  "preferences": ["sports", "technology"]
}
**Response (Success)**

{
  "message": "User saved successfully"
}

**Response (Error)**

{
  "message": "User saving failed [error message]"
}

## POST /login
Request
{
  "email": "john.doe@example.com",
  "password": "password123"
}

Response (Success)
{
  "user": {
    "id": "[user_id]"
  },
  "message": "Login successful",
  "accessToken": "[access_token]"
}

Response (Error)

{
  "message": "Invalid Password!"
}

## GET /preferences
Request
No request body is required. The request should include the Authorization header with a valid JWT.

Response (Success)
{
  "data": {
    "preferences": ["sports", "technology"]
  },
  "message": "User preferences fetched successfully"
}

Response (Error)
{
  "message": "Error fetching user preferences",
  "error": "[error_message]"
}

## PUT /preferences
Request
{
  "preferences": ["politics", "science"]
}

Response (Success)
{
  "data": ["politics", "science"],
  "message": "User preferences updated successfully"
}

Response (Error)
{
  "message": "User not authenticated"
}

## GET /news
Request
No request body is required. The request should include the Authorization header with a valid JWT.

Response (Success)
{
  "data": [
    {
      "title": "News Article 1",
      "description": "Description of the news article 1",
      // ... other fields
    },
    {
      "title": "News Article 2",
      "description": "Description of the news article 2",
      // ... other fields
    },
    // ... more articles
  ],
  "message": "News fetched successfully"
}

Response (Error)
{
  "message": "User not authenticated"
}
## API Reference

#### Register

```http
 POST /register
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `fullName` | `string` | **Required**. Your FullName|
| `email` | `string` | **Required**. Your email      |
| `role` | `string` | **Required**. Your Role        |
| `password` | `string` | **Required**. Your password|
| `preferences` | `string[]` | **Required**. preferences|
| `created ` | `Date` | **Required**. created Date |

#### Login

```http
  POST /login
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `email` | `string` | **Required**. Your email to fetch     |
| `password` | `string` |  **Required**. Password to compare     |

# Deployment
The application can be deployed on cloud platforms like AWS, Heroku, or similar services. Continuous Integration (CI) and Continuous Deployment (CD) pipelines can be set up for automated testing and deployment.

# Conclusion
The News Aggregator Application provides a seamless experience for users to stay updated on topics they care about. Its modular architecture allows for easy scalability and maintenance.

## Folder Structure
```
├───src
│   ├───config
│   ├───controllers
│   ├───middlewares
│   ├───models
│   ├───routes
│   ├───services
│   └───utils
│      ├───common

____index.js
____.env
____.gitignore
____package-lock.json
____package.json

```

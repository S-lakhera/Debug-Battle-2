# Debug-Battle-2

A full-stack web application for managing products, orders, and inventory with user authentication. This project demonstrates a complete MERN (MongoDB, Express, React, Node.js) stack implementation with debugging and fixes already applied.

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Folder Structure](#folder-structure)
- [Installation](#installation)
- [Configuration](#configuration)
- [API Documentation](#api-documentation)
- [Running the Application](#running-the-application)
- [Debugging Notes](#debugging-notes)

## 🎯 Project Overview

Debug-Battle-2 is a debugging exercise project that implements an e-commerce platform with:
- User authentication (registration, login, logout)
- Product management with image uploads
- Order placement and tracking
- Inventory management
- JWT-based authorization

## ✨ Features

- **User Authentication**: Register, login, and token refresh with JWT
- **Product Management**: Create and retrieve products with image support
- **Order Management**: Place and manage orders
- **Inventory Tracking**: Monitor and manage product stock
- **Image Upload**: Cloudinary integration for image hosting
- **Protected Routes**: Middleware-based route protection
- **Modern UI**: React with Tailwind CSS and Radix UI components

## 🛠 Tech Stack

### Backend
- **Node.js** with Express.js
- **MongoDB** with Mongoose
- **JWT** for authentication
- **Cloudinary** for image uploads
- **Bcryptjs** for password hashing
- **Multer** for file uploads

### Frontend
- **React** 19.2.6
- **Vite** for fast development and building
- **Tailwind CSS** for styling
- **Radix UI** for component library
- **React Router** v7 for routing
- **Axios** for HTTP requests

## 📁 Folder Structure

```
Debug-Battle-2/
├── server/                          # Backend application
│   ├── config/
│   │   └── db.js                   # MongoDB connection configuration
│   ├── controllers/                # Route handlers
│   │   ├── authController.js       # Authentication logic
│   │   ├── productController.js    # Product management
│   │   ├── orderController.js      # Order management
│   │   ├── userController.js       # User operations
│   │   └── inventoryController.js  # Inventory management
│   ├── middleware/
│   │   ├── authMiddleware.js       # JWT verification
│   │   ├── errorMiddleware.js      # Error handling
│   │   └── uploadMiddleware.js     # Multer configuration for file uploads
│   ├── models/                     # Mongoose schemas
│   │   ├── User.js
│   │   ├── Product.js
│   │   ├── Order.js
│   │   └── Inventory.js
│   ├── routes/                     # API route definitions
│   │   ├── authRoutes.js           # Authentication endpoints
│   │   ├── userRoutes.js           # User endpoints
│   │   ├── productRoutes.js        # Product endpoints
│   │   ├── orderRoutes.js          # Order endpoints
│   │   └── inventoryRoutes.js      # Inventory endpoints
│   ├── .env.example                # Environment variables template
│   ├── server.js                   # Express app entry point
│   └── package.json                # Backend dependencies
├── frontend/                        # React frontend application
│   ├── src/
│   │   ├── components/             # React components
│   │   ├── pages/                  # Page components
│   │   ├── utils/
│   │   │   └── axios.js            # Axios instance with base URL
│   │   ├── App.jsx                 # Main App component
│   │   └── main.jsx                # Entry point
│   ├── .env.example                # Frontend environment variables
│   ├── index.html                  # HTML template
│   ├── vite.config.js              # Vite configuration
│   ├── tailwind.config.js          # Tailwind CSS configuration
│   ├── package.json                # Frontend dependencies
│   └── public/                     # Static assets
├── ERRORS.md                       # Documentation of bugs found and fixed
└── README.md                       # This file
```

## 🚀 Installation

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn
- MongoDB (local or Atlas connection)
- Cloudinary account for image uploads

### Backend Setup

1. Navigate to the server directory:
```bash
cd server
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file based on `.env.example`:
```bash
cp .env.example .env
```

4. Update the `.env` file with your configuration:
```env
NODE_ENV=development
PORT=5000
MONGO_URI=mongodb://localhost:27017/debugbattle2
JWT_SECRET=your_secure_random_string_here
JWT_REFRESH_SECRET=your_secure_random_string_here
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

### Frontend Setup

1. Navigate to the frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file based on `.env.example`:
```bash
cp .env.example .env
```

4. Update the `.env` file:
```env
VITE_API_URL=http://localhost:5000/api
```

## ⚙️ Configuration

### MongoDB Connection
- Update `MONGO_URI` in `server/.env`
- Default: `mongodb://localhost:27017/debugbattle2`
- For MongoDB Atlas: `mongodb+srv://username:password@cluster.mongodb.net/debugbattle2`

### JWT Secrets
- Generate secure random strings for `JWT_SECRET` and `JWT_REFRESH_SECRET`
- Use different values for development and production

### Cloudinary Setup
1. Sign up at [Cloudinary](https://cloudinary.com)
2. Get your Cloud Name, API Key, and API Secret from your dashboard
3. Add these to your `.env` file

### CORS Configuration
- Frontend runs on `http://localhost:5173` (Vite default)
- Backend CORS is configured to accept requests from this origin
- Update `server/server.js` line 14 if using different ports

## 📡 API Documentation

### Base URL
```
http://localhost:5000/api
```

### Authentication Endpoints (`/api/auth`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/register` | Register a new user | No |
| POST | `/login` | Login user and receive JWT tokens | No |
| POST | `/refresh` | Refresh access token | No |
| POST | `/logout` | Logout user | Yes |

**Register Request:**
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securePassword123"
}
```

**Login Request:**
```json
{
  "email": "john@example.com",
  "password": "securePassword123"
}
```

### Product Endpoints (`/api/products`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/` | Get all products | Yes |
| POST | `/` | Create a new product | Yes |

**Create Product Request:**
```
POST /api/products
Content-Type: multipart/form-data

Form Data:
- name: "Product Name"
- price: 99.99
- description: "Product description"
- image: <file>
```

### Order Endpoints (`/api/orders`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/` | Get all orders | Yes |
| POST | `/` | Create a new order | Yes |

**Create Order Request:**
```json
{
  "productId": "product_id_here",
  "quantity": 2
}
```

### Inventory Endpoints (`/api/inventory`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/` | Get inventory status | Yes |
| PUT | `/:id` | Update inventory | Yes |

### User Endpoints (`/api/users`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/profile` | Get user profile | Yes |
| PUT | `/profile` | Update user profile | Yes |

## 🏃 Running the Application

### Start MongoDB
```bash
# If using local MongoDB
mongod
```

### Start Backend Server
```bash
cd server
npm run dev
```
The server will start on `http://localhost:5000`

### Start Frontend Development Server
```bash
cd frontend
npm run dev
```
The frontend will open at `http://localhost:5173`

### Build for Production
```bash
# Frontend
cd frontend
npm run build

# Backend is already production-ready
```

## 🐛 Debugging Notes

This project includes several debugging fixes. See `ERRORS.md` for detailed information about:

**Server Issues Fixed:**
1. Database connection called before dotenv configuration
2. Missing multer package installation
3. Password exposure in authentication responses
4. CORS origin configuration issues
5. JWT secret environment variable updates
6. Inventory stock checking logic in orders

**Frontend Issues Fixed:**
1. Incorrect password input field naming
2. Axios baseURL configuration
3. Product and order endpoint path corrections
4. UI styling (variant and color) updates

## 📝 License

ISC

## 👨‍💻 Developer Notes

- All routes except `/api/auth/register` and `/api/auth/login` require authentication
- Authentication is handled via JWT tokens passed in cookies
- Images are uploaded to Cloudinary and URLs are stored in the database
- Error handling middleware catches all application errors and returns consistent responses

## 🤝 Contributing

When working with this project:
1. Follow the existing code structure
2. Update environment variables as needed
3. Test API endpoints with tools like Postman or REST Client
4. Check the ERRORS.md file for known issues and fixes

---

**Last Updated:** June 3, 2026

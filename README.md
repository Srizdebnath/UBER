# Uber Clone Frontend

## Project Overview
This is the frontend implementation of an Uber-like ride-sharing application built with React, Vite, and modern web technologies. The application provides a seamless user interface for both riders and captains, featuring real-time ride tracking, location-based services, and an intuitive booking system.

## Tech Stack
- React 19
- Vite 6
- React Router DOM 7
- TailwindCSS 4
- GSAP (GreenSock Animation Platform)
- Socket.IO Client
- Google Maps API
- Axios

## Project Structure
```
frontend/
├── src/
│   ├── components/     # Reusable UI components
│   ├── context/       # React context providers
│   ├── pages/         # Page components
│   ├── assets/        # Static assets (images, icons)
│   ├── App.jsx        # Main application component
│   ├── main.jsx       # Application entry point
│   ├── App.css        # Global styles
│   └── index.css      # Base styles
├── public/            # Public static files
├── .env              # Environment variables
├── vite.config.js    # Vite configuration
└── package.json      # Project dependencies
```

## Features
- Modern, responsive UI with TailwindCSS
- Real-time ride tracking with Socket.IO
- Interactive maps with Google Maps API
- Smooth animations with GSAP
- Protected routes with authentication
- User and Captain dashboards
- Ride booking and management interface
- Real-time location updates
- Responsive design for all devices

## Getting Started

### Prerequisites
- Node.js (v18 or higher)
- npm or yarn package manager

### Installation
1. Clone the repository
2. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```
3. Install dependencies:
   ```bash
   npm install
   # or
   yarn install
   ```

### Environment Variables
Create a `.env` file in the frontend directory with the following variables:
```
VITE_API_URL=http://localhost:5173
VITE_GOOGLE_MAPS_API_KEY=your_google_maps_api_key
```

### Development
To start the development server:
```bash
npm run dev
# or
yarn dev
```

### Building for Production
To create a production build:
```bash
npm run build
# or
yarn build
```

To preview the production build:
```bash
npm run preview
# or
yarn preview
```

## Key Components

### Authentication
- Login/Register forms for both users and captains
- JWT token management
- Protected route handling

### Maps Integration
- Interactive Google Maps implementation
- Location picker for ride requests
- Real-time captain location tracking
- Route visualization

### Ride Management
- Ride request form
- Real-time ride status updates
- Ride history
- Payment integration

### User Interface
- Modern, clean design
- Responsive layout
- Loading states and animations
- Error handling and notifications

## API Integration
The frontend communicates with the backend through RESTful APIs and WebSocket connections:

### REST APIs
- Authentication endpoints
- User/Captain profile management
- Ride booking and management
- Location services

### WebSocket Events
- Real-time ride status updates
- Captain location tracking
- Ride request notifications
- Chat functionality

## Styling
The application uses a combination of:
- TailwindCSS for utility-first styling
- GSAP for smooth animations
- Custom CSS for specific components
- Remixicon for icons

## Performance Optimization
- Code splitting with React Router
- Lazy loading of components
- Optimized assets
- Efficient state management

## Browser Support
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Contributing
1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License
This project is licensed under the MIT License - see the LICENSE file for details.
# Uber Clone Backend

## Project Overview
This is a backend implementation of an Uber-like ride-sharing application built with Node.js, Express, and MongoDB. The application provides APIs for user and captain management, real-time ride tracking, and location-based services.

## Tech Stack
- Node.js
- Express.js
- MongoDB
- Socket.IO (for real-time communication)
- JWT (for authentication)

## Project Structure
```
backend/
├── app.js                 # Main application entry point
├── server.js             # HTTP server setup
├── socket.js             # Socket.IO configuration
├── db/
│   └── db.js             # Database connection setup
├── models/
│   ├── user.model.js     # User schema and model
│   ├── captain.model.js  # Captain schema and model
│   ├── ride.model.js     # Ride schema and model
│   └── blacklistToken.model.js  # Token blacklist for logout
├── controllers/
│   ├── user.controller.js    # User-related business logic
│   ├── captain.controller.js # Captain-related business logic
│   ├── ride.controller.js    # Ride management logic
│   └── map.controller.js     # Location and mapping logic
├── routes/
│   ├── user.routes.js    # User API endpoints
│   ├── captain.routes.js # Captain API endpoints
│   ├── ride.routes.js    # Ride-related endpoints
│   └── maps.routes.js    # Location and mapping endpoints
├── services/
│   ├── user.service.js   # User-related services
│   ├── captain.service.js # Captain-related services
│   ├── ride.service.js   # Ride management services
│   └── maps.service.js   # Location and mapping services
└── middlewares/
    └── auth.middleware.js # Authentication middleware
```

## Features
- User and Captain authentication (register, login, logout)
- JWT-based authentication with token blacklisting
- Real-time location tracking for captains
- Ride booking and management system
- Location-based services and mapping
- Socket.IO integration for real-time updates

## API Documentation

### Authentication
All protected routes require a JWT token in the Authorization header:
```
Authorization: Bearer <token>
```

### User APIs

#### Register User
**Endpoint:** `POST /users/register`

**Request Body:**
```json
{
    "fullname": {
        "firstname": "string", // minimum 3 characters
        "lastname": "string"   // optional, minimum 3 characters if provided
    },
    "email": "string",        // valid email format
    "password": "string"      // minimum 6 characters
}
```

**Success Response (201):**
```json
{
    "token": "jwt_token_string",
    "user": {
        "fullname": {
            "firstname": "string",
            "lastname": "string"
        },
        "email": "string",
        "_id": "string"
    }
}
```

#### Login User
**Endpoint:** `POST /users/login`

**Request Body:**
```json
{
    "email": "string",    // valid email format
    "password": "string"  // minimum 6 characters
}
```

**Success Response (200):**
```json
{
    "token": "jwt_token_string",
    "user": {
        "fullname": {
            "firstname": "string",
            "lastname": "string"
        },
        "email": "string",
        "_id": "string"
    }
}
```

#### Get User Profile
**Endpoint:** `GET /users/profile`

**Headers Required:**
- Authorization: Bearer token

**Success Response (200):**
```json
{
    "fullname": {
        "firstname": "string",
        "lastname": "string"
    },
    "email": "string",
    "_id": "string"
}
```

#### Logout User
**Endpoint:** `GET /users/logout`

**Headers Required:**
- Authorization: Bearer token

**Success Response (200):**
```json
{
    "message": "Logged out"
}
```

### Captain APIs

#### Register Captain
**Endpoint:** `POST /captains/register`

**Request Body:**
```json
{
    "fullname": {
        "firstname": "string",  // required, minimum 3 characters
        "lastname": "string"    // optional
    },
    "email": "string",         // required, valid email format
    "password": "string",      // required, minimum 6 characters
    "vehicle": {
        "color": "string",     // required, minimum 3 characters
        "plate": "string",     // required, minimum 3 characters
        "capacity": number,    // required, minimum value of 1
        "vehicleType": "string" // required, must be 'car', 'motorcycle', or 'auto'
    }
}
```

**Success Response (201):**
```json
{
    "token": "jwt_token_string",
    "captain": {
        "fullname": {
            "firstname": "string",
            "lastname": "string"
        },
        "email": "string",
        "vehicle": {
            "color": "string",
            "plate": "string",
            "capacity": number,
            "vehicleType": "string"
        },
        "_id": "string"
    }
}
```

#### Login Captain
**Endpoint:** `POST /captains/login`

**Request Body:**
```json
{
    "email": "string",    // required, valid email format
    "password": "string"  // required, minimum 6 characters
}
```

**Success Response (200):**
```json
{
    "token": "jwt_token_string",
    "captain": {
        "fullname": {
            "firstname": "string",
            "lastname": "string"
        },
        "email": "string",
        "vehicle": {
            "color": "string",
            "plate": "string",
            "capacity": number,
            "vehicleType": "string"
        },
        "_id": "string"
    }
}
```

#### Get Captain Profile
**Endpoint:** `GET /captains/profile`

**Headers Required:**
- Authorization: Bearer token

**Success Response (200):**
```json
{
    "captain": {
        "fullname": {
            "firstname": "string",
            "lastname": "string"
        },
        "email": "string",
        "vehicle": {
            "color": "string",
            "plate": "string",
            "capacity": number,
            "vehicleType": "string"
        },
        "_id": "string"
    }
}
```

#### Logout Captain
**Endpoint:** `GET /captains/logout`

**Headers Required:**
- Authorization: Bearer token

**Success Response (200):**
```json
{
    "message": "Logout successfully"
}
```

### Ride APIs

#### Request a Ride
**Endpoint:** `POST /rides/request`

**Headers Required:**
- Authorization: Bearer token

**Request Body:**
```json
{
    "pickup": {
        "location": {
            "ltd": number,
            "lng": number
        },
        "address": "string"
    },
    "dropoff": {
        "location": {
            "ltd": number,
            "lng": number
        },
        "address": "string"
    },
    "vehicleType": "string"  // must be 'car', 'motorcycle', or 'auto'
}
```

**Success Response (201):**
```json
{
    "ride": {
        "_id": "string",
        "userId": "string",
        "status": "pending",
        "pickup": {
            "location": {
                "ltd": number,
                "lng": number
            },
            "address": "string"
        },
        "dropoff": {
            "location": {
                "ltd": number,
                "lng": number
            },
            "address": "string"
        },
        "vehicleType": "string",
        "createdAt": "timestamp"
    }
}
```

#### Get Ride Status
**Endpoint:** `GET /rides/:rideId/status`

**Headers Required:**
- Authorization: Bearer token

**Success Response (200):**
```json
{
    "status": "string",  // pending, accepted, in-progress, completed, cancelled
    "captain": {
        "fullname": {
            "firstname": "string",
            "lastname": "string"
        },
        "vehicle": {
            "color": "string",
            "plate": "string",
            "vehicleType": "string"
        }
    },
    "location": {
        "ltd": number,
        "lng": number
    }
}
```

#### Accept Ride (Captain)
**Endpoint:** `POST /rides/:rideId/accept`

**Headers Required:**
- Authorization: Bearer token

**Success Response (200):**
```json
{
    "message": "Ride accepted successfully",
    "ride": {
        "_id": "string",
        "status": "accepted",
        "captainId": "string"
    }
}
```

#### Complete Ride (Captain)
**Endpoint:** `POST /rides/:rideId/complete`

**Headers Required:**
- Authorization: Bearer token

**Success Response (200):**
```json
{
    "message": "Ride completed successfully",
    "ride": {
        "_id": "string",
        "status": "completed"
    }
}
```

### Maps APIs

#### Get Nearby Captains
**Endpoint:** `GET /maps/nearby-captains`

**Headers Required:**
- Authorization: Bearer token

**Query Parameters:**
- `ltd`: number (latitude)
- `lng`: number (longitude)
- `radius`: number (in kilometers, default: 5)

**Success Response (200):**
```json
{
    "captains": [
        {
            "_id": "string",
            "fullname": {
                "firstname": "string",
                "lastname": "string"
            },
            "vehicle": {
                "color": "string",
                "plate": "string",
                "vehicleType": "string"
            },
            "location": {
                "ltd": number,
                "lng": number
            },
            "distance": number  // in kilometers
        }
    ]
}
```

#### Update Captain Location
**Endpoint:** `POST /maps/update-location`

**Headers Required:**
- Authorization: Bearer token

**Request Body:**
```json
{
    "location": {
        "ltd": number,
        "lng": number
    }
}
```

**Success Response (200):**
```json
{
    "message": "Location updated successfully",
    "location": {
        "ltd": number,
        "lng": number
    }
}
```

### Error Responses
All endpoints may return the following error responses:

**400 Bad Request:**
```json
{
    "errors": [
        {
            "msg": "Error message",
            "param": "field_name",
            "location": "body"
        }
    ]
}
```

**401 Unauthorized:**
```json
{
    "message": "Authentication required"
}
```

**403 Forbidden:**
```json
{
    "message": "Access denied"
}
```

**404 Not Found:**
```json
{
    "message": "Resource not found"
}
```

**500 Internal Server Error:**
```json
{
    "message": "Internal server error"
}
```

### Socket.IO Events

#### Client Events
- `join`: Join a room with user/captain ID
- `update-location-captain`: Update captain's location
- `disconnect`: Handle client disconnection

#### Server Events
- `ride-request`: Notify nearby captains of new ride requests
- `ride-accepted`: Notify user when ride is accepted
- `location-update`: Update user with captain's location
- `ride-completed`: Notify user when ride is completed

### Environment Variables
Create a `.env` file in the root directory with the following variables:
```
PORT=4000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key
```

# 💬 Real-Time Chat Application

A full-stack real-time chat application built with React, Node.js, Express, Socket.io, and PostgreSQL. Features include user authentication, real-time messaging, online/offline status tracking, and message history.

## ✨ Features

- **User Authentication**: Secure registration and login with JWT tokens
- **Real-Time Messaging**: Instant message delivery using WebSocket (Socket.io)
- **Online Status**: See who's online in real-time
- **Message History**: Persistent chat history stored in PostgreSQL
- **Typing Indicators**: Visual feedback when someone is typing
- **Responsive Design**: Clean, modern UI that works on all devices
- **Message Read Receipts**: Track message delivery and read status

## 🛠️ Tech Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **Socket.io** - Real-time bidirectional communication
- **PostgreSQL** - Database
- **JWT** - Authentication
- **bcrypt** - Password hashing

### Frontend
- **React** - UI library
- **React Router** - Navigation
- **Socket.io-client** - WebSocket client
- **Axios** - HTTP client
- **CSS3** - Styling

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (v14 or higher)
- PostgreSQL (v12 or higher)
- npm or yarn

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd chat-application
```

### 2. Backend Setup

```bash
# Navigate to server directory
cd server

# Install dependencies
npm install

# Create .env file
touch .env
```

Add the following to your `.env` file:

```env
# Database Configuration
DB_USER=chatuser
DB_HOST=localhost
DB_NAME=chatapp
DB_PASSWORD=your_password_here
DB_PORT=5432

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key_here
JWT_EXPIRES_IN=7d

# Server Configuration
PORT=5000
CLIENT_URL=http://localhost:3000
```

### 3. Database Setup

```bash
# Create PostgreSQL database
createdb chatapp

# Or using psql:
psql -U postgres
CREATE DATABASE chatapp;
\q

# Run the table creation script
node createTables.js
```

### 4. Frontend Setup

```bash
# Navigate to client directory
cd ../client

# Install dependencies
npm install
```

## 🎯 Running the Application

### Start the Backend Server

```bash
cd server
npm start

# For development with auto-reload:
npm run dev  # (requires nodemon)
```

Server will run on `http://localhost:5000`

### Start the Frontend

```bash
cd client
npm start
```

Frontend will run on `http://localhost:3000`

## 📁 Project Structure

```
chat-application/
├── server/
│   ├── routes/
│   │   ├── auth.js          # Authentication routes
│   │   ├── users.js         # User management routes
│   │   └── messages.js      # Message routes
│   ├── middleware/
│   │   └── auth.js          # JWT authentication middleware
│   ├── db.js                # Database connection
│   ├── index.js             # Main server file with Socket.io
│   ├── createTables.js      # Database schema setup
│   └── package.json
│
└── client/
    ├── src/
    │   ├── components/
    │   │   ├── UserList.js      # User list sidebar
    │   │   ├── ChatWindow.js    # Main chat interface
    │   │   └── Message.js       # Individual message component
    │   ├── pages/
    │   │   ├── Login.js         # Login page
    │   │   ├── Register.js      # Registration page
    │   │   └── Chat.js          # Main chat page
    │   ├── services/
    │   │   ├── api.js           # HTTP API calls
    │   │   └── socket.js        # Socket.io service
    │   ├── utils/
    │   │   └── AuthContext.js   # Authentication context
    │   └── App.js
    └── package.json
```

## 🔌 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user

### Users
- `GET /api/users/me` - Get current user profile (protected)
- `GET /api/users/:id` - Get user by ID (protected)

### Messages
- `GET /api/messages/history/:otherUserId` - Get message history (protected)
- `POST /api/messages/read` - Mark messages as read (protected)
- `GET /api/messages/unread/count` - Get unread message count (protected)

## 🔌 WebSocket Events

### Client → Server
- `message:send` - Send a message
- `typing:start` - User started typing
- `typing:stop` - User stopped typing

### Server → Client
- `message:receive` - Receive a new message
- `message:sent` - Confirmation of sent message
- `user:online` - User came online
- `user:offline` - User went offline
- `typing:start` - Other user started typing
- `typing:stop` - Other user stopped typing

## 🗄️ Database Schema

### Users Table
```sql
- id (SERIAL PRIMARY KEY)
- username (VARCHAR UNIQUE)
- email (VARCHAR UNIQUE)
- password_hash (VARCHAR)
- first_name (VARCHAR)
- last_name (VARCHAR)
- status_text (VARCHAR)
- phone_number (VARCHAR)
- created_at (TIMESTAMP)
- last_seen (TIMESTAMP)
- is_online (BOOLEAN)
```

### Messages Table
```sql
- id (SERIAL PRIMARY KEY)
- sender_id (INTEGER FK → users.id)
- receiver_id (INTEGER FK → users.id)
- content (TEXT)
- sent_at (TIMESTAMP)
- read_at (TIMESTAMP)
```

## 🧪 Testing

### Test Database Connection
```bash
cd server
node testDb.js
```

### Test WebSocket Connection
Open `server/test-client.html` in your browser to test WebSocket functionality.

## 🔒 Security Features

- Passwords hashed with bcrypt (10 salt rounds)
- JWT token-based authentication
- Protected API routes with authentication middleware
- CORS configuration for secure cross-origin requests
- SQL injection prevention with parameterized queries

## 🎨 UI Features

- Clean, modern interface with gradient backgrounds
- Smooth animations and transitions
- Real-time status indicators
- Message timestamps
- Responsive design for mobile and desktop
- Custom scrollbars

## 🚧 Future Enhancements

- [ ] Group chat functionality
- [ ] File and image sharing
- [ ] Voice/video calling
- [ ] Message search
- [ ] User profiles with avatars
- [ ] Push notifications
- [ ] Message reactions/emojis
- [ ] Dark mode
- [ ] End-to-end encryption
- [ ] Message editing and deletion

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is open source and available under the [ISC License](LICENSE).

## 👤 Author

Your Name

## 🙏 Acknowledgments

- Socket.io for real-time communication
- React team for the amazing framework
- PostgreSQL community
- Express.js team

---

**Note**: This is a learning project. For production use, additional security measures, error handling, and optimizations should be implemented.

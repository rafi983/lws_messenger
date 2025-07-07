# Chat Application Server

A real-time chat application backend built with Node.js, Express, JSON Server, and Socket.IO.

## 🚀 Features

- **Authentication System**: User registration and login with JWT tokens
- **Real-time Messaging**: WebSocket-based real-time communication using Socket.IO
- **RESTful API**: JSON Server with custom authentication middleware
- **Database**: JSON-based database for development and testing
- **CORS Support**: Cross-origin resource sharing enabled
- **Auto-reload**: Development server with nodemon for automatic restarts

## 🛠️ Tech Stack

- **Node.js**: Runtime environment
- **Express.js**: Web application framework
- **JSON Server**: Full fake REST API
- **JSON Server Auth**: Authentication middleware for JSON Server
- **Socket.IO**: Real-time bidirectional event-based communication
- **bcrypt**: Password hashing (via json-server-auth)

## 📦 Installation

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn package manager

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone <your-repository-url>
   cd lws_chat-app/server
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the development server**
   ```bash
   npm start
   ```

The server will start on `http://localhost:9000` by default.

## 🔧 Configuration

### Environment Variables

Create a `.env` file in the server directory (optional):

```env
PORT=9000
NODE_ENV=development
```

### Database Structure

The `db.json` file contains the following collections:

- **users**: User accounts with authentication
- **conversations**: Chat conversations between users
- **messages**: Individual messages within conversations

## 📚 API Documentation

### Base URL
```
http://localhost:9000
```

### Authentication Endpoints

#### Register User
```http
POST /register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123",
  "name": "User Name"
}
```

#### Login User
```http
POST /login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123"
}
```

### Protected Endpoints

All endpoints below require authentication header:
```http
Authorization: Bearer <your-jwt-token>
```

#### Users

- **GET /users**: Get all users (except current user)
- **GET /users/:id**: Get specific user
- **PATCH /users/:id**: Update user profile

#### Conversations

- **GET /conversations**: Get user's conversations
- **POST /conversations**: Create new conversation
- **PATCH /conversations/:id**: Update conversation
- **GET /conversations/:id**: Get specific conversation

#### Messages

- **GET /messages**: Get all messages
- **GET /messages?conversationId=:id**: Get messages by conversation
- **POST /messages**: Send new message
- **PATCH /messages/:id**: Update message
- **DELETE /messages/:id**: Delete message

### Query Parameters

#### Pagination
```http
GET /conversations?_page=1&_limit=10
GET /messages?_page=1&_limit=20
```

#### Sorting
```http
GET /conversations?_sort=timestamp&_order=desc
GET /messages?_sort=timestamp&_order=asc
```

#### Filtering
```http
GET /messages?conversationId=1
GET /users?email_ne=current-user@example.com
```

## 🔌 WebSocket Events

### Client to Server Events

- **connection**: Client connects to server
- **disconnect**: Client disconnects from server

### Server to Client Events

- **conversation**: Emitted when conversation is created or updated
  ```javascript
  {
    data: {
      id: 1,
      participants: "user1@example.com-user2@example.com",
      users: [...],
      message: "Latest message",
      timestamp: 1662704970215
    }
  }
  ```

## 🔒 Authentication & Authorization

### Permission Levels

- **Public**: `/register`, `/login`
- **User (640)**: Can read/write own data
- **Conversations (660)**: Read/write access to conversations
- **Messages (660)**: Read/write access to messages

### JWT Token Structure

Tokens include:
- User ID
- Email
- Expiration time
- Issued at time

## 🚀 Deployment

### Heroku Deployment

1. **Prepare for deployment**
   ```bash
   # Copy server folder to a separate directory
   cp -r server/ ../chat-app-server/
   cd ../chat-app-server/
   ```

2. **Initialize Git repository**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   ```

3. **Create Heroku app**
   ```bash
   heroku create your-app-name
   ```

4. **Deploy to Heroku**
   ```bash
   git push heroku main
   ```

5. **Set environment variables**
   ```bash
   heroku config:set NODE_ENV=production
   ```

### Railway/Render Deployment

1. Connect your GitHub repository
2. Set build command: `npm install`
3. Set start command: `npm start`
4. Set environment variables as needed

### Docker Deployment

Create `Dockerfile`:
```dockerfile
FROM node:16-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 9000
CMD ["npm", "start"]
```

## 🐛 Troubleshooting

### Common Issues

1. **Port already in use**
   - Change PORT in environment variables
   - Kill existing process: `npx kill-port 9000`

2. **CORS errors**
   - Ensure client URL is properly configured
   - Check CORS middleware setup

3. **Authentication failures**
   - Verify JWT token format
   - Check token expiration
   - Ensure proper Authorization header

4. **Socket connection issues**
   - Verify WebSocket URL in client
   - Check firewall settings
   - Ensure proper CORS configuration

## 📝 Development Notes

### File Structure
```
server/
├── db.json          # JSON database
├── server.js        # Main server file
├── package.json     # Dependencies and scripts
└── README.md        # This file
```

### Adding New Endpoints

To add custom endpoints, modify `server.js`:

```javascript
// Custom middleware before router
app.use('/custom-endpoint', (req, res) => {
  // Your custom logic here
  res.json({ message: 'Custom response' });
});
```

### Database Modifications

Edit `db.json` directly or use the REST API to modify data. The server will automatically detect changes.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License.

## 📞 Support

For support and questions:
- Create an issue in the repository
- Contact: Learn with Sumit team

---

# 🚀 Anonymous Room-Based Real-Time Collaboration Platform

A lightweight, anonymous real-time collaboration platform for students. No login required - just enter a nickname and start collaborating!

## ✨ Features

- **Anonymous Access** - No authentication required
- **Room-Based System** - 6-character room codes
- **Real-Time Messaging** - Instant text and code sharing
- **Code Snippet Support** - Share formatted code with `/code` prefix
- **In-Memory Storage** - Fast, simple, no database setup
- **Rate Limiting** - 1 message per second per user
- **Room Capacity** - Up to 60 users per room
- **Responsive Design** - Works on desktop and mobile

## 🏗️ Tech Stack

### Backend
- **Node.js** - Runtime environment
- **Express** - Web framework
- **Socket.io** - Real-time bidirectional communication
- **In-Memory Storage** - No database required for MVP

### Frontend
- **React 18** - UI library
- **Vite** - Build tool and dev server
- **Socket.io Client** - WebSocket client
- **CSS3** - Modern styling with animations

## 📁 Project Structure

```
collab-platform/
├── backend/
│   ├── server.js           # Main server & Socket.io logic
│   ├── roomManager.js      # In-memory room management
│   ├── validators.js       # Input validation
│   ├── package.json
│   └── README.md
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── HomePage.jsx
│   │   │   ├── RoomPage.jsx
│   │   │   ├── ChatWindow.jsx
│   │   │   ├── Message.jsx
│   │   │   └── InputBox.jsx
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css
│   ├── index.html
│   ├── vite.config.js
│   ├── package.json
│   └── README.md
│
└── README.md (this file)
```

## 🚀 Quick Start

### Prerequisites
- Node.js 16+ installed
- npm or yarn package manager

### Installation

1. **Clone or download the project**
   ```bash
   cd collab-platform
   ```

2. **Install backend dependencies**
   ```bash
   cd backend
   npm install
   ```

3. **Install frontend dependencies**
   ```bash
   cd ../frontend
   npm install
   ```

### Running the Application

1. **Start the backend server** (Terminal 1)
   ```bash
   cd backend
   npm start
   ```
   Server will run on `http://localhost:3000`

2. **Start the frontend dev server** (Terminal 2)
   ```bash
   cd frontend
   npm run dev
   ```
   Frontend will run on `http://localhost:5173`

3. **Open your browser**
   Navigate to `http://localhost:5173`

## 📖 Usage Guide

### Creating a Room
1. Enter your nickname (max 20 characters)
2. Click **"Create Room"** button
3. Share the generated 6-character room code with others
4. Start collaborating!

### Joining a Room
1. Enter your nickname
2. Enter the 6-character room code
3. Click **"Join Room"** button
4. You're in!

### Sending Messages

**Text Messages:**
- Just type and press Enter
- Max 1,000 characters
- Supports multi-line (Shift+Enter)

**Code Messages:**
- Start with `/code ` prefix
- Example: `/code console.log('Hello World');`
- Max 15,000 characters
- Displayed with code formatting

### Room Features
- **Room Code Display** - Click to copy to clipboard
- **User Count** - See active participants
- **System Notifications** - User join/leave alerts
- **Auto-scroll** - Always see latest messages
- **Leave Room** - Return to home page

## 🔧 Configuration

### Backend Port
Edit `backend/server.js`:
```javascript
const PORT = process.env.PORT || 3000;
```

### Frontend Socket URL
Edit `frontend/src/components/RoomPage.jsx`:
```javascript
const SOCKET_URL = 'http://localhost:3000';
```

### Room Settings
Edit `backend/roomManager.js`:
```javascript
this.MAX_USERS_PER_ROOM = 60;
```

### Message Limits
Edit `backend/validators.js`:
```javascript
const MAX_NICKNAME_LENGTH = 20;
const MAX_TEXT_MESSAGE_LENGTH = 1000;
const MAX_CODE_MESSAGE_LENGTH = 15000;
```

## 🛡️ Security Features

- **Input Validation** - All user inputs validated
- **Rate Limiting** - 1 message per second per user
- **Room Code Format** - Enforced 6-character alphanumeric
- **Message Size Limits** - Prevents oversized messages
- **Nickname Uniqueness** - Per room enforcement
- **XSS Prevention** - React's built-in escaping

## 📊 API Reference

### Socket.io Events

#### Client → Server

**joinRoom**
```javascript
socket.emit('joinRoom', { roomCode, nickname }, (response) => {
  // response: { success: boolean, roomInfo?: object, error?: string }
});
```

**sendMessage**
```javascript
socket.emit('sendMessage', { type: 'text' | 'code', content: string }, (response) => {
  // response: { success: boolean, error?: string }
});
```

**leaveRoom**
```javascript
socket.emit('leaveRoom', (response) => {
  // response: { success: boolean }
});
```

#### Server → Client

**newMessage**
```javascript
socket.on('newMessage', (message) => {
  // message: { type, nickname, content, timestamp }
});
```

**userJoined**
```javascript
socket.on('userJoined', (data) => {
  // data: { nickname, userCount, timestamp }
});
```

**userLeft**
```javascript
socket.on('userLeft', (data) => {
  // data: { nickname, userCount, timestamp }
});
```

## 🎯 MVP Scope

### Included ✅
- Anonymous access with nickname
- Room creation and joining
- Real-time text messaging
- Code snippet sharing
- In-memory room storage
- Rate limiting
- Input validation
- Responsive UI

### Not Included ❌
- User authentication
- Persistent storage/database
- Message history persistence
- File uploads
- Video/Audio chat
- User profiles
- Private messaging
- Room passwords

## 🚧 Known Limitations

- **Room Persistence** - Rooms disappear when server restarts
- **Message History** - Not saved after users disconnect
- **Horizontal Scaling** - Single server instance only
- **Browser Compatibility** - Modern browsers only (ES6+)

## 📝 Development Notes

### Code Style
- Functional React components
- Clear, descriptive variable names
- Comprehensive comments
- Modular architecture
- ES6+ JavaScript

### Best Practices Followed
- Single Responsibility Principle
- Component-based architecture
- Separation of concerns
- Input validation on both client and server
- Error handling with user feedback
- Graceful degradation

## 🔄 Future Enhancements (Post-MVP)

- [ ] Room persistence with Redis
- [ ] Message history (last N messages)
- [ ] User typing indicators
- [ ] Room passwords (optional)
- [ ] Admin controls (kick users)
- [ ] File sharing
- [ ] Emoji support
- [ ] Markdown support
- [ ] Dark mode
- [ ] User avatars
- [ ] @ mentions
- [ ] Message reactions

## 🐛 Troubleshooting

### Backend won't start
- Check if port 3000 is already in use
- Verify Node.js version (16+)
- Run `npm install` again

### Frontend can't connect
- Verify backend is running
- Check SOCKET_URL in RoomPage.jsx
- Check CORS settings in backend

### Messages not sending
- Check browser console for errors
- Verify rate limit (1 msg/second)
- Check message length limits

## 📄 License

This is an MVP educational project. Feel free to use and modify as needed.

## 👥 Contributing

This is an MVP template. To extend:
1. Fork the project
2. Create feature branch
3. Commit changes
4. Push to branch
5. Open pull request

## 📧 Support

For issues and questions, please check:
- Backend logs in terminal
- Browser console (F12)
- Network tab for Socket.io connection
- README files in backend/ and frontend/

---

**Built with ❤️ for student collaboration**

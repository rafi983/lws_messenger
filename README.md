# LWS Messenger

A modern, real-time chat application built with React, Redux Toolkit, and Socket.IO. This application provides a seamless messaging experience with user authentication, real-time updates, and a responsive UI.

## 🚀 Features

### Core Features
- **User Authentication**: Secure registration and login system
- **Real-time Messaging**: Instant message delivery using WebSocket
- **Conversation Management**: Create and manage chat conversations
- **Infinite Scroll**: Load more messages and conversations dynamically
- **Responsive Design**: Mobile-first design with Tailwind CSS
- **Persistent Login**: Auto-login with localStorage persistence
- **User Discovery**: Find and start conversations with other users
- **Message Status**: Real-time message delivery indicators

### Technical Features
- **State Management**: Redux Toolkit with RTK Query for efficient data fetching
- **Real-time Updates**: Socket.IO integration for live chat updates
- **Optimistic Updates**: Immediate UI feedback with automatic error handling
- **Caching**: Smart caching strategies for improved performance
- **Route Protection**: Protected and public routes with authentication guards
- **Error Handling**: Comprehensive error handling and user feedback

## 🛠️ Tech Stack

### Frontend Framework
- **React 18**: Modern React with hooks and concurrent features
- **React Router DOM v6**: Client-side routing with protected routes
- **React Redux**: Official React bindings for Redux

### State Management
- **Redux Toolkit**: Modern Redux with simplified syntax
- **RTK Query**: Powerful data fetching and caching solution

### Styling & UI
- **Tailwind CSS**: Utility-first CSS framework
- **Tailwind Forms**: Beautiful form components
- **Responsive Design**: Mobile-first approach

### Real-time Features
- **Socket.IO Client**: Real-time bidirectional communication
- **React Infinite Scroll**: Smooth infinite scrolling experience

### Utilities
- **Moment.js**: Date and time manipulation
- **Gravatar URL**: Dynamic avatar generation
- **Custom Hooks**: Reusable authentication and utility hooks

## 📦 Installation

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn package manager
- Running backend server (see `/server` directory)

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone <your-repository-url>
   cd lws_chat-app
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Environment Configuration**
   
   Create a `.env` file in the root directory:
   ```env
   REACT_APP_API_URL=http://localhost:9000
   REACT_APP_SOCKET_URL=http://localhost:9000
   ```

4. **Start the development server**
   ```bash
   npm start
   ```

   The application will open at `http://localhost:3000`

## 🏗️ Project Structure

```
src/
├── components/           # Reusable UI components
│   ├── PrivateRoute.js  # Protected route wrapper
│   ├── PublicRoute.js   # Public route wrapper
│   ├── inbox/           # Inbox-related components
│   │   ├── Navigation.js
│   │   ├── Sidebar.js
│   │   ├── ChatItem.js
│   │   ├── Modal.js
│   │   └── chatbody/    # Chat interface components
│   └── ui/              # Generic UI components
├── features/            # Feature-based Redux slices
│   ├── api/             # API configuration
│   ├── auth/            # Authentication logic
│   ├── conversations/   # Conversation management
│   ├── messages/        # Message handling
│   └── users/           # User management
├── hooks/               # Custom React hooks
├── pages/               # Route components
├── utils/               # Utility functions
└── assets/              # Static assets
```

## 🔧 Configuration

### Environment Variables

```env
# API Configuration
REACT_APP_API_URL=http://localhost:9000          # Backend API URL
REACT_APP_SOCKET_URL=http://localhost:9000       # Socket.IO server URL

# Optional: Development flags
REACT_APP_DEBUG=true
REACT_APP_ENABLE_LOGS=true
```

### Tailwind Configuration

The project uses Tailwind CSS with custom configurations:

```javascript
// tailwind.config.js
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {
      // Custom theme extensions
    },
  },
  plugins: [
    require('@tailwindcss/forms'),
  ],
}
```

## 🚀 Usage Guide

### Getting Started

1. **Register a new account** or **login** with existing credentials
2. **Browse users** in the sidebar to start new conversations
3. **Click on a user** to open a chat conversation
4. **Send messages** in real-time with other users
5. **Scroll up** in conversations to load message history

### Key Features Usage

#### Authentication
- Automatic redirect to login if not authenticated
- Persistent login across browser sessions
- Secure token-based authentication

#### Real-time Messaging
- Messages appear instantly without page refresh
- Online status indicators for users
- Typing indicators (if implemented)

#### Conversation Management
- Create new conversations by clicking on users
- Load more conversations with infinite scroll
- Latest conversations appear at the top

#### Message History
- Load previous messages by scrolling up
- Efficient pagination with RTK Query caching
- Smooth loading states and transitions

## 🔌 API Integration

### RTK Query Setup

The application uses RTK Query for efficient data fetching:

```javascript
// features/api/apiSlice.js
export const apiSlice = createApi({
  reducerPath: "api",
  baseQuery: fetchBaseQuery({
    baseUrl: process.env.REACT_APP_API_URL,
    prepareHeaders: (headers, { getState }) => {
      const token = getState()?.auth?.accessToken;
      if (token) {
        headers.set("Authorization", `Bearer ${token}`);
      }
      return headers;
    },
  }),
  // ... tag types and endpoints
});
```

### Authentication Flow

1. User submits login/register form
2. API call made with credentials
3. JWT token stored in Redux state and localStorage
4. Token included in subsequent API requests
5. Automatic logout on token expiration

### Real-time Updates

Socket.IO integration for live updates:

```javascript
// Real-time conversation updates
useEffect(() => {
  socket.on("conversation", (data) => {
    // Update conversation in Redux store
    dispatch(conversationUpdated(data));
  });
}, [socket, dispatch]);
```

## 🎨 UI/UX Features

### Responsive Design
- Mobile-first approach with Tailwind CSS
- Adaptive layouts for desktop, tablet, and mobile
- Touch-friendly interface elements

### User Experience
- Loading states for all async operations
- Error boundaries and graceful error handling
- Optimistic updates for instant feedback
- Smooth animations and transitions

### Accessibility
- Semantic HTML structure
- Keyboard navigation support
- Screen reader friendly
- High contrast color schemes

## 🧪 Available Scripts

### Development
```bash
npm start          # Start development server
npm test           # Run test suite
npm run build      # Build for production
npm run eject      # Eject from Create React App
```

### Code Quality
```bash
npm run lint       # Run ESLint
npm run format     # Format code with Prettier
npm run type-check # Run TypeScript checks (if applicable)
```

## 🚀 Deployment

### Build for Production

```bash
npm run build
```

This creates an optimized production build in the `build` folder.

### Environment-specific Builds

For different environments, create corresponding `.env` files:

```bash
.env.development     # Development environment
.env.production      # Production environment
.env.staging         # Staging environment
```

### Deployment Platforms

#### Netlify
1. Build command: `npm run build`
2. Publish directory: `build`
3. Set environment variables in Netlify dashboard

#### Vercel
1. Connect GitHub repository
2. Set build command: `npm run build`
3. Set output directory: `build`
4. Configure environment variables

#### Firebase Hosting
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
npm run build
firebase deploy
```

#### Traditional Web Servers
1. Run `npm run build`
2. Upload `build` folder contents to web server
3. Configure server for SPA routing (redirect all routes to `index.html`)

## 🔧 Customization

### Adding New Features

1. **Create feature slice**:
   ```bash
   src/features/newFeature/
   ├── newFeatureApi.js
   ├── newFeatureSlice.js
   └── index.js
   ```

2. **Add to store configuration**:
   ```javascript
   // app/store.js
   import { newFeatureApi } from '../features/newFeature/newFeatureApi';
   ```

3. **Create components**:
   ```bash
   src/components/newFeature/
   ├── NewFeatureComponent.js
   └── index.js
   ```

### Styling Customization

#### Custom Tailwind Classes
```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        'brand-primary': '#your-color',
        'brand-secondary': '#your-color',
      },
      fontFamily: {
        'custom': ['Your Font', 'sans-serif'],
      },
    },
  },
};
```

#### Component Styling
```javascript
// Example component with Tailwind classes
const ChatBubble = ({ message, isOwn }) => (
  <div className={`
    max-w-md p-3 rounded-lg mb-2
    ${isOwn 
      ? 'bg-blue-500 text-white ml-auto' 
      : 'bg-gray-200 text-gray-800 mr-auto'
    }
  `}>
    {message}
  </div>
);
```

## 🐛 Troubleshooting

### Common Issues

#### 1. API Connection Problems
- **Issue**: Cannot connect to backend server
- **Solution**: 
  - Verify backend server is running on correct port
  - Check `REACT_APP_API_URL` in `.env` file
  - Ensure CORS is properly configured on backend

#### 2. Authentication Issues
- **Issue**: Login not persisting across sessions
- **Solution**:
  - Check localStorage for stored token
  - Verify token expiration in backend
  - Clear localStorage and re-login

#### 3. Real-time Updates Not Working
- **Issue**: Messages not appearing in real-time
- **Solution**:
  - Check Socket.IO connection in browser DevTools
  - Verify `REACT_APP_SOCKET_URL` configuration
  - Ensure WebSocket ports are not blocked

#### 4. Build Errors
- **Issue**: Build fails with dependency errors
- **Solution**:
  ```bash
  # Clear node_modules and reinstall
  rm -rf node_modules package-lock.json
  npm install
  
  # Or use yarn
  rm -rf node_modules yarn.lock
  yarn install
  ```

### Performance Optimization

#### Bundle Size Analysis
```bash
npm install -g webpack-bundle-analyzer
npm run build
npx webpack-bundle-analyzer build/static/js/*.js
```

#### Code Splitting
```javascript
// Lazy load route components
const Login = lazy(() => import('./pages/Login'));
const Inbox = lazy(() => import('./pages/Inbox'));

// Wrap in Suspense
<Suspense fallback={<div>Loading...</div>}>
  <Routes>
    <Route path="/login" element={<Login />} />
    <Route path="/inbox" element={<Inbox />} />
  </Routes>
</Suspense>
```

## 📝 Development Guidelines

### Code Style
- Use functional components with hooks
- Implement proper error boundaries
- Follow Redux Toolkit patterns
- Use TypeScript for type safety (optional)

### State Management
- Keep local state in components when possible
- Use Redux for global state and complex logic
- Implement proper loading and error states
- Use RTK Query for server state management

### Testing Strategy
- Unit tests for utility functions
- Component tests with React Testing Library
- Integration tests for user flows
- E2E tests for critical paths

## 🤝 Contributing

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Make your changes**: Follow the coding guidelines
4. **Write tests**: Ensure your changes are well tested
5. **Commit your changes**: `git commit -m 'Add some amazing feature'`
6. **Push to the branch**: `git push origin feature/amazing-feature`
7. **Open a Pull Request**: Describe your changes clearly

### Development Workflow
1. Check existing issues and create new ones if needed
2. Discuss major changes in issues before implementation
3. Follow the existing code style and patterns
4. Write meaningful commit messages
5. Update documentation as needed

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Learn with Sumit**: Original course and tutorial content
- **Redux Toolkit Team**: For excellent state management tools
- **React Team**: For the amazing React framework
- **Tailwind CSS**: For the utility-first CSS framework
- **Socket.IO**: For real-time communication capabilities

## 📞 Support & Contact

- **Documentation**: Check this README and inline code comments
- **Issues**: Create an issue in the GitHub repository
- **Discussions**: Use GitHub Discussions for questions and ideas
- **Course Support**: Visit [Learn with Sumit](https://learnwithsumit.com) for course-related queries

---

**Happy Coding! 🚀**

For more advanced features and deployment strategies, check the server documentation in the `/server` directory.

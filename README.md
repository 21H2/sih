# 🌐 WhatsApp Medical AI Chatbot - Frontend

> Modern web interface for managing and monitoring your WhatsApp medical chatbot with real-time analytics and conversation management.

[![React](https://img.shields.io/badge/React-18+-blue.svg)](https://reactjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5+-blue.svg)](https://typescriptlang.org)
[![Tailwind](https://img.shields.io/badge/Tailwind-3+-green.svg)](https://tailwindcss.com)
[![Vite](https://img.shields.io/badge/Vite-4+-purple.svg)](https://vitejs.dev)

## 🚀 Quick Start

```bash
# Clone and setup
git clone <your-repo>
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

## ✨ Features

- 📊 **Real-time Dashboard** - Monitor chatbot performance and usage
- 💬 **Conversation Manager** - View and manage WhatsApp conversations
- 📈 **Analytics & Insights** - User engagement and response metrics
- ⚙️ **Bot Configuration** - Update responses and model settings
- 🏥 **Medical Data Viewer** - Browse medical knowledge base
- 📱 **Responsive Design** - Works on desktop, tablet, and mobile
- 🔐 **Admin Authentication** - Secure access to management features
- 🌙 **Dark/Light Mode** - User preference themes

## 🏗️ Architecture

```
┌─────────────────┐    ┌──────────────┐    ┌─────────────────┐
│   React App     │───▶│   REST API   │───▶│   Backend       │
│   Dashboard     │    │   Endpoints  │    │   Flask App     │
└─────────────────┘    └──────────────┘    └─────────────────┘
         │                       │                    │
         ▼                       ▼                    ▼
┌─────────────────┐    ┌──────────────┐    ┌─────────────────┐
│   WebSocket     │    │   Database   │    │   WhatsApp      │
│   Real-time     │    │   Chat Logs  │    │   Twilio API    │
└─────────────────┘    └──────────────┘    └─────────────────┘
```

## 📁 Project Structure

```
frontend/
├── src/
│   ├── components/          # Reusable UI components
│   │   ├── Dashboard/       # Dashboard widgets
│   │   ├── Chat/           # Chat interface components
│   │   ├── Analytics/      # Charts and metrics
│   │   └── Common/         # Shared components
│   ├── pages/              # Main application pages
│   │   ├── Dashboard.tsx   # Main dashboard
│   │   ├── Conversations.tsx # Chat management
│   │   ├── Analytics.tsx   # Usage analytics
│   │   ├── Settings.tsx    # Bot configuration
│   │   └── Login.tsx       # Authentication
│   ├── hooks/              # Custom React hooks
│   ├── services/           # API service functions
│   ├── utils/              # Utility functions
│   ├── types/              # TypeScript type definitions
│   └── styles/             # Global styles and themes
├── public/                 # Static assets
├── package.json           # Dependencies and scripts
├── vite.config.ts         # Vite configuration
├── tailwind.config.js     # Tailwind CSS config
├── tsconfig.json          # TypeScript configuration
└── README.md              # This file
```

## 🛠️ Installation

### Prerequisites
- Node.js 18+
- npm or yarn
- Backend API running

### Development Setup
```bash
# Install dependencies
npm install

# Setup environment variables
cp .env.example .env.local
# Edit .env.local with your API endpoints

# Start development server
npm run dev
```

### Production Build
```bash
# Build for production
npm run build

# Preview production build
npm run preview

# Deploy to Vercel/Netlify
npm run deploy
```

## ⚙️ Configuration

### Environment Variables
```bash
# .env.local
VITE_API_BASE_URL=https://your-backend.herokuapp.com
VITE_WEBSOCKET_URL=wss://your-backend.herokuapp.com
VITE_APP_TITLE=Medical AI Chatbot
VITE_ENABLE_ANALYTICS=true
```

### API Integration
The frontend connects to your backend Flask app:
- **Base URL**: Your deployed backend URL
- **Authentication**: JWT tokens for admin access
- **WebSocket**: Real-time updates for conversations

## 📊 Dashboard Features

### Main Dashboard
- 📈 **Usage Statistics**: Messages per day, active users
- 🕒 **Response Times**: Average bot response time
- 🎯 **Popular Queries**: Most common medical questions
- 🚨 **System Health**: Backend status and model performance

### Conversation Manager
- 💬 **Live Conversations**: Real-time chat monitoring
- 📝 **Message History**: Search and filter past conversations
- 🏷️ **User Analytics**: User engagement patterns
- 📋 **Export Data**: Download conversation logs

### Analytics Page
- 📊 **Interactive Charts**: Usage trends and patterns
- 🗺️ **Geographic Data**: User locations (if available)
- 🕐 **Time Analysis**: Peak usage hours and days
- 📈 **Growth Metrics**: User acquisition and retention

### Settings Panel
- 🤖 **Bot Responses**: Customize greeting and error messages
- 🏥 **Medical Disclaimers**: Update safety warnings
- ⚙️ **Model Settings**: Adjust AI confidence thresholds
- 🔔 **Notifications**: Configure admin alerts

## 🎨 UI Components

### Dashboard Widgets
```tsx
// Example usage
import { MetricCard, ChartWidget, ConversationList } from '@/components/Dashboard';

<MetricCard 
  title="Total Messages" 
  value={1234} 
  trend="+12%" 
  icon="💬" 
/>
```

### Chat Interface
```tsx
// Real-time chat component
import { ChatInterface } from '@/components/Chat';

<ChatInterface 
  conversations={conversations}
  onSendMessage={handleSendMessage}
  realTime={true}
/>
```

## 🔌 API Integration

### Service Functions
```typescript
// services/api.ts
export const chatbotAPI = {
  // Get dashboard metrics
  getDashboardStats: () => fetch('/api/dashboard/stats'),
  
  // Get conversations
  getConversations: (page: number) => fetch(`/api/conversations?page=${page}`),
  
  // Update bot settings
  updateBotSettings: (settings: BotSettings) => 
    fetch('/api/settings', { method: 'PUT', body: JSON.stringify(settings) }),
  
  // Get analytics data
  getAnalytics: (timeRange: string) => fetch(`/api/analytics?range=${timeRange}`)
};
```

### WebSocket Integration
```typescript
// hooks/useWebSocket.ts
export const useWebSocket = (url: string) => {
  const [messages, setMessages] = useState([]);
  
  useEffect(() => {
    const ws = new WebSocket(url);
    ws.onmessage = (event) => {
      const newMessage = JSON.parse(event.data);
      setMessages(prev => [...prev, newMessage]);
    };
    return () => ws.close();
  }, [url]);
  
  return messages;
};
```

## 📱 Responsive Design

### Breakpoints
- **Mobile**: < 768px
- **Tablet**: 768px - 1024px  
- **Desktop**: > 1024px

### Mobile-First Approach
```css
/* Tailwind responsive classes */
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
  <!-- Responsive grid layout -->
</div>
```

## 🧪 Testing

```bash
# Run unit tests
npm run test

# Run integration tests
npm run test:integration

# Run e2e tests
npm run test:e2e

# Test coverage
npm run test:coverage
```

### Testing Stack
- **Unit Tests**: Vitest + React Testing Library
- **Integration Tests**: MSW for API mocking
- **E2E Tests**: Playwright
- **Visual Tests**: Chromatic (optional)

## 🚀 Deployment

### Vercel (Recommended)
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel --prod
```

### Netlify
```bash
# Build and deploy
npm run build
netlify deploy --prod --dir=dist
```

### Docker
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "run", "preview"]
```

## 🔒 Security

### Authentication
- JWT token-based authentication
- Protected routes for admin features
- Session management with refresh tokens

### Data Protection
- Input sanitization for all forms
- XSS protection with Content Security Policy
- HTTPS enforcement in production

## 📈 Performance

### Optimization Techniques
- **Code Splitting**: Lazy loading for routes
- **Bundle Analysis**: Webpack bundle analyzer
- **Image Optimization**: WebP format with fallbacks
- **Caching**: Service worker for offline functionality

### Performance Metrics
- **First Contentful Paint**: < 1.5s
- **Largest Contentful Paint**: < 2.5s
- **Cumulative Layout Shift**: < 0.1
- **First Input Delay**: < 100ms

## 🎨 Theming

### Design System
```typescript
// theme/colors.ts
export const colors = {
  primary: {
    50: '#f0f9ff',
    500: '#3b82f6',
    900: '#1e3a8a'
  },
  medical: {
    primary: '#10b981',
    secondary: '#f59e0b',
    danger: '#ef4444'
  }
};
```

### Dark Mode
```tsx
// Automatic theme detection
const [theme, setTheme] = useTheme();

<div className={`${theme === 'dark' ? 'dark' : ''}`}>
  <!-- App content -->
</div>
```

## 🛠️ Development

### Available Scripts
```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run preview      # Preview production build
npm run lint         # Run ESLint
npm run type-check   # TypeScript type checking
npm run format       # Format code with Prettier
```

### Code Quality
- **ESLint**: Code linting with React hooks rules
- **Prettier**: Code formatting
- **Husky**: Pre-commit hooks
- **TypeScript**: Static type checking

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Follow coding standards and add tests
4. Commit changes: `git commit -m 'Add amazing feature'`
5. Push to branch: `git push origin feature/amazing-feature`
6. Open Pull Request

### Coding Standards
- Use TypeScript for all new code
- Follow React best practices
- Write tests for new features
- Update documentation

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- 📖 **Documentation**: Check component documentation
- 🐛 **Issues**: Open GitHub issue
- 💬 **Discussions**: GitHub Discussions tab
- 📧 **Contact**: [your-email@example.com]

## 🔮 Roadmap

- [ ] **Real-time Notifications** - Push notifications for admin alerts
- [ ] **Advanced Analytics** - ML-powered usage insights
- [ ] **Multi-language Support** - Internationalization
- [ ] **Voice Messages** - Audio message support
- [ ] **Appointment Booking** - Integration with calendar systems
- [ ] **Telemedicine** - Video consultation features

---

Made with ❤️ for healthcare accessibility# sih

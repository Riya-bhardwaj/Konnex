# Konnex

A virtual helpdesk plugin with an integrated UI that can be embedded into any web application. It provides a floating widget for end-users and a comprehensive admin panel for administrators to manage helpdesk operations.

## Features

- **Announcements System** - Admin sends real-time announcements to users via WebSocket
- **Bug Reporting** - Users report bugs through the widget; admins view and manage them in the dashboard
- **Application Navigation** - Configurable navigation links managed by admins
- **Chatbot Support** - Multi-step chatbot interaction for user assistance
- **Feature Toggle System** - Enable/disable features per client via admin panel
- **Application Improvements** - Users can suggest improvements; admins review and manage

## Tech Stack

**Frontend:**
- React.js (Admin Panel & Widget)
- TypeScript (Widget)
- Bootstrap & Reactstrap
- AG-Grid (data tables)
- Socket.io-client
- Styled-components

**Backend:**
- Node.js + Express.js
- Flask + Flask-RESTful + Flask-PyMongo
- Flask-SocketIO

**Database:**
- MongoDB (Cloud Atlas)

## Project Structure

```
Konnex/
├── konnex_widget/              # Embeddable widget (React + TypeScript)
│   ├── src/
│   │   ├── App.tsx             # Main widget app
│   │   ├── widget.ts           # Widget bootstrap & iframe creation
│   │   └── components/         # UI components (Announcements, Chat, Bug, Tasks)
│   └── webpack.config.js
│
├── konnex-admin-panel/         # Admin dashboard (React)
│   ├── src/
│   │   ├── index.js            # App entry point
│   │   ├── routes.js           # Application routes
│   │   └── views/              # Page components (Dashboard, Bugs, Navigation, etc.)
│   └── gulpfile.js
│
├── announcementSocketServer/   # Real-time announcement server (Node.js + Socket.io)
├── announcementsApi/           # Announcements REST API (Flask)
├── appNavApi/                  # Navigation REST API (Flask)
├── isActiveApi/                # Feature configuration API (Flask)
├── bugApi/                     # Bug reports API (Node.js + Express)
├── announcementsSocketApi/     # Socket.io announcements (Flask)
└── Konnex Demo/                # Screenshots and demo materials
```

## Port Configuration

| Service | Port | Technology |
|---------|------|------------|
| Widget Dev Server | 9000 | Webpack Dev Server |
| Admin Panel | 3000 | React Dev Server |
| appNavApi | 5000 | Flask |
| isActiveApi | 5001 | Flask |
| announcementSocketServer | 5002 | Node.js/Socket.io |
| announcementsApi | 5002 | Flask |
| bugApi | 5003 | Node.js/Express |
| announcementsSocketApi | 5005 | Flask/Socket.io |

## Installation & Setup

### Prerequisites
- Node.js & npm
- Python 3.x & pip
- MongoDB Atlas account (or local MongoDB)

### Admin Panel

```bash
cd konnex-admin-panel
npm install
npm start
```

### Widget

```bash
cd konnex_widget
npm install
npm run dev     # Development mode
npm run build   # Production build
```

### Backend APIs (Flask)

For each Flask API (`announcementsApi`, `appNavApi`, `isActiveApi`, `announcementsSocketApi`):

```bash
cd <api-folder>
pip install flask flask-restful flask-pymongo flask-cors pymongo flask-socketio
python app.py
```

### Backend APIs (Node.js)

For Node.js services (`announcementSocketServer`, `bugApi`):

```bash
cd <api-folder>
npm install
npm run dev     # Development with nodemon
npm start       # Production mode
```

## API Endpoints

### Configuration (isActiveApi - Port 5001)
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api?key=<key>` | Retrieve feature configuration |
| PUT | `/api?key=<key>` | Create configuration |
| PATCH | `/api?key=<key>` | Update configuration |

### Announcements (announcementsApi - Port 5002)
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api?key=<key>` | Get last 5 announcements |
| PUT | `/api?key=<key>` | Add announcement |

### Navigation (appNavApi - Port 5000)
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api?key=<key>` | Get navigation items |
| PUT | `/api?key=<key>` | Add navigation item |

### Bugs (bugApi - Port 5003)
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/bugs` | Create bug report |
| GET | `/bugs` | List all bug reports |
| PATCH | `/bugs/:id` | Update bug by ID |
| DELETE | `/bugs/:id` | Delete bug by ID |

## Client Key System

The application uses a client key system for multi-tenancy:
- Default key: `konnex123`
- Pass the key as a query parameter in API calls
- Each client has isolated configurations and data

## Usage

1. Start all backend APIs
2. Start the admin panel (`npm start` in `konnex-admin-panel`)
3. Start the widget dev server (`npm run dev` in `konnex_widget`)
4. Access admin panel at `http://localhost:3000`
5. Embed the widget in your application via iframe from `http://localhost:9000`

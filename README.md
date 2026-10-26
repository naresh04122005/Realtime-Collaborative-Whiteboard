# Real-time Collaborative Whiteboard

A high-performance, real-time collaborative whiteboard web application built with **Next.js**, **Express**, and **Socket.IO**. Designed for distributed teams and classrooms to brainstorm, sketch, and interact in real time with synchronized canvas state, live cursor tracking, and embedded chat.

---

## ✨ Features

- **⚡ Real-time Multi-user Collaboration**
  - Instant canvas stroke synchronization across all connected peers
  - Live cursor tracking with user name tags and assigned identity colors
  - Real-time room chat with user badges
  - Live user presence indicators (join/leave alerts)

- **🎨 Rich Drawing Suite**
  - Freehand drawing with adjustable stroke width and custom color palettes (RGBA support)
  - Geometric shapes: lines, rectangles, and circles
  - Eraser and selection tools
  - Image paste & upload onto the canvas

- **🧭 Advanced Canvas Navigation**
  - Infinite canvas with smooth panning and zooming
  - Interactive minimap overview for quick navigation
  - Multi-user undo stack per session
  - Configurable canvas background grid styles

- **🛡️ Robust Backend Architecture**
  - Custom Express + Socket.IO server integrated with Next.js
  - Room isolation with max-occupancy caps and dynamic join validation
  - In-memory room lifecycle management with automatic cleanup on room vacancy (preventing memory leaks)
  - Defensive event guards preventing uncaught exceptions on out-of-order socket actions

---

## 🚀 Tech Stack

- **Frontend:** Next.js, React, Recoil (State Management), Framer Motion (Animations), TailwindCSS
- **Backend:** Node.js, Express, Socket.IO (WebSockets), TypeScript
- **Tools & Build:** TypeScript, ESLint, Prettier, Nodemon

---

## 🛠️ Architecture & System Design

```
                     ┌────────────────────────────────────────┐
                     │          Browser Client(s)             │
                     │  (HTML5 Canvas, Recoil State, Minimap) │
                     └───────────────────▲────────────────────┘
                                         │
                               WebSocket │ (Socket.IO Events)
                                         │
                     ┌───────────────────▼────────────────────┐
                     │          Node / Express Server         │
                     │  - Socket.IO Room Manager              │
                     │  - In-Memory User & Move State Map     │
                     │  - Memory Leak Prevention on Vacancy   │
                     │  - Next.js SSR / Static Request Bridge │
                     └────────────────────────────────────────┘
```

### Key Socket Events

| Event | Direction | Description |
| :--- | :--- | :--- |
| `create_room` | Client ➔ Server | Creates a new whiteboard session with a unique alphanumeric room code |
| `join_room` | Client ➔ Server | Validates room existence and room capacity before admitting user |
| `draw` / `user_draw` | Bidirectional | Broadcasts stroke coordinates, shape geometry, and color metadata |
| `undo` / `user_undo` | Bidirectional | Safely pops the user's latest move without crashing backend state |
| `mouse_move` | Client ➔ Server | Streams cursor coordinates throttled for smooth peer tracking |
| `send_msg` / `new_msg` | Bidirectional | Delivers room-wide chat messages with sender attribution |

---

## 🏗️ Project Structure

```
Realtime-Collaborative-Whiteboard/
├── common/                # Shared utilities, hooks, constants & types
│   ├── components/        # Reusable UI widgets (modals, icons, inputs)
│   ├── constants/         # Color palettes, canvas defaults
│   ├── hooks/            # Custom React hooks
│   ├── lib/              # Socket.IO client instance
│   ├── recoil/           # Global state atoms & selectors
│   └── types/            # TypeScript interfaces & socket event contracts
├── modules/               # Feature modules
│   ├── home/             # Landing page & room creation/joining interface
│   └── room/             # Whiteboard canvas, toolbar, chat, minimap & hooks
├── pages/                 # Next.js Pages router
│   ├── _app.tsx          # App root wrapper with RecoilRoot & ToastContainer
│   ├── index.tsx         # Home route
│   └── [roomId].tsx      # Dynamic room route
├── public/                # Static assets
├── scripts/               # Runtime compatibility polyfills
├── server/                # Backend Express + Socket.IO server
│   └── index.ts          # Server entry point & socket event handlers
├── next.config.js         # Next.js configuration
├── package.json           # Dependencies and run scripts
└── tsconfig.json          # TypeScript compiler configuration
```

---

## 🚦 Getting Started

### Prerequisites
- Node.js (v18+)
- npm or yarn

### 1. Clone the repository
```bash
git clone https://github.com/naresh04122005/Realtime-Collaborative-Whiteboard.git
cd Realtime-Collaborative-Whiteboard
```

### 2. Install dependencies
```bash
npm install
```

### 3. Run development server
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### 4. Build for production
```bash
npm run build
npm start
```

---

## 🧑‍💻 Author

**Naresh**  
- Final Year, Indian Institute of Information Technology (IIIT) Lucknow  
- GitHub: [@naresh04122005](https://github.com/naresh04122005)  

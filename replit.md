# SmartHome Pro

## Overview

SmartHome Pro is a Progressive Web App (PWA) for unified smart home device management. The application enables users to monitor and control multiple smart home devices from a single mobile-first interface, featuring real-time status updates, room-based organization, automation through scenes and schedules, and an emergency shutdown feature for all devices.

The app targets homeowners, renters, and property managers who need a centralized platform to manage devices across different smart home ecosystems.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React 18+ with TypeScript, built using Vite for fast development and optimized production builds.

**UI Component Library**: Shadcn/ui components built on Radix UI primitives, providing accessible, unstyled components that are customized with Tailwind CSS. The "new-york" style variant is used for a modern, clean aesthetic.

**Styling System**: Tailwind CSS with custom design tokens for consistent spacing, colors, and typography. The design follows a hybrid approach combining Material Design's clarity with iOS Home's intuitive touch patterns. Key design principles include:
- Mobile-first, touch-optimized interactions
- Instant visual feedback (within 100ms)
- Safety-critical design with prominent emergency controls
- Room-based device organization

**State Management**: 
- React Context API for authentication state (`AuthProvider`)
- TanStack Query (React Query) for server state management, data fetching, and caching
- Local component state with React hooks

**Routing**: Wouter for lightweight client-side routing without the overhead of React Router.

**Real-time Updates**: WebSocket connection (`WebSocketProvider`) for live device status updates and event notifications. The WebSocket client automatically invalidates relevant queries when device states change.

**Progressive Web App**: Service workers configured for offline functionality and basic device control when internet connectivity is limited.

### Backend Architecture

**Server Framework**: Express.js with TypeScript, serving both API endpoints and the built React application.

**Authentication**: Passport.js with local strategy for username/password authentication. Passwords are hashed using Node.js crypto scrypt with random salts. Session management uses express-session with in-memory store (MemoryStore) for development.

**API Design**: RESTful endpoints organized by resource:
- `/api/auth/*` - Authentication (login, register, logout, user info)
- `/api/rooms/*` - Room CRUD operations
- `/api/devices/*` - Device management and control
- `/api/scenes/*` - Scene configuration and activation
- `/api/schedules/*` - Automation scheduling
- `/api/activity/*` - Activity logs and history

**WebSocket Server**: ws library for WebSocket connections, enabling bi-directional real-time communication. Clients are tracked by user ID, and events are broadcast to specific users when device states change.

**Development Tools**:
- Vite middleware mode for hot module replacement during development
- Custom logging with timestamps for API requests
- Runtime error overlay for debugging

### Database Architecture

**ORM**: Drizzle ORM for type-safe database queries and schema management.

**Database**: PostgreSQL (configured for Neon serverless PostgreSQL with WebSocket support via `@neondatabase/serverless`).

**Schema Design**:
- `users` - User accounts with credentials and profile information
- `rooms` - Room/zone definitions with icons for organization
- `devices` - Smart device records with type, status, settings (JSONB), and room associations
- `scenes` - Pre-configured device combinations for scenarios
- `scene_devices` - Junction table linking scenes to devices with specific states
- `schedules` - Time-based automation rules with day patterns
- `activity_logs` - Comprehensive audit trail of all system actions

**Data Relationships**:
- Users have many rooms, devices, scenes, schedules, and activity logs
- Rooms have many devices
- Scenes link to multiple devices through scene_devices junction table
- All entities cascade delete when parent user is removed
- Devices use `onDelete: "set null"` for room relationships to preserve devices when rooms are deleted

**Migrations**: Drizzle Kit handles schema migrations with files stored in `/migrations` directory.

### External Dependencies

**UI Component Dependencies**:
- Radix UI component primitives (@radix-ui/*) - Accessible, unstyled UI components
- Lucide React - Icon library for consistent iconography
- Tailwind CSS - Utility-first CSS framework
- class-variance-authority (CVA) - Type-safe component variant management
- cmdk - Command menu component

**Form Handling**:
- React Hook Form - Form state management
- Zod - Schema validation
- @hookform/resolvers - Integration between React Hook Form and Zod
- drizzle-zod - Generate Zod schemas from Drizzle tables

**Date/Time**:
- date-fns - Date manipulation and formatting

**Data Fetching**:
- @tanstack/react-query - Server state management and caching

**Database & Backend**:
- @neondatabase/serverless - Neon PostgreSQL client with WebSocket support
- drizzle-orm - TypeScript ORM
- ws - WebSocket server implementation

**Authentication**:
- passport - Authentication middleware
- passport-local - Username/password authentication strategy
- express-session - Session middleware
- memorystore - In-memory session store (development only)

**Build Tools**:
- Vite - Frontend build tool and dev server
- esbuild - Backend bundler for production
- TypeScript - Type safety across the stack
- Replit-specific plugins for development environment integration

**Font Assets**:
- Google Fonts: Inter (primary UI font), Architects Daughter, DM Sans, Fira Code, Geist Mono, JetBrains Mono, Syne (loaded via CDN in index.html)
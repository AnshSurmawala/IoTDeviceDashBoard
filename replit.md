# IoT Data Analytics Dashboard

## Overview

This is a real-time IoT data analytics dashboard for monitoring sensor data from connected devices. The application displays live metrics including temperature, humidity, pressure, and energy consumption through an interactive dashboard with charts, gauges, and data tables. Built with React on the frontend and Express on the backend, it provides a comprehensive monitoring solution for IoT sensor networks.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React with TypeScript using Vite as the build tool and development server.

**UI Component System**: Utilizes shadcn/ui components built on Radix UI primitives with Tailwind CSS for styling. The design follows Material Design principles optimized for data-intensive applications, prioritizing clear information hierarchy and readability for real-time monitoring.

**State Management**: TanStack Query (React Query) for server state management, handling data fetching, caching, and synchronization with automatic refetching every 30 seconds to maintain real-time dashboard updates.

**Routing**: Wouter for lightweight client-side routing.

**Typography**: Primary font is 'Inter' with 'JetBrains Mono' for numerical data and timestamps to enhance readability of metric values.

**Responsive Layout**: 12-column grid system with breakpoint-specific layouts (mobile: single column, tablet: 2 columns, desktop: 3-4 columns) using Tailwind's responsive utilities.

### Backend Architecture

**Server Framework**: Express.js running on Node.js with TypeScript.

**API Design**: RESTful API with endpoints for devices, sensor readings, and analytics. All responses are JSON-formatted.

**Data Storage**: Currently uses in-memory storage (MemStorage class) with sample data initialization. The architecture supports swapping to database-backed storage through the IStorage interface abstraction.

**Database Schema** (via Drizzle ORM): 
- Devices table: stores device metadata (id, name, type, location, status)
- Sensor readings table: stores timestamped sensor data (id, deviceId, timestamp, temperature, humidity, pressure, energy)
- Configured for PostgreSQL using Neon serverless driver

**Development Server**: Custom Vite integration for hot module replacement in development, with middleware-based request logging.

### Data Flow Architecture

**Real-time Updates**: Frontend polls backend every 30 seconds via query invalidation, triggering automatic data refresh for readings, analytics, and device status.

**Time Range Filtering**: Supports multiple time ranges (1h, 6h, 12h, 24h) with server-side filtering of sensor readings and analytics calculations.

**Data Transformation**: Raw sensor readings are transformed into:
- KPI metrics (averages for temperature, humidity, pressure, total energy)
- Chart data (formatted for Recharts library with time-series visualization)
- Device status enrichment (connection strength, last reading association)

### Design System

**Component Library**: Custom components built on shadcn/ui including:
- KPI Cards: Display primary metrics with trend indicators
- Charts: Line charts (temperature/humidity trends), area charts (pressure), bar charts (energy consumption)
- Gauge Charts: Visual representation of current values against thresholds
- Device Status Cards: Real-time device monitoring with connection status
- Data Tables: Recent sensor readings with device correlation

**Styling Approach**: CSS variables for theming with light/dark mode support, utility-first Tailwind CSS, and custom elevation utilities for hover/active states.

## External Dependencies

### Core Framework Dependencies
- **@neondatabase/serverless**: PostgreSQL client for serverless environments (Neon database)
- **drizzle-orm**: TypeScript ORM for database schema and queries
- **drizzle-zod**: Schema validation integration between Drizzle and Zod

### UI Component Libraries
- **@radix-ui/***: Primitive UI components (accordion, dialog, dropdown, select, etc.)
- **recharts**: Charting library for data visualization
- **lucide-react**: Icon library
- **class-variance-authority**: Component variant management
- **tailwind-merge** & **clsx**: Utility for merging CSS classes

### Form & Validation
- **react-hook-form**: Form state management
- **@hookform/resolvers**: Form validation resolvers
- **zod**: TypeScript-first schema validation

### Data Fetching
- **@tanstack/react-query**: Server state management and caching

### Session Management
- **connect-pg-simple**: PostgreSQL session store for Express (though sessions aren't currently implemented)

### Development Tools
- **vite**: Build tool and dev server
- **@vitejs/plugin-react**: React support for Vite
- **@replit/vite-plugin-***: Replit-specific development plugins (error overlay, cartographer, dev banner)
- **typescript**: Type checking and compilation
- **tailwindcss**: Utility-first CSS framework
- **postcss** & **autoprefixer**: CSS processing

### Utility Libraries
- **date-fns**: Date manipulation and formatting
- **nanoid**: Unique ID generation
- **embla-carousel-react**: Carousel component (though not currently used in main dashboard)
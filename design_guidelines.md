# IoT Data Analytics Dashboard - Design Guidelines

## Design Approach

**Selected Approach:** Design System - Material Design  
**Justification:** This is a data-intensive, utility-focused application requiring clear information hierarchy, consistent component patterns, and excellent readability for monitoring real-time sensor data. Material Design provides robust patterns for cards, data visualization, and dashboard layouts optimized for information density.

## Typography System

**Font Family:** 
- Primary: 'Inter' via Google Fonts CDN
- Monospace: 'JetBrains Mono' for numerical data and timestamps

**Hierarchy:**
- Dashboard Title: 2.5rem (40px), font-weight: 700
- Section Headers: 1.5rem (24px), font-weight: 600
- Card Titles: 1.125rem (18px), font-weight: 600
- Metric Values: 2rem (32px), font-weight: 700, monospace
- Metric Labels: 0.875rem (14px), font-weight: 500
- Body Text/Descriptions: 1rem (16px), font-weight: 400
- Timestamps/Meta: 0.75rem (12px), font-weight: 400

## Layout System

**Spacing Units:** Tailwind utilities of 2, 4, 6, and 8 (e.g., p-4, gap-6, m-8)

**Grid Structure:**
- Dashboard container: max-w-[1600px] mx-auto px-6
- Primary grid: 12-column system with gap-6
- Card layouts: grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4

**Breakpoint Strategy:**
- Mobile: Single column cards, stacked metrics
- Tablet (md): 2-column layout for cards
- Desktop (lg): 3-column for smaller cards, 2-column for charts
- Large (xl): 4-column for KPI cards, flexible chart arrangements

## Component Library

### Dashboard Header
- Full-width header with title, real-time status indicator (pulsing dot), last updated timestamp
- Quick action toolbar: refresh button, time range selector, export options
- Height: h-20, sticky positioning

### KPI Cards (Key Metrics)
- Compact design: p-6, rounded-lg
- Content: Large metric value (top), label (bottom), trend indicator (small arrow + percentage)
- 4-column grid on desktop, stacked on mobile
- Include: Current Temperature, Humidity, Pressure, Energy Consumption

### Chart Containers
- White/elevated cards with p-6 padding
- Chart title with icon prefix
- Full-width responsive charts
- Minimum height: min-h-[400px] for proper data visibility

**Chart Types:**
- **Line Charts (Time Series):** Temperature and humidity trends over time with dual y-axes
- **Bar Charts:** Energy consumption by device/hour
- **Gauge Charts:** Real-time sensor readings with min/max indicators and colored zones
- **Area Charts:** Pressure variations with gradient fills

### Device Status Grid
- Card-based layout showing individual sensor/device status
- Each card: device name, status badge, last reading, connection strength indicator
- Grid: grid-cols-1 md:grid-cols-2 lg:grid-cols-3 with gap-4

### Time Range Selector
- Pill-button group: "1H", "6H", "24H", "7D", "30D"
- Active state with distinct treatment
- Positioned in header toolbar

### Data Table
- Responsive table for recent sensor readings
- Columns: Timestamp, Device, Temperature, Humidity, Pressure, Status
- Alternating row treatment, sticky header
- Max 10 rows with "Load More" option

### Alert/Notification Banner
- Appears when anomalies detected
- Position: Below header, dismissible
- Content: Alert icon, message, timestamp, action button

## Navigation

**Sidebar Navigation (Optional based on scope):**
- Narrow collapsed state (w-16) with icon-only
- Expanded state (w-64) with labels
- Items: Dashboard, Devices, Analytics, Settings
- Toggle button for expansion

**OR Simple Top Navigation:**
- Horizontal tab-style navigation
- Sticky below header
- Items: Overview, Devices, Historical Data, Settings

## Data Visualization Principles

**Chart Specifications:**
- Use Chart.js or Recharts library via CDN
- Consistent axis labeling and grid lines
- Legend positioning: top-right for line/area charts
- Interactive tooltips showing exact values on hover
- Responsive scaling with maintainAspectRatio

**Real-Time Updates:**
- Smooth transitions (300ms) when data updates
- Pulsing indicator during data fetch
- Timestamp update on each refresh

## Responsive Behavior

**Mobile (< 768px):**
- Single column layout
- KPI cards in 2-column grid for compact display
- Charts full-width with vertical scrolling
- Collapsible sections for better organization

**Tablet (768px - 1024px):**
- 2-column layouts for most cards
- Side-by-side chart comparisons

**Desktop (1024px+):**
- Full multi-column layouts
- Dashboard spans available width up to max-w-[1600px]
- Optimal information density without overcrowding

## Accessibility

- All charts include aria-labels describing data trends
- Keyboard navigation for time range selectors
- Focus indicators on all interactive elements
- ARIA live regions for real-time data updates announcement
- Sufficient contrast ratios for all text and icons

## Icons

**Library:** Heroicons (outline for general UI, solid for status indicators)
- Dashboard: ChartBarIcon
- Devices: CpuChipIcon
- Temperature: FireIcon
- Humidity: CloudIcon
- Pressure: ArrowsPointingOutIcon
- Energy: BoltIcon
- Refresh: ArrowPathIcon
- Settings: Cog6ToothIcon
- Alert: ExclamationTriangleIcon

## Page Structure

```
├── Header (Dashboard Title + Controls)
├── KPI Cards Row (4 primary metrics)
├── Charts Section
│   ├── Temperature/Humidity Line Chart (2/3 width)
│   └── Energy Bar Chart (1/3 width)
├── Gauges Row (3 real-time gauges)
├── Device Status Grid
└── Recent Data Table
```

## Animations

**Minimal & Purposeful:**
- Chart data transitions: 300ms ease-in-out
- Real-time status pulse: 2s infinite for active connections
- Card hover: subtle lift with shadow (translate-y-1)
- No elaborate scroll animations or unnecessary motion

This dashboard prioritizes data clarity, real-time monitoring efficiency, and responsive performance over decorative elements.
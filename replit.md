# Rental SaaS - Sports Equipment Rental System

## Overview
This project is a production-ready SaaS application designed for sports equipment rental. Its primary purpose is to provide accurate pricing calculations, streamline order management, and support a multi-tenant architecture. The system aims to simplify rental operations, manage inventory effectively, and offer flexible pricing and discount options, positioning it as a robust solution for businesses in the sports equipment rental market.

## User Preferences
I prefer detailed explanations.
Do not make changes to the folder Z.
Do not make changes to the file Y.

## System Architecture
The application is built with a modern web stack. The **Frontend** uses React with TypeScript, Vite, TailwindCSS, and Shadcn UI for a responsive and aesthetically pleasing user interface. The **Backend** is developed with Express and TypeScript, providing a robust API layer. **PostgreSQL (Neon)** is used as the database, managed with Drizzle ORM, ensuring data integrity and scalability. Authentication is handled via **Passport.js** with a local strategy. **TanStack Query** manages state, and **Wouter** is used for routing.

### UI/UX Decisions
- **Font Primary**: Inter
- **Font Mono**: JetBrains Mono (for prices, codes, order numbers)
- **Colors**: Material Design 3 with a blue primary palette
- **Components**: Shadcn UI with custom theming
- **Spacing**: Consistent Material Design spacing
- **Dark Mode**: Full support via CSS variables
- **Navigation**: Sidebar navigation with role-based menu items and user profile
- **Collapsible Sidebar** (Nov 2024): Burger menu for toggling sidebar on all screen sizes
  - Desktop (≥768px): Content shifts with margin-left when sidebar toggles, sidebar state persists across navigation
  - Mobile (<768px): Sidebar overlays content with backdrop, auto-closes after navigation
  - Smooth 300ms width transition animation
  - Accessible toggle button always visible in header

### Technical Implementations
- **Accurate Pricing Engine**: Supports weekday/weekend rates, 30-minute increments, and adult/child categories.
- **Multi-tenancy**: Achieved through workspace and location isolation.
- **Order Management**: Comprehensive CRUD operations for rental orders, including status tracking.
  - **Inline Editing** (Nov 2024): Orders can be edited directly in the dashboard table without navigation to separate pages.
    - Editable fields: Equipment selection (dialog-based multi-select), start time, end time
    - Read-only fields: Client name, phone
    - Auto-calculated: Price recalculates in real-time when times or equipment change
    - State synchronization: Equipment selections sync with backend data via useEffect
    - Data persistence: PATCH /api/orders/:id with cache invalidation for both orders and order-items
- **Client Management**: A client database with tagging capabilities (e.g., student, privileged, VIP).
- **Inventory Management**: Tracks equipment status and availability with barcode system.
  - **Barcode System** (Nov 2024): Automatic barcode generation and management
    - Format: EQ-XXXXXXXXXX (prefix + 10 alphanumeric characters)
    - Auto-generation using nanoid for unique identifiers
    - Visual barcode display using react-barcode library
    - Regenerate button for creating new barcodes
    - Search/filter inventory by barcode or item number
    - Database column: nullable unique barcode field in equipment_items table
- **Discount System**: Configurable discounts (percentage-based) and promo codes.
- **Admin Panels**: Dedicated interfaces for managing tariffs, bundles, calendar special days, and system settings.
  - **Tariff Inline Editing**: Tariffs can be edited directly in the admin table (weekday/weekend prices, base hours, increments)
  - **Client Tag Customization** (Nov 2024): Superadmin can customize client tag categories through UI
    - Database-driven tag definitions stored in `clientTagDefinitions` table
    - Full CRUD operations for tags (create, read, update, delete)
    - Configurable tag properties: code (unique identifier), name (display label), color (8 options), sort order
    - Tags dynamically displayed throughout application (clients page, order forms)
    - Settings page at `/admin/settings` with tabbed interface
  - **Interactive Calendar** (Nov 2024): Visual calendar interface for managing special days
    - Click dates to create or edit special days
    - Color-coded day types: Holidays (amber), Weekends (purple), Weekdays (blue)
    - Full CRUD operations (create, read, update, delete) with workspace isolation
    - Calendar uses react-day-picker for visual date selection
    - Mobile-responsive grid layout
  - **Workspace Settings** (Nov 2024): Configurable workspace preferences via General Settings tab
    - Timezone selection with 11 Russian zones (UTC+2 Kaliningrad through UTC+12 Kamchatka)
    - Company name, currency, business hours, default rental duration
    - Backend uses upsert pattern to handle missing settings gracefully
    - Settings persist across sessions and auto-load on page refresh
- **UX Enhancements**: Features like quick client creation, order editing, and smart time defaults.

### Feature Specifications
- **Authentication**: Username/password-based, with roles (SUPERADMIN, MANAGER, CASHIER).
- **Database Schema**: Core entities include users, workspaces, locations, clients, equipment types, individual equipment items, bundle definitions, tariffs, orders, payments, discounts, client tag definitions, and workspace settings.
- **Pricing Logic**: Detailed rates for various equipment types (e.g., Skis, Snowboard, Boots, Helmets) for adult/child categories and weekday/weekend/holiday pricing. Pricing increments are in 30-minute blocks, rounded up.
- **Discount System**: Specific rules for various client tags and general promo codes, including special rules like free helmets for certain student types.
- **Bundle Architecture**: Bundles are defined as billing groups, not physical inventory items. They group multiple physical equipment types for a single tariff, with physical items assigned upon rental.
- **Frontend Routes**: Includes `/auth`, `/`, `/orders/new`, `/orders/:id/edit`, `/clients`, `/inventory`, `/reports`, `/admin/tariffs`, `/admin/bundles`, `/admin/calendar`, and `/admin/settings`.

## External Dependencies
- **Database**: PostgreSQL (specifically Neon for cloud hosting).
- **Authentication**: Passport.js.
- **UI Component Library**: Shadcn UI.
- **State Management**: TanStack Query.
- **Routing**: Wouter.
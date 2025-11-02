# Design Guidelines: Sports Equipment Rental SaaS

## Design Approach

**Selected System:** Material Design 3  
**Rationale:** This is a utility-focused, data-intensive business application requiring efficient workflows, clear information hierarchy, and professional polish. Material Design provides excellent patterns for forms, tables, and dashboards while maintaining modern aesthetics.

**Key Principles:**
- Clarity over decoration - every element serves a functional purpose
- Efficient data entry and quick task completion
- Scannable information hierarchy for busy cashiers
- Professional, trustworthy appearance for business software
- Consistent patterns reduce cognitive load during repetitive tasks

---

## Core Design Elements

### A. Typography

**Font Families:**
- Primary: Inter (via Google Fonts CDN)
- Monospace: JetBrains Mono (for order numbers, codes, prices)

**Type Scale:**
- Display (Dashboard headers): 32px, font-bold
- H1 (Page titles): 24px, font-semibold
- H2 (Section headers): 20px, font-semibold
- H3 (Card headers, subsections): 16px, font-semibold
- Body (primary content): 14px, font-normal
- Small (metadata, helpers): 12px, font-normal
- Button text: 14px, font-medium
- Monospace (prices, IDs): 14px, font-mono

---

### B. Layout System

**Spacing Primitives:** Tailwind units of **2, 4, 6, 8, 12, 16**
- Micro spacing (icons, inline elements): p-2, gap-2
- Standard component padding: p-4, p-6
- Section spacing: p-8, gap-8
- Page margins: p-6 (mobile), p-8 (desktop)
- Large breaks: mt-12, mb-16

**Grid System:**
- Dashboard: 12-column responsive grid
- Forms: Single column (max-w-2xl) for focused data entry
- Data tables: Full-width with horizontal scroll on mobile
- Cards grid: grid-cols-1 md:grid-cols-2 lg:grid-cols-3

**Containers:**
- Main content area: max-w-7xl mx-auto
- Forms/detail views: max-w-3xl mx-auto
- Full-width tables: w-full with container padding

---

### C. Component Library

**Navigation:**
- Sidebar navigation (desktop): Fixed left sidebar, w-64, with workspace logo, main navigation links, user profile at bottom
- Mobile navigation: Bottom tab bar or hamburger menu
- Top bar: Breadcrumbs, current location selector, online/offline indicator, user menu

**Dashboard Cards:**
- Elevated cards with subtle shadow (shadow-md)
- White/surface background with p-6
- Header with icon + title (flex items-center gap-2)
- Metric display: Large number (text-3xl font-bold) + label + optional trend indicator
- Action links/buttons at card footer

**Forms:**
- Floating labels or top-aligned labels
- Input fields: border-2 focus:ring-2 focus:border-primary rounded-lg p-3
- Required indicators: Red asterisk or "(required)" text
- Inline validation: Error messages below field, success checkmark
- Field groups: Related fields in rows with gap-4
- Submit area: Sticky footer on mobile, inline on desktop

**Data Tables:**
- Header row: bg-gray-50, font-semibold, sticky top
- Row hover: bg-gray-50 hover state
- Alternating rows: Optional subtle striping
- Inline actions: Icon buttons on row hover
- Status badges: Rounded-full px-3 py-1 text-xs font-medium
- Numeric columns: Right-aligned, monospace font
- Empty state: Centered message with icon

**Buttons:**
- Primary: Solid, prominent (bg-primary with hover/active states)
- Secondary: Outlined (border-2 border-primary text-primary)
- Tertiary/Ghost: Text only with hover background
- Sizes: h-10 px-4 (default), h-12 px-6 (large), h-8 px-3 (small)
- Icon buttons: Square aspect ratio, p-2 or p-3
- Loading state: Spinner + disabled opacity

**Modals/Dialogs:**
- Overlay: backdrop-blur-sm bg-black/30
- Content: rounded-xl shadow-2xl max-w-lg/2xl/4xl
- Header: p-6 border-b flex justify-between items-center
- Body: p-6
- Footer: p-6 border-t flex justify-end gap-3

**Status Indicators:**
- Online/Offline: Dot indicator (w-2 h-2 rounded-full) + text
- Order status badges: DRAFT (gray), OPEN (blue), PAID (green), CLOSED (gray)
- Inventory status: Color-coded badges with icons

**Price Display:**
- Large, prominent pricing: text-2xl font-bold font-mono
- Breakdown lines: text-sm with flex justify-between
- Discounts: text-green-600 with minus sign
- Total: border-t-2 pt-2 mt-2, text-xl font-bold

---

### D. Animations

**Use Sparingly:**
- Transitions: transition-all duration-200 for hover states
- Modal entry: fade + scale animation (duration-300)
- Success feedback: Checkmark with brief scale pulse
- Loading states: Spinner or skeleton screens
- NO page transitions, scroll animations, or decorative effects

---

## Screen-Specific Guidelines

### Login Page
- Centered card on neutral background
- Logo at top
- Single-column form (max-w-sm)
- Clear labels, password visibility toggle
- Remember me checkbox
- Prominent login button

### Dashboard
- KPI cards in grid (3-4 across on desktop)
- Active rentals summary table
- Quick actions toolbar
- Recent activity feed
- Clear visual hierarchy: metrics → active orders → secondary info

### New Order / Order Details
- Two-column layout on desktop (order details left, price calculation right)
- Sticky price summary on scroll
- Equipment selection: Cards or dropdown with autocomplete
- Time picker: Calendar + time slots
- Client search: Autocomplete with recent clients
- Price breakdown: Line items with live updates
- Large "Create Order" or "Save & Close" button

### Inventory Management
- Filterable table with search
- Status column with color-coded badges
- Quick actions: Mark as rented/available/service
- Detail drawer or modal for equipment info
- Photo thumbnails in table (small, square)

### Admin Panels
- Tab navigation for different admin sections
- Forms for tariff editing with clear field labels
- Calendar view for holiday/pricing management
- User management table with role badges

### Reports
- Date range picker at top
- Filter sidebar or collapsible filters
- Chart library integration (Chart.js or Recharts)
- Export button prominently placed
- Tabular data with sorting

---

## Images

**Minimal Image Usage:**
- Workspace logo in sidebar (max h-10)
- Equipment photos in inventory (thumbnail 64x64, detail view larger)
- Client profile photos (rounded-full, 40x40 in lists, 80x80 in details)
- Empty states: Simple illustration or icon (h-32 w-32)
- NO hero images, NO decorative photography

**Image Treatment:**
- Equipment photos: White background, consistent aspect ratio (1:1 or 4:3)
- Rounded corners: rounded-lg for photos
- Placeholder states: bg-gray-200 with icon

---

## Accessibility
- All interactive elements minimum 44x44px touch target
- Proper focus indicators (ring-2 ring-offset-2)
- ARIA labels for icon-only buttons
- Keyboard navigation throughout
- High contrast text (minimum WCAG AA)
- Form validation accessible to screen readers
# Qarz Daftar - Complete Code Documentation

## Project Structure

```
qarz-daftar/
├── client/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── AddDebtDialog.tsx
│   │   │   ├── DebtAnalytics.tsx
│   │   │   ├── DebtCard.tsx
│   │   │   ├── DashboardStats.tsx
│   │   │   ├── EditDebtDialog.tsx
│   │   │   ├── PaymentDialog.tsx
│   │   │   └── ui/ (shadcn/ui components)
│   │   ├── contexts/
│   │   │   └── DebtContext.tsx
│   │   ├── hooks/
│   │   │   └── useDebts.ts
│   │   ├── pages/
│   │   │   └── Home.tsx
│   │   ├── App.tsx
│   │   ├── index.css
│   │   └── main.tsx
│   └── index.html
├── server/
│   └── index.ts
└── package.json
```

---

## Core Files

### 1. useDebts.ts - Custom Hook for Debt Management

**Location**: `client/src/hooks/useDebts.ts`

This hook manages all debt-related state and operations with localStorage persistence.

**Key Interfaces**:
- `Debt`: Main debt object with creditor info, amount, interest rate, due date, status, and payments
- `Payment`: Payment record with amount, date, and optional notes

**Key Functions**:
- `addDebt()`: Create a new debt
- `updateDebt()`: Modify existing debt
- `deleteDebt()`: Remove a debt
- `addPayment()`: Record a payment and update remaining balance
- `deletePayment()`: Remove a payment record
- `getTotalDebt()`: Calculate total outstanding debt
- `getTotalPaid()`: Calculate total amount paid
- `getDebtsByStatus()`: Filter debts by status
- `getDebtsByCreditor()`: Filter debts by creditor name

**Data Persistence**: All debts are automatically saved to localStorage under the key `qarz_daftar_debts`

---

### 2. DebtContext.tsx - Global State Management

**Location**: `client/src/contexts/DebtContext.tsx`

Provides global access to debt management functions throughout the application using React Context API.

**Exports**:
- `DebtProvider`: Wrapper component that provides debt context to children
- `useDebtContext()`: Hook to access debt context in any component

---

### 3. Home.tsx - Main Page

**Location**: `client/src/pages/Home.tsx`

The main dashboard page with three tabs: Overview, Debts, and Analytics.

**Features**:
- Sticky header with title and action buttons
- Dashboard statistics showing key metrics
- Tabbed interface for different views
- Filter buttons for debt status
- Export functionality for debt data
- Empty state messaging when no debts exist

---

### 4. DashboardStats.tsx - Statistics Component

**Location**: `client/src/components/DashboardStats.tsx`

Displays four key metrics:
- Total Debt (outstanding amount)
- Total Paid (cumulative payments)
- Number of Creditors
- Overdue Debts Count

Uses icons from lucide-react and color-coded backgrounds.

---

### 5. DebtCard.tsx - Individual Debt Display

**Location**: `client/src/components/DebtCard.tsx`

Displays a single debt with:
- Creditor name and due date
- Status badge (Active/Overdue/Paid)
- Remaining amount and interest rate
- Circular progress ring showing payoff percentage
- Payment summary and history
- Action buttons (Add Payment, Edit, Delete)

---

### 6. DebtAnalytics.tsx - Charts and Visualizations

**Location**: `client/src/components/DebtAnalytics.tsx`

Uses Recharts library to display three interactive charts:

**Pie Chart**: Debt distribution by creditor
- Shows which creditors have the largest debt amounts
- Color-coded with warm amber palette

**Bar Chart**: Debt by status
- Compares amounts across Active, Overdue, and Paid debts
- Helps visualize debt distribution by status

**Line Chart**: Payment timeline
- Shows payment history over time
- Last 12 payment entries displayed
- Aggregates multiple payments on same date

---

### 7. AddDebtDialog.tsx - New Debt Form

**Location**: `client/src/components/AddDebtDialog.tsx`

Modal dialog for creating new debts with fields:
- Creditor Name (required)
- Debt Amount (required, positive number)
- Interest Rate (required, percentage)
- Due Date (required)
- Notes (optional)

Validates input and shows toast notifications on success/error.

---

### 8. EditDebtDialog.tsx - Edit Debt Form

**Location**: `client/src/components/EditDebtDialog.tsx`

Modal dialog for modifying existing debt details:
- Creditor Name
- Interest Rate
- Due Date
- Status (Active/Overdue/Paid)
- Notes

---

### 9. PaymentDialog.tsx - Payment Recording Form

**Location**: `client/src/components/PaymentDialog.tsx`

Modal dialog for recording payments:
- Payment Amount (required)
- Payment Date (required)
- Notes (optional)

Automatically updates remaining balance and debt status.

---

### 10. index.css - Global Styles

**Location**: `client/src/index.css`

**Color Scheme** (Light Mode):
- Primary: #B45309 (Warm Amber)
- Secondary: #F1F5F9 (Light Gray)
- Accent: #059669 (Emerald Green)
- Destructive: #DC2626 (Red)
- Background: #F8FAFC (Off-white)
- Card: #FFFFFF (White)

**Typography**:
- Headings: Poppins (600-700 weight)
- Body: Inter (400-500 weight)
- Monospace: JetBrains Mono (for numbers)

**Custom Classes**:
- `.debt-card`: Card styling with hover effects
- `.stat-box`: Statistics box styling
- `.progress-ring`: Circular progress visualization

---

### 11. App.tsx - Root Component

**Location**: `client/src/App.tsx`

Sets up the application structure:
- ThemeProvider (light theme)
- DebtProvider (global state)
- TooltipProvider (for UI tooltips)
- Router (page navigation)
- Toaster (for notifications)

---

### 12. index.html - HTML Template

**Location**: `client/index.html`

Includes:
- Google Fonts imports (Inter, Poppins, JetBrains Mono)
- Meta tags for responsiveness
- Root div for React
- Analytics script

---

## Key Technologies

| Technology | Purpose |
|-----------|---------|
| React 19 | UI framework |
| TypeScript | Type safety |
| Tailwind CSS 4 | Styling |
| shadcn/ui | UI components |
| Recharts | Data visualization |
| Wouter | Client-side routing |
| Sonner | Toast notifications |
| Lucide React | Icons |

---

## Data Flow

```
User Action (Add Debt)
    ↓
AddDebtDialog Component
    ↓
useDebtContext() hook
    ↓
useDebts() hook
    ↓
localStorage.setItem()
    ↓
State Update
    ↓
Components Re-render
    ↓
UI Updated
```

---

## Component Hierarchy

```
App
├── ThemeProvider
│   └── DebtProvider
│       └── TooltipProvider
│           ├── Router
│           │   └── Home
│           │       ├── Header
│           │       ├── DashboardStats
│           │       ├── Tabs
│           │       │   ├── Overview Tab
│           │       │   │   └── DebtCard (multiple)
│           │       │   ├── Debts Tab
│           │       │   │   ├── Filter Buttons
│           │       │   │   └── DebtCard (filtered)
│           │       │   └── Analytics Tab
│           │       │       └── DebtAnalytics
│           │       │           ├── PieChart
│           │       │           ├── BarChart
│           │       │           └── LineChart
│           │       └── AddDebtDialog
│           └── Toaster
```

---

## State Management Flow

**useDebts Hook** manages:
- `debts[]`: Array of all debt objects
- `loading`: Loading state during initialization

**localStorage** persists:
- All debt data under key `qarz_daftar_debts`
- Automatically synced on every change

**DebtContext** provides:
- Global access to all debt operations
- Available to any component via `useDebtContext()`

---

## Features Explained

### Debt Tracking
Each debt stores:
- Creditor name and contact info
- Original amount and remaining balance
- Interest rate percentage
- Due date
- Current status (Active/Overdue/Paid)
- Array of payment records

### Payment Management
Payments automatically:
- Reduce the remaining balance
- Update debt status if fully paid
- Mark debt as overdue if past due date
- Store date and optional notes

### Progress Visualization
Circular progress ring shows:
- Percentage of debt paid off
- Calculated as: (Total Paid / Original Amount) × 100
- Color-coded with primary amber color

### Analytics
Three charts provide insights:
- **Pie Chart**: Which creditors have largest debts
- **Bar Chart**: How much is owed by status
- **Line Chart**: Payment activity over time

### Data Export
JSON export includes:
- All debt records
- All payment history
- Timestamped filename for organization

---

## Styling System

### Color Variables (CSS)
```css
--primary: #B45309 (Warm Amber)
--accent: #059669 (Emerald)
--destructive: #DC2626 (Red)
--muted: #E2E8F0 (Gray)
--border: #E2E8F0
--background: #F8FAFC
--card: #FFFFFF
```

### Responsive Breakpoints
- Mobile: < 640px
- Tablet: 640px - 1024px
- Desktop: > 1024px

### Spacing System
Uses Tailwind's default spacing scale (4px base unit)

---

## Error Handling

**Toast Notifications** for:
- Successful operations (Add, Update, Delete)
- Validation errors
- Export success
- Failed operations

**Input Validation**:
- Required fields checked before submission
- Positive number validation
- Date format validation
- Empty string trimming

---

## Performance Optimizations

1. **localStorage Persistence**: Reduces API calls
2. **useCallback Hooks**: Prevents unnecessary re-renders
3. **Lazy Loading**: Components load on demand
4. **Memoization**: Computed values cached
5. **Responsive Images**: Optimized for different screen sizes

---

## Browser Compatibility

- Chrome/Edge: Full support
- Firefox: Full support
- Safari: Full support
- Mobile browsers: Full responsive support

---

## Future Enhancement Opportunities

1. **Backend Integration**: Replace localStorage with database
2. **User Authentication**: Multi-user support
3. **Recurring Payments**: Automatic payment scheduling
4. **Notifications**: Due date reminders
5. **Budget Planning**: Debt payoff projections
6. **Multiple Currencies**: International support
7. **Dark Mode**: Theme switching
8. **Mobile App**: React Native version

---

## Getting Started

### Installation
```bash
cd qarz-daftar
pnpm install
```

### Development
```bash
pnpm dev
```

### Build
```bash
pnpm build
```

### Type Checking
```bash
pnpm check
```

---

## File Sizes (Approximate)

| File | Size |
|------|------|
| useDebts.ts | 2.5 KB |
| DebtContext.tsx | 1.2 KB |
| Home.tsx | 3.8 KB |
| DebtCard.tsx | 4.2 KB |
| DebtAnalytics.tsx | 3.5 KB |
| AddDebtDialog.tsx | 2.8 KB |
| EditDebtDialog.tsx | 3.1 KB |
| PaymentDialog.tsx | 2.6 KB |
| DashboardStats.tsx | 2.1 KB |
| index.css | 4.5 KB |
| App.tsx | 1.8 KB |

---

## Code Quality

- **TypeScript**: Full type safety with no `any` types
- **ESLint**: Code style consistency
- **Prettier**: Automatic code formatting
- **Component Structure**: Modular and reusable
- **Naming Conventions**: Clear, descriptive names
- **Comments**: Inline documentation where needed

---

## Testing Recommendations

1. **Unit Tests**: Test individual components
2. **Integration Tests**: Test data flow between components
3. **E2E Tests**: Test complete user workflows
4. **Visual Tests**: Verify UI appearance across browsers

---

## Security Considerations

- **localStorage**: Client-side only, not for sensitive data
- **Input Sanitization**: All inputs validated
- **XSS Prevention**: React escapes content by default
- **CSRF Protection**: Not needed for static app

---

## Accessibility Features

- Semantic HTML structure
- ARIA labels where needed
- Keyboard navigation support
- Color contrast compliance
- Focus indicators on interactive elements

---

## License

MIT License - Free to use and modify

---

## Support & Documentation

For questions or issues:
1. Check component prop types in TypeScript
2. Review hook documentation above
3. Examine component examples in Home.tsx
4. Refer to shadcn/ui documentation for UI components
5. Check Recharts documentation for chart customization

---

**Last Updated**: January 19, 2026
**Version**: 1.0.0
**Status**: Production Ready

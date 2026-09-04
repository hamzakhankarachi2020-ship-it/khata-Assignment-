# Hamza Rusk Counter Desk

An offline-first operations dashboard for a bakery, rusk shop, or small retail counter. Hamza Rusk brings point-of-sale billing, product catalog management, customer credit, stock control, purchasing, sales history, and business reporting into one focused workspace.

The application is designed for quick counter work: fewer screens, clear stock signals, searchable records, and local data that remains available in the browser without a backend connection.

## Highlights

- **Dashboard overview** with today's sales, items moved, low-stock alerts, open customer credit, sales rhythm, and latest tickets.
- **Point of sale** with product search, cart quantity controls, customer selection, payment method selection, held carts, and instant stock deduction.
- **Product catalog** with SKU, category, unit, selling price, cost price, stock level, active status, search, filters, edit, delete, and CSV export.
- **Customer ledger** with contact information, area, opening balance, search, edit, delete, and CSV export.
- **Purchasing workflow** for recording supplier deliveries and increasing product stock automatically.
- **Inventory control** with low-stock thresholds, stock value, manual adjustments, adjustment reasons, and an adjustment trail.
- **Sales history** with receipt numbers, payment methods, status, date filtering by search, and CSV export.
- **Reports** for recorded revenue, gross profit, average ticket value, stock value, and product movement.
- **Shop settings** for store details, currency, address, receipt footer, low-stock alerts, and restoring demo data.
- **Responsive layout** with a desktop sidebar, compact mobile navigation, responsive tables, and mobile-friendly forms.
- **Offline-ready local workspace** with browser persistence through `localStorage` and no required server-side database.

## Complete Application Functions

| Area | Available functions |
| --- | --- |
| **Overview** | View daily revenue, completed tickets, units moved, low-stock count, open credit, sales rhythm, latest tickets, and items needing attention. |
| **Point of sale** | Search or scan-style product search, add products to cart, change quantities, remove items, select a customer, select cash/card/credit payment, hold a cart, restore a held cart, complete a sale, create a receipt number, and update stock. |
| **Products** | Add products, edit products, delete products, activate or deactivate catalog items, set SKU, category, unit, selling price, cost price, stock quantity, low-stock threshold, search products, filter by category, and export product records to CSV. |
| **Customers** | Add customer records, edit contact details, delete customers, store phone/email/area, record opening balance, search by name/phone/area, view customer status, and export the customer ledger to CSV. |
| **Purchases** | Record supplier deliveries, add invoice/reference numbers, select received products, enter quantities, calculate purchase totals, mark purchases as received, increase stock automatically, search supplier records, and export purchases to CSV. |
| **Inventory** | Search stock, view SKU and on-hand quantity, view low-stock threshold, calculate stock value at cost, identify healthy/low/out-of-stock items, make manual quantity adjustments, record adjustment reasons, and review recent adjustments. |
| **Sales history** | Search receipts, customers, and payment methods; view items, totals, status, and dates; and export filtered sales records to CSV. |
| **Reports** | Calculate recorded revenue, cost of goods, gross profit, average ticket, stock value, product movement, and export a summary report to CSV. |
| **Settings** | Update shop name, phone, currency, address, receipt footer, and low-stock alert preference; save settings locally; and restore the original demo dataset. |
| **Navigation and feedback** | Responsive sidebar, mobile menu, route-based navigation, active navigation state, search controls, confirmation dialogs, success toasts, empty states, loading/error boundary, and a branded 404 page. |

## Routes

| Route | Screen |
| --- | --- |
| `/` | Overview dashboard |
| `/pos` | Point of sale counter |
| `/sales` | Sales history |
| `/customers` | Customer ledger |
| `/products` | Product catalog |
| `/inventory` | Stock and adjustments |
| `/purchases` | Purchase records |
| `/reports` | Business reports |
| `/settings` | Workspace settings |

## Product Rules and Workflows

### Point of sale

1. Only active products can be added to the counter.
2. Products with zero stock cannot be added.
3. Cart quantities cannot exceed available stock.
4. Completing a sale creates a receipt, records the selected payment method, and deducts stock.
5. Empty carts cannot be completed.

### Inventory

1. A product is considered low stock when its quantity is at or below its configured threshold.
2. Stock can never become negative; adjustments are clamped at zero.
3. Every manual adjustment stores the product, quantity change, reason, and date.
4. Received purchases increase the related product stock immediately.

### Customers and credit

1. Customer records require a name and phone number.
2. Opening balances are stored against the customer record.
3. The dashboard calculates open credit from all customer balances.

### Data and privacy

1. Demo data is loaded on first visit.
2. Changes are persisted in the current browser using the `hamza-rusk-data` local-storage key.
3. Data is device-local and is not synchronized between browsers or computers.
4. The Settings page can restore the original demo dataset.

### Validation and safety rules

1. Product and customer forms reject required fields that are empty.
2. Prices, costs, quantities, and thresholds use non-negative numeric inputs.
3. A sale with no cart items is rejected with a user notification.
4. A purchase requires a supplier and a valid product selection.
5. An inventory adjustment requires a non-zero quantity change.
6. Delete actions require browser confirmation before changing local data.
7. CSV export safely quotes values and is available for products, customers, purchases, sales, and reports.
8. Route-level rendering is wrapped in an error boundary so a screen failure does not silently break the entire workspace.

## Technology Stack

### Frontend

- React 19
- TypeScript
- Vite 7
- Wouter for lightweight client-side routing
- TanStack Query for the application query client foundation
- Tailwind CSS 4 with the Tailwind Vite plugin
- Radix UI primitives for accessible interface building blocks
- Lucide React for interface icons
- React Hook Form and Zod-compatible form tooling
- DM Sans, Playfair Display, and DM Mono typography

### Workspace and tooling

- pnpm workspaces
- TypeScript project references
- ESLint-style component conventions through the existing UI structure
- Reusable UI primitives in `artifacts/hamza-rusk/src/components/ui`
- API, database, and generated client packages are kept in the workspace for future expansion

## Package Guide

### Root workspace

- `typescript`: TypeScript compiler and project-reference orchestration.
- `prettier`: Formatting support.
- `@replit/connectors-sdk`: Connector support available to the workspace.
- `pnpm-workspace.yaml`: Workspace package definitions, dependency catalogs, release-age policy, and platform overrides.

### `@workspace/hamza-rusk`

- `react`, `react-dom`: UI rendering.
- `vite`, `@vitejs/plugin-react`: Development server and production bundling.
- `wouter`: Client-side routing.
- `@tanstack/react-query`: Query client/provider foundation.
- `tailwindcss`, `@tailwindcss/vite`, `tw-animate-css`, `tailwind-merge`: Styling and utility-class support.
- `lucide-react`, `react-icons`: Interface icons.
- `@radix-ui/*`: Accessible primitives for dialogs, menus, forms, navigation, overlays, and controls.
- `react-hook-form`, `@hookform/resolvers`, `zod`: Form and validation foundations.
- `date-fns`: Date-related utility support.
- `recharts`: Charting support for reporting surfaces.
- `framer-motion`: Motion support available for interactive UI.
- `sonner`, `vaul`, `cmdk`, `embla-carousel-react`, `react-day-picker`, `input-otp`, `react-resizable-panels`, `next-themes`, `class-variance-authority`, and `clsx`: Reusable UI and interaction utilities.
- `@replit/vite-plugin-runtime-error-modal`, `@replit/vite-plugin-cartographer`, `@replit/vite-plugin-dev-banner`: Development-only Replit tooling.
- Windows native packages for `rollup`, `esbuild`, `lightningcss`, and Tailwind Oxide: Platform-specific build support on Windows.

### Backend and data packages

- `@workspace/api-server`: Express 5 API server with CORS, cookie parsing, structured logging through Pino, and source-map enabled runtime scripts.
- `@workspace/db`: Drizzle ORM, PostgreSQL driver, Drizzle Zod integration, and database schema exports.
- `@workspace/api-zod`: Shared Zod schemas and generated API types.
- `@workspace/api-client-react`: React Query-compatible generated API client package.
- `@workspace/api-spec`: OpenAPI source and Orval code generation configuration.

### Supporting workspace

- `@workspace/mockup-sandbox`: Separate Vite-based mockup preview environment with reusable Radix UI components, Framer Motion, Recharts, and development file watching.
- `scripts`: Workspace utility package and post-merge support script.
- `attached_assets`: Shared static assets used by the workspace.

## Project Structure

```text
artifacts/
	hamza-rusk/        Main React and Vite application
	api-server/        Lightweight API server workspace
	mockup-sandbox/    UI mockup and preview workspace
lib/
	api-client-react/  Generated React API client
	api-spec/          OpenAPI specification and Orval config
	api-zod/           Generated Zod API types
	db/                Drizzle database package and schema
scripts/             Workspace utility scripts
attached_assets/     Application assets
```

## Requirements

- Node.js 20 or newer
- pnpm 11 or newer

## Local Development

From the repository root:

```bash
pnpm install
```

The Vite configuration expects two environment variables:

```bash
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/hamza-rusk dev
```

On PowerShell:

```powershell
$env:PORT = "5173"
$env:BASE_PATH = "/"
pnpm --filter @workspace/hamza-rusk dev
```

Open `http://localhost:5173/` in your browser.

## Useful Commands

```bash
# Start the main frontend
pnpm --filter @workspace/hamza-rusk dev

# Type-check the main frontend
pnpm --filter @workspace/hamza-rusk typecheck

# Build the main frontend
pnpm --filter @workspace/hamza-rusk build

# Type-check all workspace packages
pnpm typecheck

# Build all workspace packages
pnpm build
```

## Deployment Notes

The main application is a Vite single-page application. For a static deployment, build the frontend and serve the generated output from `artifacts/hamza-rusk/dist/public`.

```bash
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/hamza-rusk build
```

When deploying under a subpath, set `BASE_PATH` to that path, for example `/khata-Assignment-/`, and configure the hosting provider to fall back to `index.html` for client-side routes.

## Current Scope

This repository currently focuses on a polished local counter experience. The application intentionally keeps records in browser storage, so authentication, multi-user access, cloud synchronization, server-side persistence, and payment gateway integration are outside the current scope.

## License

This project is private and intended for the associated project workspace.
# Oak Cafeteria - Robot Delivery System

Oak Cafeteria is a modern food ordering application designed for seamless integration with a robotic delivery system (Arduino-based). It allows customers to place orders from a digital menu and enables chefs to manage those orders and dispatch a delivery robot to specific tables.

## Project Overview

### Tech Stack
- **Frontend:** React 18, Vite, TypeScript, Tailwind CSS
- **Backend:** Node.js, Express (simple API for order validation and Arduino integration)
- **Database/Real-time:** Firebase Realtime Database (for orders, robot commands, and chef authentication)
- **Icons:** Lucide React
- **Notifications:** React Toastify
- **Routing:** React Router DOM

### Architecture
1.  **Customer Interface:** Customers browse menu items and combo meals, select a table (A-J), and place orders.
2.  **Order Processing:** Orders are first attempted to be sent to a local Express server (`server.js`) and then persisted to Firebase Realtime Database as a primary/backup storage.
3.  **Chef Dashboard:** A protected interface for chefs to view pending orders, mark them as "Preparing", and dispatch the robot once ready.
4.  **Robot Integration:** When a chef dispatches the robot, a command is sent to Firebase, and the local Express server's `/api/table` endpoint is updated. An Arduino-based robot can fetch the target table number from this endpoint.

## Getting Started

### Prerequisites
- Node.js installed
- Firebase project setup (credentials in `src/firebase/config.ts`)

### Building and Running
- **Install Dependencies:** `npm install`
- **Development Mode (Frontend):** `npm run dev` (runs Vite on default port)
- **Backend Server:** `npm start` (runs `server.js` on port 3001)
- **Build for Production:** `npm run build`
- **Linting:** `npm run lint`

## Project Structure
- `src/components`: UI components, including layout (Header/Footer) and ProtectedRoute.
- `src/context`: Auth and Theme contexts.
- `src/data`: `menuData.ts` contains the menu items and combo meal definitions.
- `src/firebase`: Firebase initialization and configuration.
- `src/hooks`: `useFirebase.ts` contains the core logic for orders and robot commands.
- `src/pages`: Main application views (Home, Menu, Auth, Chef Dashboard).
- `server.js`: Express backend providing an API for the robot and order fallback.

## Development Conventions
- **Typing:** Use TypeScript for all components and hooks. Interfaces for orders and menu items are defined in `src/data/menuData.ts` and `src/hooks/useFirebase.ts`.
- **Styling:** Tailwind CSS is used for styling. Global styles are in `src/index.css`.
- **Authentication:** Chef access is restricted via a "Chef Key" system (keys defined in `src/hooks/useFirebase.ts`).
- **Data Consistency:** Ensure that price changes in `src/data/menuData.ts` are mirrored in the `calculateTotal` function in `server.js`.

## Future Improvements (TODO)
- [ ] Implement a more robust database for order history.
- [ ] Add real-time robot status tracking.
- [ ] Sync menu data between frontend and backend to avoid duplication.
- [ ] Enhance chef authentication with Firebase Auth.

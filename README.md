## 🏗 Architecture & Technical Overview

This application is built as a modern, responsive Single Page Application (SPA) using **React.js**. To fulfill the requirement of operating without a backend, the app utilizes a simulated data layer with React's state management to provide a seamless, interactive user experience.

### 💻 Tech Stack
* **Frontend Framework:** React.js (Bootstrapped via Vite/CRA)
* **Styling:** Tailwind CSS for utility-first, highly responsive, and scalable UI design.
* **State Management:** React Hooks (`useState`, `useEffect`) and Context API for global state (e.g., current user role, assignment data).
* **Icons & Typography:** FontAwesome & Google Fonts (Inter, Plus Jakarta Sans).

### 📂 Folder Structure
The project follows a modular, feature-based directory structure to ensure clean, readable, and maintainable code:

```text
src/
├── assets/            # Static assets (images, icons, global CSS)
├── components/        # Reusable UI components
│   ├── common/        # Buttons, Modals, Toast notifications, Progress Bars
│   ├── layout/        # Sidebar, Header, Main Layout wrappers
│   ├── student/       # Student-specific components (AssignmentGrid, ProgressRing)
│   └── admin/         # Admin-specific components (CreateForm, DataTable)
├── context/           # React Context for global state (Auth/Role Context, Data Context)
├── data/              # Mock JSON data and initial state configurations
├── hooks/             # Custom React hooks (e.g., useAssignments, useToast)
├── utils/             # Helper functions (date formatting, ID generation)
├── App.jsx            # Root component handling role-based routing/rendering
└── index.js           # Application entry point

🧩 Component-Based Design
The UI is heavily compartmentalized to promote reusability and separation of concerns:

RoleProvider / DataProvider: Wraps the application to inject mock data and user roles seamlessly into any deeply nested component without prop-drilling.

Layout Component: Manages the responsive sidebar and mobile header, rendering dynamic children based on the active role.

Dashboard Views: Isolated view components (StudentDashboard.jsx and AdminDashboard.jsx) that consume data from the context and render the appropriate sub-components.

AssignmentCard: A highly reusable component that conditionally renders different action buttons based on the user's role (e.g., "Submit" for students, "Delete" for admins).

🔄 Data Flow & State Management (No Backend)
Since no external database is used, the application simulates a backend environment:

Initial State: On load, the app fetches initial mock data (Users, Assignments, Submissions) from the data/mockDb.js file.

Local Storage (Optional persistence): Changes to the state (creating an assignment, submitting coursework) are synced to the browser's localStorage using a custom useLocalStorage hook. This ensures data persists across page reloads during the review process.

Double Verification Flow: When a student submits an assignment, a temporary state (pendingSubmission) is triggered to open the confirmation modal. Upon confirmation, the central context state is updated, immediately triggering a UI re-render across all relevant components.

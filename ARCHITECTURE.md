"Independent UI Nexus" (Physical Codebase Separation)

📂Repository A: edutech-ui-system (The Library)
edutech-ui-system/
├── dist/                    # Production-ready build (JS/CSS/Types)
├── public/                  # Static assets (Favicons, base fonts)
├── src/
│   ├── theme/               # DESIGN TOKENS
│   │   ├── tokens.css       # Native CSS Variables (Colors, Spacing, Shadow)
│   │   ├── typography.css   # Font-face declarations and sizes
│   │   └── index.ts         # Exporting JS constants for Charting/Logic
│   ├── icons/               # ICON SYSTEM
│   │   ├── RoleIcons/       # StudentIcon, TeacherIcon, AdminIcon SVGs
│   │   ├── ActionIcons/     # Edit, Delete, Chevron, Search SVGs
│   │   └── IconRenderer.tsx # Wrapper to handle size, color, and stroke
│   ├── components/          # ATOMIC UI COMPONENTS
│   │   ├── Button/
│   │   │   ├── Button.tsx       # Component logic (variants, sizes)
│   │   │   ├── Button.css       # Scoped styling using var(--tokens)
│   │   ├── Card/
│   │   │   ├── Card.tsx
│   │   │   └── Card.css
│   │   └── Feedback/            # Skeleton, Loader, Toast UI
│   ├── modules/             # COMPLEX UI BLOCKS (Still stateless)
│   │   ├── Quiz/            # TimerDisplay, QuestionBox, OptionCard
│   │   ├── Charts/          # Recharts wrappers (Line, Bar, Radar)
│   │   └── Navigation/      # SidebarItem, NavbarBrand, UserMenu
│   ├── types/               # SHARED TYPES (Component Props)
│   │   └── common.ts        # Variant types: 'primary' | 'secondary' etc.
│   └── index.ts             # THE BARREL EXPORT (The entry point)
├── .babelrc                 # Compilation config
├── .npmignore               # Files to exclude from the published package
├── package.json             # Build scripts and versioning
├── tsconfig.json            # Strict TypeScript rules
└── .gitignore               # Files to exclude from the git repository


📂 Repository B: edutech-main-platform (The Application)
edutech-main-platform/
src/
├── assets/                 # Global static files (mostly role-specific imagery)
├── config/                 # App-wide settings
│   ├── constants.ts        # Boards (CBSE, ICSE), Grades, Subject lists
│   ├── endpoints.ts        # Centralized API route definitions
│   └── roles.ts            # Permission maps for the 5 roles
├── context/                # Global State
│   ├── AuthContext.tsx     # Handles Login, JWT, and User Role
│   └── NotificationContext.tsx # Global success/error toasts
├── features/               # BUSINESS ENGINE (The logic)
│   ├── study-plan/         
│   │   ├── hooks/          # useGeneratePlan, useMilestones
│   │   ├── services/       # planService.ts (API calls)
│   │   └── utils/          # Logic to map Board requirements
│   ├── testing/            
│   │   ├── hooks/          # useQuizEngine, useTimer
│   │   ├── state/          # Redux/Zustand for quiz progress
│   │   └── services/       # testService.ts
│   └── analytics/          
│       ├── hooks/          # usePerformanceData
│       └── utils/          # AI Insight processing logic
├── hooks/                  # Global Utility Hooks (useAuth, useLocalStorage)
├── layouts/                # ROLE-SPECIFIC SHELLS
│   ├── AdminLayout.tsx     # Sidebar: Institutions, Payments, Logs
│   ├── StudentLayout.tsx   # Sidebar: My Plan, Tests, Insights
│   ├── TeacherLayout.tsx   # Sidebar: Classroom, Question Bank, Grades
│   ├── ParentLayout.tsx    # Sidebar: Child Progress, Attendance
│   └── AppLayout.tsx       # Main Layout
├── lib/                    # SDK & Third-party Config
│   ├── axios.ts            # Interceptors (Attaches @edutech/ui tokens to headers)
│   └── react-query.ts      # Global cache settings
├── pages/                  # FINAL SCREEN ASSEMBLY
│   ├── admin/              # UserManagement.tsx, SystemHealth.tsx
│   ├── student/            # Dashboard.tsx, QuizView.tsx, Roadmap.tsx
│   ├── shared/             # Login.tsx, Profile.tsx, Unauthorized.tsx
│   └── index.ts            # Role-based router/traffic controller
├── services/               # Generic API services (Logging, Uploads)
├── types/                  # TYPESCRIPT DEFINITIONS
│   ├── models.ts           # Student, Teacher, Institution interfaces
│   └── api.ts              # API Response/Request generic types
└── App.tsx                 # Routing and Provider setup
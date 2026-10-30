Project 1 — ShipShape: Full-Stack Engineering Management Platform
Priority: P0 — Build this first.

This is your flagship conventional software project. Think of it as a smaller version of Linear or Jira.
Technology stack
| Layer | Technology |
|---|---|
| Frontend | Next.js, React, TypeScript |
| UI | Tailwind CSS, accessible component library |
| Backend | Node.js, TypeScript, Next.js Route Handlers or a separate API |
| Database | PostgreSQL |
| Database access | Prisma or Drizzle ORM |
| Authentication | Auth.js or a managed authentication provider |
| Validation | Zod |
| Testing | Vitest, React Testing Library, Playwright |
| Infrastructure | Docker, GitHub Actions |
| Deployment | Vercel or another suitable host; managed PostgreSQL |

Choose one ORM and one authentication approach. Don't add competing tools just to make the technology list longer.
What you will build
Users can create workspaces, manage projects, assign issues, comment on tasks, track progress, and collaborate with teammates.

The platform should support:
- Registration and authentication.
- Workspace and project creation.
- Issues with priority, status, assignee, and due date.
- Search, filtering, sorting, and pagination.
- Comments and activity history.
- Workspace membership and roles.
- A dashboard showing outstanding work.
- Responsive layouts.
- A basic notification system.

Modular architecture
shipshape/
├── apps/
│   └── web/
│       └── src/
│           ├── app/
│           │   ├── (auth)/
│           │   ├── dashboard/
│           │   ├── workspaces/[workspaceId]/
│           │   ├── projects/[projectId]/
│           │   └── api/
│           ├── components/
│           │   ├── ui/
│           │   ├── forms/
│           │   └── layout/
│           ├── features/
│           │   ├── auth/
│           │   ├── workspaces/
│           │   ├── projects/
│           │   ├── issues/
│           │   ├── comments/
│           │   └── notifications/
│           └── lib/
│               ├── auth/
│               ├── db/
│               ├── validation/
│               └── observability/
├── packages/
│   ├── database/
│   │   ├── schema/
│   │   ├── migrations/
│   │   └── queries/
│   ├── shared/
│   │   ├── types/
│   │   └── validation/
│   └── testing/
├── tests/
│   ├── integration/
│   └── e2e/
├── docker-compose.yml
├── .github/workflows/
└── README.md

This is a proposed structure, not something you must copy mechanically. Start with a single Next.js application and shared modules. Add a monorepo structure only if it provides real value.
How the modules should work
1. Authentication module

Responsible for identity, sessions, and sign-in flows.

It should not decide whether a user can access every resource by itself. Authentication tells you who the user is; authorization determines what that user may do.

2. Workspace module

Responsible for workspace creation, membership, and roles.
createWorkspace()
addMember()
removeMember()
changeMemberRole()
getWorkspaceForUser()

The module should enforce membership rules and prevent unauthorised users from accessing private workspace information.

3. Issue module

Responsible for the main business logic:
createIssue()
updateIssue()
assignIssue()
changeIssueStatus()
listIssues()
searchIssues()

Keep business rules out of UI components. For example, an issue-status transition should be validated on the server even if the frontend already prevents invalid transitions.

4. Database module

Responsible for schema definitions, migrations, and database access.

Start with entities such as:
User
Workspace
WorkspaceMember
Project
Issue
Comment
ActivityEvent
Notification
Define foreign keys, uniqueness constraints, indexes, and deletion rules deliberately.

5. API module

Responsible for HTTP requests, input validation, authentication checks, calling business logic, and producing consistent responses.

6. Testing module

Tests important business rules and security boundaries. For example, a user from Workspace A must not be able to read or update a private issue belonging to Workspace B.
What makes this a senior-level project?
Don't stop at CRUD functionality.

Demonstrate that you can:
- Design cursor-based pagination and explain when offset pagination is sufficient.
- Prevent unauthorised cross-workspace access.
- Handle concurrent updates without silently overwriting changes.
- Add database indexes based on actual query patterns.
- Implement consistent API errors and structured logs.
- Test critical workflows.
- Explain how you would add background jobs and notifications at higher scale.
- Document the trade-offs between a modular monolith and microservices.
Completion target: a working live application, a well-organised public repository, meaningful automated tests, a deployment pipeline, and an architecture document.

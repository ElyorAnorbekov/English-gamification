UI_GUIDE.md — Final 20-Section Implementation Plan

Project: English Teacher Gamification System

DOCUMENT PURPOSE

UI_GUIDE.md is the authoritative UI implementation specification for the project.

It defines how the application interface must be structured, behave, communicate with users, handle states, and interact with application data.

The implementation must remain consistent with:
- PROJECT_REQUIREMENTS.md
- DATABASE.md
- GAMIFICATION.md

No UI implementation may silently contradict these documents.

If a requirement is configurable or defined elsewhere, the UI must consume the authoritative value or logic rather than inventing its own version.


CORE PROJECT VALUES

- Teacher-first
- Maximum 40 teacher accounts
- Simple
- Fast
- Lightweight
- Responsive
- Accessible
- Secure
- Data-accurate
- Maintainable
- Scalable within the intended project size
- Free/lightweight services where practical
- No unnecessary complexity
- No student application login
- Teacher-level ownership and isolation
- Teacher group-level statistics
- Dynamic Journal Core
- Practical classroom usability
- No unnecessary enterprise infrastructure
- Consistency with PROJECT_REQUIREMENTS.md, DATABASE.md, and GAMIFICATION.md


SECTION 1 — UI Architecture & Core Principles

Define the fundamental UI architecture and implementation rules.

Include:
- Teacher-first architecture
- Maximum 40 teacher accounts
- Simple and practical classroom workflows
- Fast interaction
- Consistent UI behavior
- Responsive design
- Accessibility
- Security
- Data accuracy
- Maintainability
- Scalability appropriate to the project
- Minimal visual complexity
- Practical classroom usage
- Clear separation between UI, business logic, and data access
- Reusable component architecture
- No unnecessary infrastructure or dependencies

Core principle:
The UI must make frequent teacher workflows faster and clearer rather than adding visual complexity.

Completion criteria:
Section 1 is complete only when the fundamental UI architecture and all core principles are explicitly defined and consistently applied across the application.


SECTION 2 — Application Shell & Global Layout

Define the complete application shell.

Include:
- App shell
- Header
- Sidebar
- Main content area
- Page containers
- Global actions
- Breadcrumbs where useful
- Global search where required
- Desktop layout
- Tablet layout
- Mobile layout
- Navigation placement
- Responsive layout behavior
- Global loading behavior
- Global error behavior

Boundary:
Section 2 defines where major UI elements are placed.
Detailed navigation behavior belongs to Section 3.


SECTION 3 — Navigation & Information Architecture

Define how teachers move through the application.

Primary navigation:
- Dashboard
- Groups
- Students
- Journal
- Homework
- Payments
- Gamification
- Analytics
- Reports
- Activity
- Settings

Include:
- Navigation hierarchy
- Active states
- Group context
- Group selector where required
- Back navigation
- Deep links
- Mobile navigation
- Navigation consistency
- Breadcrumb behavior
- Route protection
- Unauthorized navigation behavior
- Empty-state navigation
- Navigation persistence where appropriate

Navigation must remain predictable and should minimize the number of steps required for common classroom workflows.


SECTION 4 — Design System & Visual Language

Define the complete visual design system.

Include:
- Typography
- Font family
- Font scale
- Font weights
- Line height
- Spacing system
- Grid system
- Borders
- Border radius
- Shadows
- Icons
- Icon sizing
- Containers
- Cards
- Dividers
- UI density
- Visual hierarchy
- Design tokens
- Breakpoints
- Layering and z-index rules
- Motion/transition principles

Design tokens must be reusable and centrally defined rather than independently chosen by individual pages.

The design system must prevent inconsistent spacing, typography, colors, sizing, and component behavior.


SECTION 5 — Color System & Semantic States

Define how colors communicate meaning.

Include:
- Primary colors
- Neutral colors
- Success
- Warning
- Error
- Information
- Attendance states
- Homework states
- Payment states
- Gamification states
- Disabled states
- Selected states
- Hover/focus states
- Contrast requirements
- Semantic color tokens

Primary implementation:
- Light theme is the default.
- Dark theme must not be implemented unless explicitly required by project requirements.

Colors must be semantic and consistent rather than arbitrary.

The same semantic state must use the same visual language throughout the application.


SECTION 6 — Reusable Components

Define the reusable UI component library.

Include:
- Buttons
- Inputs
- Textareas
- Selects
- Dropdowns
- Tables
- Cards
- Tabs
- Modals
- Drawers
- Badges
- Tooltips
- Toasts
- Pagination
- Search
- Filters
- Date picker
- Loading components
- Skeletons
- Empty states
- Error states
- Confirmation dialogs
- File upload components
- Progress indicators

Every reusable component must define:
- Purpose
- Variants
- States
- Validation behavior where applicable
- Accessibility behavior
- Responsive behavior
- Loading behavior
- Error behavior

Components must be reused instead of recreated independently on different pages.


SECTION 7 — Authentication & Teacher Account

Define teacher account UI and authentication behavior.

Include:
- Login
- Session handling
- Logout
- Authentication errors
- Unauthorized states
- Teacher profile
- Teacher settings
- Language settings
- Account status
- Account restrictions
- Session expiration behavior
- Secure redirect behavior

Important:
- Teachers have application accounts.
- Maximum application teacher accounts: 40.
- Students do not have direct application login.
- Authentication identity must remain consistent with DATABASE.md.
- Frontend authentication state must not replace database authorization.
- Teacher ownership must be enforced at the database/security layer.


SECTION 8 — Dashboard

Define the main teacher dashboard.

Include:
- Today's lessons
- Current group context where applicable
- Groups overview
- Cross-group summary
- Attendance summary
- Homework summary
- Points/XP overview
- Rankings overview
- Recent activity
- Notifications
- Quick actions
- Loading states
- Empty states
- Error states
- Permission states

The dashboard must prioritize information required during normal teaching workflows.

Dashboard statistics must use authoritative application data.


SECTION 9 — Group Management

Define the complete group lifecycle UI.

Include:
- Group list
- Create group
- Edit group
- Archive group
- Group details
- Student count
- Group statistics
- Group switching
- Group context
- Group-level access behavior
- Search
- Filters
- Empty states
- Loading states
- Error states
- Confirmation dialogs

Destructive actions such as archive/delete must use confirmation when appropriate.

Archived groups must remain consistent with historical data requirements in DATABASE.md.


SECTION 10 — Student Management

Define the complete student lifecycle UI.

Include:
- Student list
- Add student
- Edit student
- Archive student
- Student profile
- Academic information
- Attendance
- Homework
- Payments
- Gamification
- Teacher notes
- History
- Search
- Filters
- Loading states
- Empty states
- Error states
- Permission states

Student information must be scoped to the authenticated teacher's authorized groups/data.

Historical records must not be unnecessarily destroyed when a student is archived.


SECTION 11 — Dynamic Journal Core

This is one of the most important UI components of the project.

Define in detail:
- Journal architecture
- Group selection
- Current group context
- Date selection
- Lesson selection
- Student rows
- Lesson columns
- Attendance
- Present
- Absent with reason
- Absent without reason
- Late
- Homework
- Points
- XP
- Inline actions
- Quick actions
- Auto-save
- Save status
- Safe optimistic UI where appropriate
- Synchronization state
- Error recovery
- Retry behavior
- Undo where appropriate
- Journal filters
- Search where required
- Large-group performance
- Mobile journal behavior
- Loading states
- Empty states
- Permission states
- Network failure states
- Concurrent update handling

Critical synchronization requirements:
- Prevent duplicate attendance records.
- Prevent duplicate homework submissions.
- Prevent accidental duplicate actions.
- Preserve unsaved changes safely.
- Clearly communicate Saving, Saved, Failed, and Retrying states.
- Handle synchronization failures without silently losing teacher input.
- Handle concurrent updates safely.
- Allow safe retry after failed operations.

The Journal must be optimized for real classroom usage and rapid teacher interaction.

The Journal must not invent business rules. Point and XP effects must follow GAMIFICATION.md.


SECTION 12 — Attendance & Lesson Management

Define lesson and attendance workflows.

Include:
- Lesson creation
- Lesson editing
- Lesson date/time
- Attendance statuses
- Present
- Absent with reason
- Absent without reason
- Late
- Absence reason input
- Absence reason history
- Attendance history
- Attendance statistics
- Attendance correction
- Correction workflow
- Confirmation states
- Error handling
- Retry behavior

Attendance-related point and XP effects must follow GAMIFICATION.md.

Attendance corrections must preserve historical integrity where required by DATABASE.md.


SECTION 13 — Homework Management

Define the complete homework workflow.

Include:
- Homework creation
- Homework assignment
- Sequential homework upload
- One primary upload action
- Upload progress
- File validation
- File upload
- Upload failure recovery
- Prevent duplicate uploads
- Homework list
- Homework statuses
- Evaluation
- Points
- XP
- Homework history
- Search
- Filters
- Loading states
- Empty states
- Error handling
- Retry behavior

Homework business rules must follow GAMIFICATION.md and PROJECT_REQUIREMENTS.md.

The UI must not hardcode homework point/XP rules that are defined elsewhere.


SECTION 14 — Payments & Financial UI

Define teacher-facing financial functionality.

Include:
- Payment entry
- Payment history
- Payment status
- Due indicators
- Filters
- Search
- Monthly summaries
- Payment corrections
- Confirmation dialogs
- Error handling
- Retry behavior
- Historical financial records
- Financial empty states
- Financial loading states

Payment data must remain independent from gamification unless explicitly defined otherwise by business rules.

Financial records must remain historically traceable and must not be silently overwritten.


SECTION 15 — Gamification UI

Define the UI for the complete gamification system.

Include:
- Points
- XP
- Levels
- Monthly levels
- Rankings
- Badges
- Achievements
- Streaks
- Rewards
- Progress indicators
- Group leaderboard
- Student progress
- Ranking states
- Achievement states
- Badge states
- Level progress

Critical rules:
- The UI must implement the business rules defined in GAMIFICATION.md.
- The UI must not invent conflicting gamification rules.
- The UI must not duplicate authoritative gamification calculations unnecessarily.
- Point values must not be hardcoded in UI components unless explicitly defined as presentation-only constants.
- XP values must not be hardcoded in UI components.
- Level thresholds must not be hardcoded in UI components.
- Badge requirements must not be hardcoded in UI components.
- Achievement requirements must not be hardcoded in UI components.
- Streak rules must not be hardcoded in UI components.
- Rewards rules must not be hardcoded in UI components.

Displayed gamification data must originate from authoritative application/database data or approved gamification logic.


SECTION 16 — Analytics & Statistics

Define teacher-facing analytics.

Include:
- Group-level statistics
- Student-level details where required for the teacher
- Attendance analytics
- Homework analytics
- Payment analytics
- Points analytics
- XP analytics
- Level analytics
- Ranking analytics
- Trends
- Monthly statistics
- Date filters
- Group filters
- Student filters where appropriate
- Charts
- Tables
- Performance indicators
- Empty states
- Loading states
- Error states

Analytics must use authoritative database data and remain consistent with DATABASE.md.

Teachers must only see analytics derived from data they are authorized to access.

Cross-teacher analytics are prohibited.


SECTION 17 — Reports, Certificates, Exports & Telegram

Define all external output workflows.

Include:
- Reports
- Report generation
- Certificate generation
- Certificate history
- Export
- Telegram reporting
- Telegram status
- Success states
- Failure states
- Retry behavior
- File references
- Upload progress where applicable
- Loading states
- Empty states
- Error states

Important:
- Telegram messages are outputs, not the database source of truth.
- File storage behavior must remain consistent with DATABASE.md.
- Telegram failure must not silently corrupt or roll back successful core database operations unless explicitly required by the business workflow.
- Reporting operations should be retryable where practical.
- Generated files must have clear ownership and access controls.


SECTION 18 — Activity, Notifications & Teacher Notes

Define teacher-facing historical and communication UI.

Include:
- Activity timeline
- Notifications
- Read/unread states
- Teacher notes
- Important events
- Filters
- Search
- Historical records
- Loading states
- Empty states
- Error states
- Retry behavior where applicable

Activity and audit concepts must remain consistent with DATABASE.md.

Teacher notes must remain scoped to the authorized teacher and applicable student/group.


SECTION 19 — Forms, Validation, UX States, Accessibility & Security

Define cross-cutting UI quality requirements.

FORMS AND VALIDATION:
- Required fields
- Input validation
- Type validation
- Range validation
- Validation messages
- Inline validation where appropriate
- Success feedback
- Error feedback
- Confirmation dialogs
- Delete protection
- Duplicate submission protection

UX STATES:
- Loading
- Skeleton loading
- Empty state
- Error state
- Network failure
- Permission failure
- Authentication failure
- Retry behavior
- Save failure
- Synchronization failure
- Offline/unstable network feedback where practical

Confirmation rule:
Confirmation dialogs shall be used primarily for destructive, irreversible, or high-impact actions.
Routine classroom actions should remain fast and should not require unnecessary confirmation.

ACCESSIBILITY:
- Keyboard navigation
- Focus states
- Screen-reader support
- Semantic HTML
- Color contrast
- Accessible labels
- Accessible interactive controls
- Focus visibility
- Form error accessibility
- Touch target usability

SECURITY:
- Secure rendering
- No sensitive data leakage
- No trust in frontend-only authorization
- Permission-aware UI
- Safe file handling
- Secure error messages
- No credentials in frontend source
- No exposure of privileged keys
- Safe handling of user-generated content

The frontend must never be treated as the only security layer.


SECTION 20 — Performance, Responsive Behavior & Implementation Acceptance

Define the final implementation standards.

PERFORMANCE:
- Fast initial load
- Minimal dependencies
- Lazy loading where appropriate
- Pagination for large datasets
- Debouncing for search/input
- Efficient database queries
- No unnecessary API calls
- Avoid N+1 query patterns
- Avoid unnecessary re-renders
- Optimize the Dynamic Journal Core
- Avoid loading entire historical datasets unnecessarily
- Prefer server/database-side filtering for large datasets
- Keep transactions short where applicable
- Measure performance using realistic workloads

Initial performance targets:
- Common journal database queries should target <= 500 ms database-side execution under expected workload.
- Simple lookup queries should target <= 100 ms database-side execution where practical.
- Common teacher interactions should feel immediate under normal conditions.
- Large datasets must use pagination, controlled loading, or virtualization where appropriate.

RESPONSIVE BEHAVIOR:
- Desktop
- Tablet
- Mobile
- Small-screen Journal
- Mobile tables
- Touch-friendly controls
- Responsive modals
- Responsive drawers
- Responsive navigation
- Appropriate content density for smaller screens

IMPLEMENTATION STANDARDS:
- Reusable components
- Consistent naming
- Maintainable folder structure
- Clear separation between UI and business logic
- Clear separation between UI and database access
- No business-rule duplication
- No hardcoded production data
- No hardcoded configurable business rules
- No unnecessary libraries
- No unnecessary animations
- No unnecessary infrastructure
- No direct database access patterns that bypass approved security architecture
- No frontend-only authorization
- No duplicated source-of-truth data

CONFIGURABLE BUSINESS RULES:
The UI must not hardcode:
- Point values
- XP values
- Level thresholds
- Badge requirements
- Achievement requirements
- Streak rules
- Reward rules
- Other configurable gamification rules

These values must come from authoritative configuration or application logic defined by the project architecture.

CROSS-DOCUMENT CONSISTENCY:
- PROJECT_REQUIREMENTS.md defines product requirements and scope.
- DATABASE.md defines data architecture, persistence, relationships, security, and database behavior.
- GAMIFICATION.md defines gamification business rules.
- UI_GUIDE.md defines UI behavior, visual standards, interaction patterns, and implementation standards.
- No document may silently contradict another document.
- The implementation must not invent missing business rules in the UI.
- When requirements conflict, explicit higher-level project requirements and authoritative business rules take precedence.
- Changes affecting multiple documents must be reflected consistently across all relevant documentation.

FINAL ACCEPTANCE CRITERIA:

Every major UI feature must be:
- Functional
- Responsive
- Accessible
- Secure
- Performant
- Consistent
- Error-handled
- Database-connected where required
- Business-rule compliant
- Ownership-aware
- Tested against realistic teacher workflows
- Compatible with the project's maximum 40-teacher scale

The implementation is complete only when all 20 sections are satisfied and the resulting UI is practical for real classroom use.

FINAL IMPLEMENTATION PRINCIPLE:

The application should be as simple as possible while still satisfying all defined functional, security, data, gamification, performance, and usability requirements.

Do not add features, infrastructure, dependencies, UI complexity, or workflows that are not required by the project specification.

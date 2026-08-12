TECH_STACK.md — FINAL 20-SECTION IMPLEMENTATION PLAN

Project: English Teacher Gamification System

Core project values:
- Teacher-first
- Maximum 40 teachers
- Simple
- Fast
- Lightweight
- Responsive
- Accessible
- Secure
- Data-accurate
- Maintainable
- Scalable
- Free/lightweight services where practical
- No unnecessary complexity
- No student login
- Teacher group-level statistics
- Dynamic Journal Core
- PostgreSQL/Supabase as the database source of truth
- Technology choices must remain consistent with PROJECT_REQUIREMENTS.md, DATABASE.md, UI_GUIDE.md, GAMIFICATION.md, and API_SPECIFICATION.md

Technology decision principles:
- Prefer stable, well-supported technologies.
- Prefer the smallest practical technology stack.
- Prefer free or low-cost services where practical.
- Do not add a dependency unless it solves a real project requirement.
- Avoid duplicate libraries that solve the same problem.
- Avoid enterprise infrastructure that is unnecessary for the intended scale.
- Technology choices must support maintainability and predictable deployment.
- No technology may silently introduce a conflicting architecture or business rule.


SECTION 1 — Technology Architecture & Core Principles

Define the complete technology architecture.

Include:
- Overall system architecture
- Frontend
- Backend/API layer
- Database
- Authentication
- Storage
- Server-side functions
- External integrations
- Testing
- Deployment
- Monitoring
- Development tooling
- Maximum 40 teachers
- Lightweight architecture
- No unnecessary microservices
- Source-of-truth principle
- Completion criteria


SECTION 2 — Frontend Framework & Application Runtime

Define the frontend framework and runtime.

Include:
- Selected framework
- Programming language
- Runtime requirements
- Version policy
- Routing
- Rendering strategy
- Client/server boundaries where applicable
- Browser support
- Build strategy
- Development server
- Production build
- Compatibility with UI_GUIDE.md
- Compatibility with Dynamic Journal Core

The selected framework must be stable, maintainable, and appropriate for the project scale.


SECTION 3 — UI Framework, Styling & Design System Implementation

Define the technologies used to implement the UI design system.

Include:
- CSS strategy
- Component styling
- Design tokens
- Typography
- Responsive utilities
- Theme support if required
- Accessibility support
- Component library policy
- Icon library
- Animation policy
- UI density
- Compatibility with UI_GUIDE.md

The stack must not introduce unnecessary visual complexity.


SECTION 4 — Component Architecture & Reusability

Define the frontend component architecture.

Include:
- Reusable components
- Layout components
- Form components
- Data display components
- Journal components
- Gamification components
- Analytics components
- Modal/drawer components
- Loading/error/empty-state components
- Component composition
- Naming conventions
- Component boundaries
- Shared vs feature-specific components
- Avoiding duplicated UI logic

Components must remain consistent with UI_GUIDE.md.


SECTION 5 — State Management & Data Fetching

Define how application state and server data are managed.

Include:
- Local UI state
- Server state
- Form state
- Authentication state
- Group context
- Journal state
- Gamification state
- Cache strategy
- Data invalidation
- Optimistic updates
- Rollback behavior
- Avoiding unnecessary global state
- Avoiding duplicated server data

Server-authoritative data must remain consistent with DATABASE.md and API_SPECIFICATION.md.


SECTION 6 — Forms, Validation & Type Safety

Define the technology approach for forms and validation.

Include:
- Form library if required
- Schema validation
- Type-safe request/response handling
- Client-side validation
- Server-side validation
- Database constraint compatibility
- Error mapping
- Required fields
- Enum validation
- Date/time validation
- Numeric validation
- File validation
- Shared types/schemas where practical

Client validation must never replace server/database validation.


SECTION 7 — Backend & API Technology

Define the backend/API technology stack.

Include:
- API architecture
- Supabase client usage
- Server-side functions
- RPC/database functions where appropriate
- Edge Functions where required
- Authentication integration
- Authorization
- RLS compatibility
- Validation
- Error handling
- Business logic boundaries
- External API communication
- API_SPECIFICATION.md compatibility

The architecture must avoid creating a redundant backend layer unless genuinely required.


SECTION 8 — Database & Data Access Technology

Define the database technology.

Include:
- PostgreSQL
- Supabase
- SQL
- Database migrations
- Foreign keys
- Constraints
- Indexes
- Transactions
- Functions
- Triggers
- RLS
- Database types
- Query strategy
- Connection/access model
- Compatibility with DATABASE.md

PostgreSQL remains the authoritative persistent data source.


SECTION 9 — Authentication & Authorization Technology

Define authentication and authorization technologies.

Include:
- Supabase Authentication
- Session management
- Authenticated user ID
- Teacher profile mapping
- RLS
- Authorization boundaries
- Service-role access
- Secret handling
- Account status
- Logout/session expiration
- No student login

Authentication and authorization must remain consistent with API_SPECIFICATION.md and DATABASE.md.


SECTION 10 — Storage & File Management Technology

Define file storage architecture.

Include:
- Supabase Storage
- Certificate files
- Certificate templates
- Homework files
- Export files
- Import files
- File metadata
- Storage paths
- Access control
- Signed URLs where appropriate
- File validation
- File size limits
- File type restrictions
- Temporary file handling
- File cleanup
- Database references

Binary files should not be unnecessarily stored directly in relational tables.


SECTION 11 — Gamification Technology Architecture

Define technologies supporting gamification.

Include:
- Point transactions
- XP transactions
- Levels
- Monthly levels
- Rankings
- Badges
- Achievements
- Streaks
- Rewards
- Gamification events
- Rule configuration
- Transaction processing
- Idempotency
- Atomic operations
- Derived statistics
- Event processing

Critical rule:
Technology must implement GAMIFICATION.md rules and must not invent business rules.


SECTION 12 — Dynamic Journal Core Technology

Define the technical implementation of the Journal.

Include:
- Large interactive data grid/table strategy
- Group selection
- Date selection
- Student rows
- Attendance updates
- Homework updates
- Inline actions
- Fast updates
- Optimistic UI
- Rollback
- Debouncing where appropriate
- Efficient data fetching
- Pagination/virtualization where necessary
- Mobile behavior
- Touch interaction
- Rendering optimization
- Transaction integrity

The Journal is a critical performance area and must receive special optimization attention.


SECTION 13 — Analytics, Charts & Reporting Technology

Define technologies for analytics.

Include:
- Charts
- Tables
- Aggregations
- Date-range filtering
- Group statistics
- Student statistics
- Attendance analytics
- Homework analytics
- Payment analytics
- Points/XP analytics
- Ranking analytics
- Monthly statistics
- Report-ready data
- Lightweight charting solution
- Avoiding unnecessary analytics infrastructure

Analytics must use authoritative data or reproducible derived data.


SECTION 14 — Telegram & External Integration Technology

Define external integration technology.

Include:
- Telegram Bot API integration
- Server-side credential handling
- Edge Functions/server-side communication
- Group-level reporting
- Message formatting
- Delivery status
- Retry behavior
- Failure handling
- Idempotency where appropriate
- External service timeout handling
- Logging

Telegram must remain an output channel, not the system of record.


SECTION 15 — Testing Technology & Quality Assurance

Define the testing stack and strategy.

Include:
- Unit testing
- Integration testing
- API testing
- Database testing
- RLS testing
- Component testing
- Dynamic Journal testing
- Gamification rule testing
- End-to-end testing
- Authentication testing
- File/storage testing
- Telegram integration testing
- Mocking strategy
- Test data
- Test environment
- CI-compatible testing

Critical business rules must have automated tests.


SECTION 16 — Development Tooling, Code Quality & Type Safety

Define development tooling.

Include:
- Package manager
- TypeScript/type checking if selected
- Linter
- Formatter
- Git
- Pre-commit checks where justified
- Environment variable validation
- Code organization
- Import conventions
- Naming conventions
- Strictness settings
- Dependency auditing
- Build validation
- CI checks

Tooling must remain lightweight and avoid unnecessary developer overhead.


SECTION 17 — Dependency Management & Third-Party Services

Define dependency policy.

Include:
- Approved dependency principles
- Dependency selection criteria
- Version pinning/ranges
- Security updates
- Deprecated dependency handling
- Duplicate-library prevention
- Bundle-size awareness
- Free-tier awareness
- Third-party service evaluation
- Vendor lock-in considerations
- Removal of unused dependencies
- No unnecessary services

Every major dependency must have a clear reason to exist.


SECTION 18 — Performance, Scalability & Resource Management

Define technical performance requirements.

Include:
- Initial load performance
- Bundle size
- Code splitting
- Lazy loading
- Database query efficiency
- API payload efficiency
- Caching
- Journal performance
- Ranking performance
- Analytics performance
- Image/file optimization
- Memory usage
- Avoiding unnecessary re-renders
- N+1 query prevention
- Concurrent operations
- Scalability to the intended project size

The system must remain lightweight before introducing advanced infrastructure.


SECTION 19 — Security, Environment Configuration & Secrets

Define technology-level security standards.

Include:
- Environment variables
- Public vs private configuration
- Supabase anon/publishable key usage where applicable
- Service-role key protection
- Telegram credentials
- Storage credentials
- No secrets in source code
- No secrets in Git
- Secure API calls
- Dependency security
- Input validation
- Output safety
- File security
- RLS
- Production access control
- Security logging
- Backup/security compatibility

The frontend must never receive credentials capable of bypassing authorization.


SECTION 20 — Build, Deployment Compatibility, Governance & Final Acceptance

Define final technology standards.

Build:
- Development build
- Production build
- Environment-specific configuration
- Build validation
- Migration compatibility
- Static asset handling
- Error reporting where appropriate

Deployment compatibility:
- Supabase
- Frontend hosting
- Edge/server functions
- Environment variables
- Database migrations
- Storage
- Telegram integration
- Domain/HTTPS requirements where applicable

Governance:
- Technology decisions must be documented.
- Major dependency changes must be reviewed.
- Production technology changes must be reproducible.
- No undocumented infrastructure.
- No unnecessary services.
- No silent framework/library replacement.
- Technology must remain compatible with all project documentation.

Cross-document consistency:
- PROJECT_REQUIREMENTS.md defines product requirements.
- DATABASE.md defines data architecture and persistence.
- GAMIFICATION.md defines gamification business rules.
- UI_GUIDE.md defines UI implementation behavior.
- API_SPECIFICATION.md defines communication contracts.
- TECH_STACK.md defines the approved technology architecture.
- Each document is authoritative within its own domain.
- No document may silently contradict another document.
- Undefined requirements must not be invented by the implementation.

Final acceptance criteria:

The technology stack is complete only when:
- All selected technologies have a clear purpose.
- Frontend architecture is defined.
- Backend/API architecture is defined.
- PostgreSQL/Supabase architecture is defined.
- Authentication is defined.
- Storage is defined.
- Gamification implementation technology is defined.
- Dynamic Journal technology is defined.
- Analytics technology is defined.
- Telegram integration technology is defined.
- Testing technology is defined.
- Development tooling is defined.
- Dependency policy is defined.
- Performance requirements are defined.
- Security requirements are defined.
- Deployment compatibility is defined.
- Environment configuration is defined.
- No unnecessary infrastructure is introduced.
- The stack supports maximum 40 teachers.
- The stack remains lightweight and maintainable.
- The stack is consistent with PROJECT_REQUIREMENTS.md, DATABASE.md, UI_GUIDE.md, GAMIFICATION.md, and API_SPECIFICATION.md.
- The implementation does not invent undefined business rules.

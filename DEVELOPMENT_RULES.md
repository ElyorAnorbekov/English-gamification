DEVELOPMENT_RULES.md — FINAL 20-SECTION IMPLEMENTATION PLAN

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

Authoritative project documents:
- PROJECT_REQUIREMENTS.md — product requirements
- DATABASE.md — database architecture, persistence, integrity, and data rules
- UI_GUIDE.md — UI behavior and implementation standards
- GAMIFICATION.md — gamification business rules
- API_SPECIFICATION.md — API and communication contracts
- TECH_STACK.md — approved technology stack
- DEVELOPMENT_RULES.md — development and coding rules

Development principle:
The implementation must follow the project documents as a coordinated specification. Developers and AI coding agents must not invent, silently change, duplicate, or contradict requirements that are already defined elsewhere.


SECTION 1 — Development Philosophy & Core Principles

Define the fundamental development rules for the project.

Include:
- Teacher-first development
- Correctness before unnecessary complexity
- Simple solutions first
- Performance-conscious implementation
- Security by design
- Data integrity first
- Maintainable code
- Reusable architecture
- Explicit business logic
- Clear separation of concerns
- Minimal dependencies
- No unnecessary infrastructure
- Maximum 40 teacher accounts
- Practical classroom usage
- Completion criteria

The implementation must optimize for reliability and maintainability rather than technical novelty.


SECTION 2 — Project Structure & Folder Architecture

Define the approved project directory structure.

Include:
- Application root structure
- Pages/routes
- Components
- Features/modules
- Hooks
- Services
- API layer
- Database access
- Types
- Schemas
- Utilities
- Configuration
- Tests
- Assets
- Supabase/migrations
- Edge/server functions where applicable
- Shared components
- Feature-specific components
- Naming conventions

The structure must provide clear separation between:
- UI
- application logic
- business logic
- data access
- external integrations
- configuration
- tests


SECTION 3 — Naming Conventions & Code Style

Define naming standards for the entire codebase.

Include:
- Files
- Folders
- Components
- Functions
- Variables
- Constants
- Types
- Interfaces
- Database entities
- API endpoints
- Hooks
- Services
- Event identifiers
- Environment variables
- CSS/design tokens
- Test files

Naming must be:
- Predictable
- Consistent
- Descriptive
- Domain-oriented
- Free of unnecessary abbreviations

The same business concept must use the same terminology throughout the codebase and documentation.


SECTION 4 — Type Safety & Data Contracts

Define type-safety rules.

Include:
- TypeScript/type checking where applicable
- Strict type checking
- API request types
- API response types
- Database-generated types
- Form types
- Validation schemas
- Enum handling
- Nullable values
- Date/time types
- File metadata types
- Gamification transaction types
- Shared domain types
- Avoiding unsafe `any`
- Runtime validation at trust boundaries

Database, API, and frontend types must remain synchronized.


SECTION 5 — Separation of Concerns & Application Architecture

Define architectural boundaries.

Include:
- UI layer
- Presentation logic
- Application/service layer
- Business logic
- Data-access layer
- Database layer
- External integration layer
- Validation layer
- Configuration layer

Rules:
- UI components must not contain large business workflows.
- Database queries must not be scattered arbitrarily throughout UI components.
- Gamification rules must not be duplicated in UI code.
- External integrations must not be tightly coupled to presentation components.
- Business logic must have a clear authoritative location.
- Shared utilities must remain generic and not become hidden business-rule containers.


SECTION 6 — Component Development Rules

Define frontend component standards.

Include:
- Reusable components
- Single responsibility
- Component composition
- Props design
- State ownership
- Controlled/uncontrolled inputs where appropriate
- Accessibility requirements
- Loading states
- Error states
- Empty states
- Responsive behavior
- Avoiding oversized components
- Avoiding duplicated components
- Feature-specific vs shared components
- Journal component standards
- Gamification component standards

Components must remain consistent with UI_GUIDE.md.


SECTION 7 — State, Data Fetching & Server Interaction Rules

Define how frontend state and server data must be handled.

Include:
- Local UI state
- Server state
- Authentication state
- Group context
- Journal state
- Form state
- Cache invalidation
- Refetching
- Optimistic updates
- Rollback
- Loading states
- Error states
- Retry behavior
- Avoiding stale data
- Avoiding duplicated server state
- Avoiding unnecessary global state
- Avoiding N+1 requests

The frontend must treat the database/API as authoritative for persistent data.


SECTION 8 — Database Development Rules

Define rules for all database changes.

Include:
- PostgreSQL
- Supabase
- Migration-based development
- Foreign keys
- Constraints
- Indexes
- Transactions
- Functions
- Triggers
- RLS
- Naming conventions
- Schema changes
- Seed data
- Historical data preservation
- No manual undocumented production schema changes
- Migration testing
- Rollback/recovery considerations
- Database source-of-truth principle

Every database change must remain compatible with DATABASE.md.


SECTION 9 — API & Backend Development Rules

Define backend/API development standards.

Include:
- API_SPECIFICATION.md compliance
- Request validation
- Response consistency
- Authentication
- Authorization
- RLS
- Error handling
- Status codes
- Idempotency
- Transaction handling
- Pagination
- Filtering
- Sorting
- Rate considerations where appropriate
- Logging
- External API handling
- Server-side secrets
- RPC/functions where appropriate

Backend code must not bypass database security or silently change business rules.


SECTION 10 — Gamification Development Rules

Define implementation rules for gamification.

Include:
- GAMIFICATION.md as the business-rule authority
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
- Idempotency
- Duplicate prevention
- Reversal transactions
- Corrections
- Historical preservation
- Deterministic calculations
- Transaction atomicity

Critical rule:
Never implement a new gamification rule directly in UI code without updating the authoritative business-rule definition first.


SECTION 11 — Dynamic Journal Core Development Rules

Define special rules for the Dynamic Journal Core.

Include:
- Performance-first implementation
- Group context
- Date/lesson context
- Student row rendering
- Attendance actions
- Homework actions
- Inline updates
- Optimistic UI only where safe
- Transaction confirmation
- Rollback
- Duplicate prevention
- Debouncing where appropriate
- Minimal re-rendering
- Efficient data fetching
- Pagination/virtualization where required
- Mobile behavior
- Offline/network failure handling where supported
- Error recovery
- Journal consistency with gamification

The Journal must remain responsive during real classroom workflows.


SECTION 12 — Forms, Validation & Error Handling

Define form and error-handling standards.

Include:
- Client validation
- Server validation
- Database validation
- Required fields
- Field-level errors
- Form-level errors
- Business-rule errors
- Network errors
- Authentication errors
- Permission errors
- File errors
- Retry behavior
- User-friendly error messages
- Safe technical error logging
- Confirmation dialogs
- Destructive-action protection

Errors must be handled explicitly rather than silently ignored.


SECTION 13 — Security & Privacy Development Rules

Define secure coding requirements.

Include:
- Least privilege
- RLS
- Authentication
- Authorization
- Secure server-side operations
- Secret management
- No credentials in source code
- No service-role credentials in the browser
- Input validation
- Output safety
- File security
- Safe error messages
- Data minimization
- Teacher data isolation
- Audit logging
- Dependency security
- Production access restrictions
- No frontend-only authorization assumptions

Security requirements must remain consistent with DATABASE.md and API_SPECIFICATION.md.


SECTION 14 — Performance & Resource Management Rules

Define coding practices required for performance.

Include:
- Efficient queries
- Appropriate indexes
- Pagination
- Lazy loading
- Code splitting
- Debounced search
- Avoiding unnecessary requests
- Avoiding N+1 queries
- Avoiding unnecessary re-renders
- Efficient state updates
- Journal optimization
- Ranking optimization
- Analytics optimization
- File/image optimization
- Bundle-size awareness
- Memory-conscious implementation
- Performance measurement before complex optimization

Do not introduce caching or infrastructure solely because it appears technically sophisticated.


SECTION 15 — Testing & Quality Assurance Rules

Define the required testing strategy.

Include:
- Unit tests
- Integration tests
- Component tests
- API tests
- Database tests
- RLS tests
- Gamification tests
- Journal workflow tests
- Authentication tests
- File/storage tests
- External integration tests
- End-to-end tests
- Regression tests
- Test data
- Edge cases
- Error cases
- Security cases
- Realistic teacher workflows

Critical business rules must be covered by automated tests.


SECTION 16 — Git, Branching, Commits & Code Review

Define version-control rules.

Include:
- Git as the source-control system
- Branch naming
- Feature branches
- Bug-fix branches
- Documentation changes
- Commit naming
- Small logical commits
- Pull requests
- Code review
- Merge policy
- Conflict resolution
- Migration review
- No secrets in commits
- No generated build artifacts unless explicitly required
- Reverting unsafe changes
- Keeping history understandable

Database migrations and business-rule changes require additional review because they can affect historical data.


SECTION 17 — Environment Configuration & Secrets

Define development/staging/production configuration rules.

Include:
- Environment variables
- `.env.example`
- Local development configuration
- Test configuration
- Production configuration
- Public vs private variables
- Supabase configuration
- Telegram credentials
- Service-role credentials
- Storage credentials
- Secret rotation
- No secrets in Git
- No secrets in frontend bundles
- Configuration validation
- Missing-variable behavior

The application must fail safely when required configuration is missing.


SECTION 18 — Dependencies, Libraries & AI Coding Rules

Define dependency and AI-agent development rules.

Dependency rules:
- Every dependency must have a clear purpose.
- Prefer existing project dependencies when sufficient.
- Avoid duplicate libraries.
- Prefer stable and maintained packages.
- Remove unused dependencies.
- Monitor security vulnerabilities.
- Avoid unnecessary large packages.
- Avoid libraries that duplicate native/browser/platform capabilities without a clear benefit.

AI coding-agent rules:
- Read relevant project documentation before modifying code.
- Follow existing architecture.
- Do not invent requirements.
- Do not silently change technology choices.
- Do not rewrite working systems unnecessarily.
- Do not bypass RLS/security.
- Do not hardcode production data.
- Do not create undocumented business rules.
- Do not introduce infrastructure without justification.
- Explain significant architectural changes.
- Update documentation when an approved architectural rule changes.
- Preserve backward compatibility where practical.
- Prefer small, reviewable changes.


SECTION 19 — Documentation, Change Management & Cross-Document Consistency

Define how implementation changes affect project documentation.

Include:
- Documentation ownership
- Requirement changes
- Architecture changes
- Database changes
- API changes
- UI changes
- Gamification changes
- Technology changes
- Migration documentation
- Changelog requirements
- Decision records where necessary
- Versioning
- Deprecation
- Cross-document review

Authority model:
- PROJECT_REQUIREMENTS.md → product requirements
- DATABASE.md → data/persistence rules
- UI_GUIDE.md → UI behavior
- GAMIFICATION.md → gamification business rules
- API_SPECIFICATION.md → API contracts
- TECH_STACK.md → approved technologies
- DEVELOPMENT_RULES.md → coding/development standards

No implementation change should leave contradictory documentation behind.


SECTION 20 — Final Development Standards, CI/CD Readiness & Acceptance

Define the final standards required before code is considered complete.

Code quality:
- Type checks pass
- Lint checks pass
- Formatting is consistent
- Tests pass
- No critical warnings remain
- No unnecessary dependencies
- No secrets committed
- No unresolved security issues
- No duplicated business rules
- No undocumented production behavior

Architecture:
- UI/business/data layers remain separated
- Database access is controlled
- API contracts are respected
- Gamification rules are authoritative
- Journal performance is acceptable
- RLS is enforced
- Teacher ownership is preserved

CI/CD readiness:
- Automated validation can run in CI
- Tests can run without production data
- Build is reproducible
- Migrations are reproducible
- Environment variables are documented
- Deployment prerequisites are known

Final acceptance criteria:

Development is considered compliant only when:
- Code follows the approved architecture.
- Naming and folder conventions are consistent.
- Type safety is maintained.
- UI and business logic are properly separated.
- Database access follows DATABASE.md.
- API implementation follows API_SPECIFICATION.md.
- Gamification implementation follows GAMIFICATION.md.
- UI implementation follows UI_GUIDE.md.
- Technology choices follow TECH_STACK.md.
- Security controls are enforced.
- RLS requirements are respected.
- Dynamic Journal Core remains performant and reliable.
- Critical workflows are tested.
- Errors are handled explicitly.
- Historical data is preserved.
- Transactions are safe and idempotent where required.
- No unnecessary infrastructure is introduced.
- No undocumented business rules are introduced.
- No project document is silently contradicted.
- The implementation is practical for real teacher workflows.
- The project remains maintainable and scalable for the intended maximum of 40 teachers.

ROADMAP.md — FINAL 20-SECTION IMPLEMENTATION PLAN

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
- PROJECT_REQUIREMENTS.md — product requirements and scope
- DATABASE.md — database architecture, persistence, integrity, and data rules
- UI_GUIDE.md — UI behavior and implementation standards
- GAMIFICATION.md — gamification business rules
- API_SPECIFICATION.md — API contracts
- TECH_STACK.md — approved technology stack
- DEVELOPMENT_RULES.md — coding and development standards
- DEPLOYMENT.md — deployment and operational standards
- ROADMAP.md — implementation order, milestones, phases, dependencies, and delivery criteria

Roadmap principle:
The roadmap must describe a practical, dependency-aware path from project foundation to stable production. Each phase must produce a usable and verifiable result. Do not build features before their required foundations are ready, and do not introduce unnecessary work that does not contribute to the project's defined scope.


SECTION 1 — Roadmap Purpose, Strategy & Completion Model

Define the purpose and methodology of the roadmap.

Include:
- Overall implementation strategy
- Development phases
- Milestones
- Dependencies
- Deliverables
- Verification points
- Definition of done
- Incremental development
- Risk-aware sequencing
- Teacher-first prioritization
- Maximum 40 teacher accounts
- Lightweight architecture
- Production-readiness principle

The roadmap must convert the project documentation into an executable implementation sequence.


SECTION 2 — Project Foundation & Repository Setup

Define the first implementation phase.

Include:
- Repository initialization
- Project structure
- Package manager
- Approved technology stack
- Environment configuration
- `.env.example`
- Git configuration
- Formatting
- Linting
- Type checking
- Basic testing framework
- Development scripts
- Documentation structure
- Local development setup
- Initial CI validation where appropriate

Completion criteria:
A developer or AI coding agent can clone the repository and start the project using documented steps.


SECTION 3 — Architecture Baseline & Shared Infrastructure

Define the foundational application architecture.

Include:
- Frontend architecture
- Routing
- Application shell foundation
- Shared components
- Design tokens
- Configuration layer
- API/data-access layer
- Error-handling foundation
- Authentication boundary
- Database access boundary
- Feature-module structure
- Shared utilities
- Logging foundation
- Type generation/synchronization where applicable

Do not implement feature-specific business logic prematurely.


SECTION 4 — Supabase, PostgreSQL & Database Foundation

Define the database implementation phase.

Include:
- Supabase project setup
- PostgreSQL schema
- Initial migrations
- Teacher table/profile
- Teacher settings
- Core entities
- Foreign keys
- Constraints
- Indexes
- RLS foundation
- Database functions where required
- Seed/configuration data
- Migration workflow
- Database testing

Completion criteria:
The database can safely support the application's core ownership and persistence model.


SECTION 5 — Authentication & Teacher Account Foundation

Define the authentication phase.

Include:
- Supabase Authentication
- Teacher login
- Session handling
- Logout
- Teacher profile
- Teacher settings
- Account status
- Authentication errors
- Unauthorized states
- RLS integration
- Maximum 40 teacher accounts
- No student login
- Security testing

Completion criteria:
A teacher can securely authenticate and access only their own authorized application data.


SECTION 6 — Application Shell, Navigation & Core UI

Define the initial usable application interface.

Include:
- App shell
- Header
- Sidebar
- Main content area
- Navigation
- Mobile navigation
- Breadcrumbs
- Page containers
- Responsive behavior
- Loading states
- Empty states
- Error states
- Shared buttons/forms/tables
- Accessibility foundation
- Group context

Navigation must follow UI_GUIDE.md.


SECTION 7 — Groups & Students

Define the academic structure implementation.

Groups:
- Group creation
- Group editing
- Group archive
- Group details
- Group switching
- Group statistics foundation

Students:
- Add student
- Edit student
- Archive student
- Student profile
- Search
- Filters
- Student history foundation
- Teacher notes foundation where appropriate

Completion criteria:
Teachers can create and manage their groups and students securely.


SECTION 8 — Lessons, Attendance & Journal Foundation

Define the first classroom workflow phase.

Include:
- Lesson creation
- Lesson scheduling/records
- Journal data structure
- Student rows
- Date/lesson context
- Attendance statuses:
  - Present
  - Absent with reason
  - Absent without reason
  - Late
- Attendance history
- Corrections
- Journal loading
- Journal filtering
- Permission states
- Error recovery

The Journal must be designed around real classroom interaction rather than generic CRUD behavior.


SECTION 9 — Dynamic Journal Core Optimization

Treat the Dynamic Journal Core as a dedicated milestone.

Include:
- Fast group loading
- Efficient student rendering
- Inline actions
- Attendance interaction
- Homework interaction hooks
- Point/XP display hooks
- Optimistic UI only where safe
- Transaction confirmation
- Rollback
- Duplicate prevention
- Minimal re-rendering
- Debouncing where appropriate
- Efficient queries
- Large-group behavior
- Mobile behavior
- Network failure recovery
- Performance measurement

Completion criteria:
The Journal is reliable and fast enough for real-time teacher classroom usage before additional complex features are layered onto it.


SECTION 10 — Homework Management

Define the homework implementation phase.

Include:
- Homework creation
- Homework assignment
- Sequential homework upload
- Homework statuses
- Evaluation
- Completed
- Perfect
- Homework history
- File upload/storage
- Search
- Filters
- Corrections
- Error handling
- Journal integration

Gamification effects must be implemented according to GAMIFICATION.md rather than independently inside the homework UI.


SECTION 11 — Payments & Financial Records

Define the financial module.

Include:
- Payment entry
- Payment history
- Payment status
- Due indicators
- Search
- Filters
- Monthly summaries
- Corrections
- Historical preservation
- Group/student financial views
- Security
- Journal/dashboard integration where required

Payment data must remain independent from gamification unless an explicit project rule connects them.


SECTION 12 — Gamification Engine & Transaction System

Define the core gamification implementation phase.

Include:
- Point transactions
- XP transactions
- Gamification events
- Rule configuration
- Idempotency
- Duplicate prevention
- Reversal/correction transactions
- Attendance effects
- Homework effects
- Manual adjustments if approved
- Transaction atomicity
- Historical preservation
- Auditability

Completion criteria:
All authoritative gamification transactions are deterministic, traceable, and reproducible.


SECTION 13 — Levels, Monthly Cycle, Rankings, Badges, Achievements & Streaks

Define the advanced gamification phase.

Include:
- XP thresholds
- Levels
- Monthly levels
- Monthly cycle
- Monthly rankings
- Current rankings
- Tie-breaking
- Badges
- Badge eligibility
- Achievements
- Achievement progress
- Streaks
- Historical gamification records
- Recalculation
- Late corrections
- Time-zone handling
- Group leaderboard

All rules must come from GAMIFICATION.md.


SECTION 14 — Rewards, Certificates & Recognition

Define recognition-related features.

Include:
- Rewards
- Reward eligibility
- Reward history
- Redemption status if applicable
- Certificates
- Certificate templates
- Certificate generation
- Certificate history
- File storage
- Teacher-facing recognition UI
- Historical records
- Correction behavior

Do not introduce financial/external obligations not defined in the project requirements.


SECTION 15 — Dashboard, Analytics & Statistics

Define the reporting and analytics phase.

Dashboard:
- Today's lessons
- Groups overview
- Attendance summary
- Homework summary
- Gamification summary
- Recent activity
- Notifications
- Quick actions

Analytics:
- Group statistics
- Student statistics
- Attendance analytics
- Homework analytics
- Payment analytics
- Points
- XP
- Levels
- Rankings
- Monthly statistics
- Trends
- Date filtering
- Charts
- Performance indicators

Analytics must be derived from authoritative database data.


SECTION 16 — Reports, Exports, Telegram & External Integrations

Define external output workflows.

Include:
- Reports
- Report generation
- Export
- Import where approved
- Telegram reporting
- Telegram configuration
- Server-side credentials
- Delivery status
- Retry behavior
- Failure handling
- File references
- External integration logging
- Idempotency where required

External systems must never become the application's source of truth.


SECTION 17 — Security, Accessibility, Performance & Reliability Hardening

Define the cross-cutting hardening phase.

Security:
- RLS verification
- Teacher isolation
- Authorization
- Secret protection
- File security
- Secure errors
- Dependency review

Accessibility:
- Keyboard navigation
- Focus management
- Semantic HTML
- Screen-reader support
- Contrast
- Labels

Performance:
- Query optimization
- Index verification
- Pagination
- Lazy loading
- Code splitting
- Journal optimization
- Ranking optimization
- Analytics optimization
- Avoid N+1 queries
- Avoid unnecessary API calls

Reliability:
- Network failures
- Retry behavior
- Transaction failures
- Error boundaries
- Recovery workflows


SECTION 18 — Testing, QA & Realistic Teacher Workflows

Define the full verification phase.

Include:
- Unit tests
- Integration tests
- Component tests
- API tests
- Database tests
- RLS tests
- Gamification tests
- Journal tests
- Authentication tests
- Storage tests
- Telegram tests
- End-to-end tests
- Regression tests
- Mobile/responsive tests
- Accessibility tests
- Performance tests
- Security tests

Realistic workflows must include:
- Teacher login
- Group creation
- Student creation
- Lesson creation
- Attendance marking
- Homework evaluation
- Payment recording
- Gamification updates
- Monthly ranking
- Certificate generation
- Report/export
- Telegram reporting

Critical business rules must be tested independently of the UI.


SECTION 19 — Production Deployment, Monitoring & Operational Readiness

Define the transition from completed development to production.

Include:
- Production environment
- Deployment configuration
- Database migrations
- Environment variables
- Secrets
- Hosting
- Supabase
- Storage
- Edge Functions
- Telegram
- HTTPS
- Monitoring
- Logging
- Backups
- Restore procedure
- Rollback
- Incident response
- Production verification
- Post-deployment smoke tests

All deployment steps must follow DEPLOYMENT.md.


SECTION 20 — Launch, Post-Launch, Governance & Final Acceptance

Define the final project lifecycle.

Launch:
- Final acceptance review
- Production release
- Smoke testing
- Teacher workflow verification
- Security verification
- Performance verification
- Backup verification
- Monitoring verification

Post-launch:
- Bug monitoring
- Performance monitoring
- Teacher feedback
- Controlled improvements
- Documentation updates
- Changelog updates
- Dependency/security maintenance
- Capacity monitoring
- Database maintenance

Governance:
- No undocumented business rules
- No silent architecture changes
- No conflicting project documents
- Changes must follow DEVELOPMENT_RULES.md
- Database changes follow DATABASE.md
- UI changes follow UI_GUIDE.md
- Gamification changes follow GAMIFICATION.md
- API changes follow API_SPECIFICATION.md
- Technology changes follow TECH_STACK.md
- Deployment changes follow DEPLOYMENT.md
- Product scope remains governed by PROJECT_REQUIREMENTS.md

Final acceptance criteria:

The roadmap is complete only when:
- All required project foundations are implemented.
- Teacher authentication works securely.
- Maximum 40 teacher accounts is respected.
- Groups and students work correctly.
- Lessons and Dynamic Journal Core work reliably.
- Attendance works correctly.
- Homework works correctly.
- Payments work correctly.
- Points and XP are deterministic.
- Levels and monthly cycles are correct.
- Rankings are deterministic.
- Badges and achievements work correctly.
- Streaks work correctly.
- Rewards and certificates work correctly.
- Analytics are reproducible.
- Reports and exports work.
- Telegram integration works where configured.
- RLS prevents unauthorized teacher access.
- Critical workflows are tested.
- Performance is acceptable.
- Accessibility requirements are satisfied.
- Production deployment is reproducible.
- Backups and recovery are defined.
- Monitoring is operational.
- Documentation is consistent.
- No unnecessary infrastructure has been introduced.
- The system is practical for real classroom use.
- The implementation remains maintainable and scalable for the intended project size.

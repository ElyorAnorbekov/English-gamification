API_SPECIFICATION.md — FINAL 20-SECTION IMPLEMENTATION PLAN

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
- API behavior must remain consistent with PROJECT_REQUIREMENTS.md, DATABASE.md, UI_GUIDE.md, and GAMIFICATION.md

API authority:
- PROJECT_REQUIREMENTS.md defines product requirements.
- DATABASE.md defines persistence, entities, relationships, constraints, and database security requirements.
- GAMIFICATION.md defines gamification business rules.
- UI_GUIDE.md defines UI behavior and presentation requirements.
- API_SPECIFICATION.md defines communication contracts, request/response behavior, validation, errors, authorization boundaries, and integration behavior.
- Each document is authoritative within its own domain.
- No document may silently contradict another document.
- If a required business rule is not explicitly defined, the implementation must not invent a conflicting rule.


SECTION 1 — API Architecture & Core Principles

Define the overall API architecture and purpose.

Include:
- API purpose
- Frontend-to-backend communication model
- Supabase/PostgreSQL integration
- Direct database access vs server-side functions
- REST/RPC patterns where applicable
- External integration boundaries
- Teacher-first architecture
- Maximum 40 teachers
- Lightweight architecture
- Source-of-truth principle
- Separation of UI, API, business logic, and persistence
- No unnecessary microservices
- Completion criteria


SECTION 2 — API Layers & Request Flow

Define the complete request lifecycle.

Include:
- Client request
- Authentication
- Authorization
- Input validation
- Business-rule evaluation
- Database operation
- Transaction handling
- External service interaction
- Response generation
- Error handling
- Logging
- Audit/activity recording

Define the preferred flow:

Client
↓
Authentication
↓
Authorization / RLS
↓
Validation
↓
Business Logic
↓
Database Transaction
↓
External Integration if required
↓
Response
↓
UI


SECTION 3 — Authentication, Sessions & Teacher Identity

Define API authentication behavior.

Include:
- Supabase Authentication
- Authenticated user ID
- Teacher profile mapping
- Session validation
- Session expiration
- Login state
- Logout
- Unauthorized requests
- Authentication failures
- Teacher account status
- Suspended/archived teacher behavior
- No student login
- Identity consistency with DATABASE.md

The API must never trust a teacher ID supplied by the client when the authenticated identity is available from the secure session.


SECTION 4 — Authorization, Ownership & RLS Integration

Define API authorization boundaries.

Include:
- Teacher ownership
- Group ownership
- Student ownership through groups
- Teacher-specific records
- Group-level access
- Cross-teacher isolation
- Supabase Row Level Security
- Permission-aware requests
- Authorization failures
- Backend/service-role boundaries
- No frontend-only authorization
- No client-controlled ownership escalation

The API must remain compatible with DATABASE.md RLS policies.


SECTION 5 — API Conventions & Contract Standards

Define common API conventions.

Include:
- Endpoint naming
- HTTP methods where applicable
- RPC/function naming
- Request format
- Response format
- JSON conventions
- UUID handling
- Timestamp format
- Time-zone handling
- Pagination format
- Sorting
- Filtering
- Search parameters
- Idempotency keys
- Correlation/request IDs where useful
- Consistent success responses
- Consistent error responses

Use predictable conventions throughout the system.


SECTION 6 — Validation & Data Integrity

Define request validation.

Include:
- Required fields
- Type validation
- Format validation
- Range validation
- Enum validation
- UUID validation
- Date/time validation
- Teacher ownership validation
- Group ownership validation
- Student relationship validation
- Duplicate detection
- Business-rule validation
- Database constraint handling
- Sanitization where applicable

Critical rule:
Client-side validation improves UX but must never replace server/database validation.


SECTION 7 — Error Handling & Recovery

Define the complete API error model.

Include:
- Authentication errors
- Authorization errors
- Validation errors
- Not-found errors
- Conflict errors
- Duplicate request errors
- Database errors
- Transaction errors
- External-service errors
- File/storage errors
- Rate/usage errors if applicable
- Unexpected errors
- Safe error messages
- Retry behavior
- Rollback behavior
- User-facing vs internal error details

Errors must never expose secrets, credentials, SQL internals, or unnecessary sensitive information.


SECTION 8 — Teacher, Group & Student APIs

Define CRUD and retrieval contracts for core academic entities.

Teacher:
- Profile
- Settings
- Language
- Account status

Groups:
- List
- Create
- Read
- Update
- Archive
- Group statistics

Students:
- List
- Search
- Filter
- Create
- Read
- Update
- Archive
- Student history

Include:
- Ownership checks
- Pagination
- Filtering
- Sorting
- Empty results
- Validation
- Error handling
- Historical preservation

No student-facing authentication or API access is required.


SECTION 9 — Lessons, Journal & Attendance APIs

Define the API contract for the Dynamic Journal Core.

Include:
- Lesson creation
- Lesson retrieval
- Lesson update
- Date selection
- Group selection
- Journal retrieval
- Student rows
- Attendance status
- Present
- Absent with reason
- Absent without reason
- Late
- Attendance correction
- Bulk operations where appropriate
- Inline updates
- Fast journal loading
- Journal filtering
- Pagination/virtualization support where appropriate
- Atomic attendance + gamification processing
- Idempotency
- Error rollback

The Journal API must be optimized for rapid classroom interaction.


SECTION 10 — Homework APIs

Define the complete homework API contract.

Include:
- Homework creation
- Assignment
- Homework list
- Sequential upload workflow
- Homework status
- Assigned
- Completed
- Perfect
- Evaluation
- Re-evaluation
- File upload/reference
- Homework history
- Search
- Filters
- Point/XP processing
- Correction/reversal
- Duplicate prevention
- Idempotency
- Error handling

Gamification effects must be delegated to GAMIFICATION.md rules.


SECTION 11 — Payments & Financial APIs

Define teacher-facing payment APIs.

Include:
- Payment creation
- Payment update
- Payment history
- Payment status
- Due information
- Search
- Filters
- Monthly summaries
- Corrections
- Historical records
- Validation
- Ownership
- Error handling

Payment data must remain independent from gamification unless explicitly defined by approved business rules.


SECTION 12 — Gamification APIs

Define APIs for the gamification system.

Include:
- Point transactions
- Current points
- XP transactions
- Current XP
- Levels
- Monthly levels
- Rankings
- Badges
- Achievements
- Achievement progress
- Streaks
- Rewards
- Gamification events
- Gamification history

Critical rule:
API implementation must execute the business rules defined in GAMIFICATION.md and must not invent or duplicate conflicting rules.


SECTION 13 — Gamification Transactions, Idempotency & Atomicity

Define transaction behavior for gamification-triggering actions.

Include:
- Event identifiers
- Idempotency keys
- Duplicate request protection
- Atomic transactions
- Point transaction creation
- XP transaction creation
- Achievement evaluation
- Badge evaluation
- Streak evaluation
- Reversal transactions
- Correction handling
- Source event references
- Historical preservation
- Failed transaction rollback
- Concurrent request handling

Example:

Teacher action
↓
Business event
↓
Gamification rule evaluation
↓
Point/XP transactions
↓
Achievement/Badge/Streak evaluation
↓
Activity log
↓
Atomic commit


SECTION 14 — Analytics, Statistics & Reporting APIs

Define APIs for teacher-facing analytics.

Include:
- Dashboard statistics
- Group statistics
- Student statistics
- Attendance statistics
- Homework statistics
- Payment statistics
- Points statistics
- XP statistics
- Level statistics
- Ranking statistics
- Badge statistics
- Achievement statistics
- Streak statistics
- Monthly statistics
- Trends
- Date-range filters
- Aggregation
- Pagination where required

Analytics must be derived from authoritative data and remain consistent with DATABASE.md.


SECTION 15 — Reports, Certificates, Exports & File APIs

Define output and file-related APIs.

Include:
- Report generation
- Report retrieval
- Certificate generation
- Certificate history
- Certificate templates
- Export generation
- Export history
- File upload
- File references
- Storage paths
- File access authorization
- Temporary files
- Retry behavior
- Generation status
- Failure handling

Database records should store file metadata/references rather than unnecessary binary data.


SECTION 16 — Telegram & External Integration APIs

Define external integration boundaries.

Include:
- Telegram reporting
- Group-level statistics reporting
- Message generation
- Message delivery
- Delivery status
- Retry behavior
- Failure handling
- External API credentials
- Server-side secret handling
- Integration logging
- Idempotency where necessary
- Rate/usage considerations
- External service unavailability

Critical rule:
Telegram is an output/integration channel and is never the database source of truth.


SECTION 17 — Activity Logs, Audit Logs & Notifications APIs

Define APIs for historical activity and notifications.

Include:
- Activity events
- Audit events
- Teacher actions
- Gamification events
- Security-sensitive events
- Notification creation
- Notification retrieval
- Read/unread state
- Notification history
- Filtering
- Pagination
- Ownership
- Historical preservation

Activity logs and audit logs must remain conceptually distinct where required by DATABASE.md.


SECTION 18 — Performance, Caching & Scalability

Define API performance requirements.

Include:
- Fast response times
- Minimal payloads
- Pagination
- Filtering at database/API level
- Debouncing for search where appropriate
- Avoiding N+1 queries
- Efficient journal queries
- Efficient ranking queries
- Efficient analytics queries
- Avoiding unnecessary API calls
- Caching only derived/non-authoritative data where appropriate
- Cache invalidation
- Lazy loading
- Lightweight dependencies
- Connection/resource efficiency
- Concurrent request handling

Performance optimizations must never bypass security or source-of-truth requirements.


SECTION 19 — Security, Secrets, Rate Protection & Observability

Define API security standards.

Include:
- Least privilege
- RLS compatibility
- Service-role key protection
- Environment variables
- No secrets in frontend code
- No secrets in Git
- Secure external API credentials
- Input validation
- Output sanitization where applicable
- File access security
- Secure error handling
- Request logging
- Correlation IDs where useful
- Security event logging
- Rate protection where appropriate
- Abuse prevention
- Monitoring
- Alerting
- Sensitive-data minimization

Frontend code must never receive credentials that provide unauthorized database access.


SECTION 20 — Testing, Documentation, Governance & Final Acceptance

Define final API implementation standards.

Testing:
- Authentication tests
- Authorization tests
- Cross-teacher isolation tests
- RLS tests
- CRUD tests
- Validation tests
- Error-handling tests
- Journal workflow tests
- Attendance tests
- Homework tests
- Payment tests
- Point calculation tests
- XP calculation tests
- Level tests
- Monthly cycle tests
- Ranking/tie tests
- Badge tests
- Achievement tests
- Streak tests
- Reward tests
- Idempotency tests
- Concurrent transaction tests
- File/storage tests
- Telegram integration tests
- Analytics tests
- Realistic teacher workflow tests
- Time-zone/date-boundary tests

Documentation:
- Every endpoint/function must have a defined purpose.
- Request and response schemas must be documented.
- Authentication requirements must be documented.
- Authorization requirements must be documented.
- Error behavior must be documented.
- Side effects must be documented.
- Idempotency requirements must be documented.
- External integrations must be documented.
- Breaking changes must be documented.

Governance:
- API contracts must be version-controlled.
- Production API behavior must not depend on undocumented manual changes.
- Business rules remain centralized in GAMIFICATION.md.
- Persistence rules remain centralized in DATABASE.md.
- UI behavior remains centralized in UI_GUIDE.md.
- API_SPECIFICATION.md defines the communication contract.
- No duplicated or conflicting business rules.
- No unnecessary endpoints.
- No unnecessary services.
- No silent breaking changes.

Final acceptance criteria:

The API implementation is complete only when:
- Authentication is secure
- Teacher ownership is enforced
- Cross-teacher access is impossible
- RLS requirements are satisfied
- All major CRUD workflows function correctly
- Dynamic Journal operations are fast and reliable
- Attendance processing is atomic
- Homework processing is reliable
- Payment records are accurate
- Gamification transactions are deterministic
- Duplicate requests are prevented
- Corrections preserve historical data
- Analytics are reproducible
- Reports and certificates work correctly
- File access is secure
- Telegram integration handles failure safely
- Errors are predictable and safe
- Performance is acceptable
- Critical workflows are tested
- Documentation is complete
- API behavior is consistent with PROJECT_REQUIREMENTS.md, DATABASE.md, GAMIFICATION.md, and UI_GUIDE.md
- No implementation invents undefined business rules
- The system remains lightweight and appropriate for the intended project scale

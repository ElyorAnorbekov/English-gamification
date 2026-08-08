# Database Documentation

# Section 1 — Database Overview

---

## 1.1 Purpose

The database is the central data layer of the English Teacher Gamification System.

It shall provide reliable, secure, and structured storage for:

- Teacher accounts
- Groups
- Students
- Lessons
- Journal records
- Attendance
- Homework
- Payments
- Points
- XP
- Levels
- Rankings
- Badges
- Achievements
- Streaks
- Rewards
- Certificates
- Teacher Notes
- Analytics
- Reports
- Notifications
- Activity Logs
- Audit Logs
- Import and Export records

The database shall act as the authoritative source of truth for application data.

---

## 1.2 Database Technology

The primary database technology shall be:

**PostgreSQL**

The preferred managed database platform shall be:

**Supabase**

The database architecture shall remain compatible with standard PostgreSQL principles and SQL syntax wherever practical.

---

## 1.3 Database Philosophy

The database shall follow these principles:

1. Data integrity first.
2. Security at the database level.
3. Historical data preservation.
4. Clear relationships between entities.
5. Minimal duplication of authoritative data.
6. Efficient queries.
7. Simple architecture.
8. Easy maintenance.
9. Version-controlled migrations.
10. Scalability without unnecessary complexity.

---

## 1.4 Database as the Source of Truth

PostgreSQL shall be the authoritative source of application data.

The following shall not replace the database as the source of truth:

- Frontend state
- Browser localStorage
- Browser session data
- Cached analytics
- Telegram messages
- Exported files
- Generated reports

Cached or derived data may be used for performance, but it must always be possible to regenerate it from authoritative database records.

---

## 1.5 Initial Scale

The initial database shall be designed for approximately:

- Up to 20 teachers
- Multiple groups per teacher
- Multiple students per group
- Multiple lessons per group
- Long-term attendance history
- Homework history
- Payment history
- Gamification history
- Analytics history
- Activity history

The architecture shall provide sufficient capacity for this scale without introducing unnecessary enterprise infrastructure.

---

## 1.6 Multi-Tenant Data Model

The application shall use logical teacher-level data isolation.

Each teacher shall own their application data.

The primary ownership relationship shall be:

Teacher
↓
Groups
↓
Students
↓
Academic Records

Teacher-owned data shall include, where applicable:

- Groups
- Students
- Lessons
- Attendance
- Homework
- Payments
- Gamification records
- Certificates
- Analytics
- Reports
- Teacher Notes
- Notifications
- Activity Logs

---

## 1.7 Data Ownership Principle

Every teacher-owned record shall be traceable to the authenticated teacher either:

- Directly through `teacher_id`, or
- Indirectly through a securely validated relationship.

The database shall never rely only on frontend filtering to enforce ownership.

---

## 1.8 Historical Data Principle

Historical records shall be preserved whenever they have analytical, financial, academic, or gamification value.

The following data shall remain historically accessible:

- Attendance
- Homework
- Payments
- Point transactions
- XP transactions
- Levels
- Badges
- Achievements
- Streaks
- Certificates
- Activity Logs

Deleting or archiving an active entity must not unnecessarily destroy its historical records.

---

## 1.9 Derived Data Principle

The system shall distinguish between:

### Authoritative Data

Data directly representing an actual event or user action.

Examples:

- Attendance record
- Payment record
- Homework evaluation
- Point transaction
- XP transaction

### Derived Data

Data calculated from authoritative records.

Examples:

- Current points
- Ranking
- Attendance percentage
- Monthly statistics
- Achievement progress
- Trend indicators

Derived data may be cached or stored for performance, but the authoritative records must remain available.

---

## 1.10 Transactional Integrity

Operations that modify multiple related records shall use database transactions where required.

Example:

Attendance update:

Attendance
↓
Point Transaction
↓
XP Transaction
↓
Achievement Progress
↓
Analytics Update
↓
Activity Log

If a critical multi-step operation fails, the database shall prevent an inconsistent partial state where practical.

---

## 1.11 Security Principle

Database security shall be enforced at the database level.

The application shall use:

- Authentication
- Authorization
- Row Level Security
- Foreign Key Constraints
- Unique Constraints
- Input Validation
- Secure Database Functions

Frontend restrictions shall not be considered a sufficient security mechanism.

---

## 1.12 Performance Principle

The database shall be optimized for the application's most frequently used workflows.

Priority shall be given to:

1. Journal loading
2. Attendance updates
3. Homework updates
4. Student search
5. Dashboard statistics
6. Rankings
7. Analytics

Database queries shall avoid unnecessary data retrieval.

---

## 1.13 Infrastructure Principle

The initial implementation shall use lightweight infrastructure.

Preferred stack:

- PostgreSQL
- Supabase
- Supabase Authentication
- Supabase Storage
- Supabase Row Level Security
- Supabase Edge Functions where server-side logic is required

The system shall not require:

- Microservices
- Kubernetes
- Dedicated database servers
- Redis
- Separate analytics databases
- Message queues

unless future scale creates a genuine technical requirement.

---

## 1.14 Migration-Based Development

All database structure changes shall be implemented through version-controlled migrations.

Examples:

```text
supabase/
└── migrations/
    ├── 001_initial_schema.sql
    ├── 002_rls_policies.sql
    ├── 003_database_functions.sql
    └── ...

# Section 2 — Database Architecture

---

## 2.1 Purpose

This section defines the overall database architecture of the English Teacher Gamification System.

The architecture shall define how the following components interact:

- Frontend Application
- Supabase Authentication
- PostgreSQL Database
- Row Level Security
- Supabase Storage
- Server-side Functions
- External Integrations
- Analytics and Reporting

The architecture shall remain lightweight and appropriate for the initial scale of the application.

---

## 2.2 High-Level Architecture

The primary architecture shall follow:

Teacher
↓
Frontend Application
↓
Authentication
↓
Supabase API / Server Functions
↓
PostgreSQL Database
↓
Storage / External Integrations

The database shall remain the central persistent data layer.

---

## 2.3 Architecture Components

The database architecture shall contain the following primary components.

### 1. Supabase Authentication

Responsible for:

- Teacher authentication
- User sessions
- Identity management
- Authentication state

Authentication credentials shall not be stored directly in application tables.

---

### 2. PostgreSQL Database

Responsible for:

- Application data
- Relationships
- Transactions
- Constraints
- Historical records
- Gamification data
- Analytics source data

PostgreSQL shall be the primary source of truth.

---

### 3. Row Level Security

Responsible for:

- Teacher data isolation
- Authorization at database level
- Protection of teacher-owned records

RLS shall prevent unauthorized access even if a user attempts to manipulate frontend requests.

---

### 4. Supabase Storage

Responsible for storing files such as:

- Certificate templates
- Generated certificates
- Export files
- Temporary import files where required

The database shall store metadata and references to stored files.

---

### 5. Server-side Functions

Server-side functions shall be used when an operation requires:

- Private credentials
- External API communication
- Sensitive business logic
- Telegram integration
- Secure file processing
- Operations that should not run in the browser

Server-side functions may use Supabase Edge Functions.

---

### 6. Frontend Application

The frontend shall communicate with the database through secure APIs and Supabase services.

The frontend shall:

- Display data
- Collect teacher input
- Request data
- Submit changes
- Display analytics
- Display gamification information

The frontend shall not bypass database security.

---

## 2.4 Logical Data Layers

The database shall be logically organized into the following data layers.

### Layer 1 — Identity

Contains:

- Authentication identity
- Teacher profile
- Teacher settings

---

### Layer 2 — Academic Structure

Contains:

- Groups
- Students
- Lessons

---

### Layer 3 — Academic Activity

Contains:

- Attendance
- Homework
- Teacher Notes

---

### Layer 4 — Financial Data

Contains:

- Payments
- Payment History
- Financial Status

---

### Layer 5 — Gamification

Contains:

- Points
- XP
- Levels
- Rankings
- Badges
- Achievements
- Streaks
- Rewards

---

### Layer 6 — Documents

Contains:

- Certificate Templates
- Certificates
- Export Records

---

### Layer 7 — Analytics

Contains:

- Statistics
- Aggregated Data
- Trends
- Report Data

---

### Layer 8 — System Activity

Contains:

- Notifications
- Activity Logs
- Audit Logs
- System Events

---

## 2.5 Core Data Flow

The primary application data flow shall follow:

Teacher
↓
Group
↓
Student
↓
Lesson
↓
Attendance / Homework
↓
Transactions
↓
Gamification
↓
Analytics
↓
Reports

This flow shall maintain traceability from an individual teacher action to the resulting statistical and gamification changes.

---

## 2.6 Example Attendance Data Flow

When a teacher marks a student as Present:

Teacher
↓
Journal
↓
Attendance Record
↓
Point Transaction
↓
XP Transaction
↓
Achievement Evaluation
↓
Analytics Update
↓
Activity Log

The exact gamification effects shall follow the rules defined in `GAMIFICATION.md`.

---

## 2.7 Example Homework Data Flow

When a teacher evaluates homework:

Teacher
↓
Homework Evaluation
↓
Homework Status
↓
Point Transaction
↓
XP Transaction
↓
Achievement Evaluation
↓
Analytics Update
↓
Activity Log

The system shall preserve the original homework event and the resulting transactions.

---

## 2.8 Example Payment Data Flow

When a teacher records a payment:

Teacher
↓
Payment Record
↓
Payment Status
↓
Relevant Statistics
↓
Activity Log

Payment information shall remain independent from gamification unless explicitly configured by the business rules.

---

## 2.9 Example Certificate Data Flow

When a teacher generates a certificate:

Teacher
↓
Certificate Request
↓
Certificate Record
↓
Template
↓
File Generation
↓
Storage
↓
Certificate File Reference
↓
Activity Log

The generated file shall be stored separately from the relational database where appropriate.

---

## 2.10 Authentication Architecture

Authentication shall use Supabase Authentication.

The relationship shall be:

Teacher
↓
Supabase Auth User
↓
Teacher Profile
↓
Teacher-owned Records

The authenticated user's unique identity shall be used to determine database access.

---

## 2.11 Teacher Profile Architecture

Authentication identity and application profile data shall remain logically separate.

Authentication system:

- User ID
- Email
- Authentication state

Application profile:

- Display name
- Language
- Preferences
- Account status
- Application-specific settings

The application shall reference the authenticated user through a stable identifier.

---

## 2.12 Ownership Architecture

Teacher ownership shall be enforced through relationships.

Primary pattern:

```text
teacher
   |
   └── groups
          |
          └── students
                 |
                 ├── attendance
                 ├── homework
                 ├── payments
                 ├── transactions
                 ├── achievements
                 └── certificates

# Section 3 — Core Entities

---

## 3.1 Purpose

This section defines the core database entities of the English Teacher Gamification System.

Each entity represents a major business object or persistent concept within the application.

The purpose of this section is to establish:

- Core entities
- Entity responsibilities
- Ownership
- Primary relationships
- Data boundaries
- Entity dependencies

Detailed table schemas and column definitions shall be specified in Section 4 — Table Definitions.

---

## 3.2 Entity Design Principles

The database shall follow these principles:

1. Each entity shall have a clearly defined responsibility.
2. Entities shall not contain unrelated data.
3. Relationships shall be represented through foreign keys.
4. Historical records shall remain traceable.
5. Teacher ownership shall be enforceable.
6. Authoritative data shall be separated from derived data.
7. Gamification events shall remain traceable.
8. Duplicate authoritative records shall be prevented.
9. Entities shall be designed for PostgreSQL.
10. The schema shall remain simple enough for the initial project scale.

---

# 3.3 Identity Entities

## 3.3.1 Teacher

Represents the application-level profile of an authenticated teacher.

Responsibilities:

- Store teacher profile information.
- Store application preferences.
- Define ownership of teacher-specific data.
- Provide the root ownership relationship for application records.

Primary relationship:

```text
Teacher
├── Groups
├── Students
├── Lessons
├── Payments
├── Certificates
├── Reports
├── Activity Logs
└── Settings

# Section 4 — Table Definitions

---

## 4.1 Purpose

This section defines the physical PostgreSQL tables required by the English Teacher Gamification System.

Each table shall have:

- A clearly defined responsibility
- A primary key
- Appropriate foreign keys
- Required timestamps
- Appropriate constraints
- Appropriate indexes
- Teacher ownership where applicable

The final PostgreSQL implementation shall follow these definitions.

---

# 4.2 Identity Tables

## 4.2.1 `teachers`

Stores the application-level profile of each teacher.

| Column | Type | Required | Description |
|---|---|---:|---|
| id | UUID | Yes | Primary key and reference to authenticated user |
| full_name | TEXT | Yes | Teacher display name |
| email | TEXT | No | Application-level email reference |
| language | TEXT | Yes | Preferred interface language |
| status | TEXT | Yes | Account status |
| created_at | TIMESTAMPTZ | Yes | Creation timestamp |
| updated_at | TIMESTAMPTZ | Yes | Last update timestamp |

Allowed `status` values:

- `active`
- `suspended`
- `archived`

---

## 4.2.2 `teacher_settings`

Stores teacher-specific application preferences.

| Column | Type | Required | Description |
|---|---|---:|---|
| id | UUID | Yes | Primary key |
| teacher_id | UUID | Yes | Teacher owner |
| language | TEXT | Yes | Interface language |
| default_group_id | UUID | No | Default group |
| notification_enabled | BOOLEAN | Yes | Notification preference |
| created_at | TIMESTAMPTZ | Yes | Creation timestamp |
| updated_at | TIMESTAMPTZ | Yes | Last update timestamp |

Constraint:

```text
UNIQUE(teacher_id)

# Section 5 — Relationships & Foreign Keys

---

## 5.1 Purpose

This section defines the relationships between database entities and the foreign key rules used to maintain referential integrity.

The database shall use PostgreSQL foreign keys to ensure that related records cannot reference non-existent entities.

All relationships shall respect teacher ownership and the application's multi-tenant data isolation model.

---

# 5.2 Relationship Principles

The database shall follow these principles:

1. Every child record must reference an existing parent record.
2. Teacher-owned data must be associated with the correct `teacher_id`.
3. Records belonging to a deleted or archived parent must follow the defined deletion policy.
4. Historical records should normally be preserved.
5. Foreign keys shall be indexed where required for query performance.
6. Cross-teacher relationships shall not be permitted.
7. Application logic and database constraints shall work together to enforce ownership.

---

# 5.3 Teacher Relationships

The `teachers` table is the primary ownership entity for teacher-specific data.

### Main relationships

```text
teachers
   ├── teacher_settings
   ├── groups
   ├── students
   ├── lessons
   ├── attendance_records
   ├── homework_assignments
   ├── homework_results
   ├── payments
   ├── point_transactions
   ├── xp_transactions
   ├── certificate_templates
   ├── certificates
   ├── teacher_notes
   ├── activity_logs
   ├── audit_logs
   ├── notifications
   ├── reports
   ├── import_jobs
   ├── export_jobs
   └── stored_files

# Section 6 — Row-Level Security (RLS) & Data Isolation

---

## 6.1 Purpose

This section defines the database-level security model for protecting teacher-owned data.

The system shall ensure that:

- Teachers can access only their own data.
- Teachers cannot access another teacher's groups.
- Teachers cannot access another teacher's students.
- Teachers cannot access another teacher's journal records.
- Teachers cannot access another teacher's gamification data.
- Teachers cannot access another teacher's reports or files.
- Database-level security shall not rely only on frontend restrictions.

Supabase PostgreSQL Row-Level Security (RLS) shall be used as the primary database-level data isolation mechanism.

---

# 6.2 Multi-Tenant Data Model

The application shall use a teacher-based multi-tenant architecture.

Each teacher represents an isolated data owner.

Conceptually:

```text
Teacher A
│
├── Groups
├── Students
├── Lessons
├── Attendance
├── Homework
├── Payments
├── Points
├── XP
├── Badges
├── Achievements
├── Reports
└── Files

Teacher B
│
├── Groups
├── Students
├── Lessons
├── Attendance
├── Homework
├── Payments
├── Points
├── XP
├── Badges
├── Achievements
├── Reports
└── Files

# Section 7 — Indexes & Query Performance

---

## 7.1 Purpose

This section defines the database indexing and query-performance requirements for the English Teacher Gamification System.

The database must remain fast when teachers have:

- Multiple groups
- Hundreds of students
- Large journal histories
- Many attendance records
- Large homework histories
- Extensive point and XP transactions
- Long-term activity logs

Indexes shall be designed around actual application query patterns rather than being added indiscriminately.

---

# 7.2 General Indexing Principles

The database shall follow these rules:

1. Primary keys are automatically indexed.
2. Frequently queried foreign keys should be indexed.
3. Teacher ownership columns should be indexed.
4. Columns frequently used in filtering and sorting should be indexed.
5. Composite indexes should reflect real query patterns.
6. Duplicate or unnecessary indexes shall be avoided.
7. Indexes shall be reviewed using query performance analysis.
8. Large historical tables shall receive particular attention.

Indexes must improve read performance without unnecessarily increasing write overhead.

---

# 7.3 Primary Key Indexes

Every table shall use a primary key.

Example:

```sql
id UUID PRIMARY KEY DEFAULT gen_random_uuid()

# Section 8 — Data Integrity, Constraints & Validation

---

## 8.1 Purpose

This section defines the database constraints and validation rules required to maintain accurate, consistent, and reliable application data.

The database shall prevent invalid states wherever possible.

Data integrity shall be enforced through:

- PostgreSQL constraints
- Foreign keys
- Unique constraints
- NOT NULL constraints
- CHECK constraints
- Backend validation
- Row-Level Security
- Transactional operations

The frontend shall not be considered a sufficient data-integrity layer.

---

# 8.2 Data Integrity Principles

The database shall follow these principles:

1. Invalid data should be rejected as early as possible.
2. Referential integrity shall be enforced through foreign keys.
3. Required fields shall use `NOT NULL`.
4. Enumerated business states shall use controlled values.
5. Duplicate records shall be prevented where uniqueness is required.
6. Historical records shall not be silently overwritten.
7. Related changes shall be performed transactionally.
8. Business-critical calculations shall not depend only on frontend logic.
9. Teacher ownership shall be validated before related records are created.
10. Database constraints shall complement application-level validation.

---

# 8.3 NOT NULL Constraints

Fields that are required for the correct operation of the system shall use:

```sql
NOT NULL

# Section 9 — Database Functions, Triggers & Automation

---

## 9.1 Purpose

This section defines the database functions, triggers, and automated database operations required by the English Teacher Gamification System.

Database automation shall be used for operations that are:

- Consistent
- Deterministic
- Closely related to database integrity
- Required across multiple application entry points
- Safer when executed atomically at the database level

Complex business workflows should remain in the application/backend layer unless there is a clear reason to execute them inside PostgreSQL.

---

# 9.2 Database Automation Principles

The system shall follow these principles:

1. Database functions shall have a clearly defined responsibility.
2. Triggers shall be used selectively.
3. Critical integrity rules shall not depend only on frontend code.
4. Functions must respect Row-Level Security where applicable.
5. Security-sensitive functions shall use carefully controlled privileges.
6. Functions shall not silently modify unrelated data.
7. Recursive trigger behavior must be prevented.
8. Complex workflows should normally remain in the backend.
9. Every automated operation must be documented.
10. Automated operations must be testable.

---

# 9.3 Function Categories

Database functions may be divided into:

```text
1. Utility Functions
2. Validation Functions
3. Timestamp Functions
4. Security Functions
5. Aggregation Functions
6. Gamification Functions
7. Reporting Functions

# Section 10 — Database Security & Row-Level Security (RLS)

---

## 10.1 Purpose

This section defines the database security model for the English Teacher Gamification System.

The database must ensure that:

- Teachers can access only their own data.
- Teachers cannot access another teacher's groups.
- Teachers cannot access another teacher's students.
- Teachers cannot modify records belonging to another teacher.
- Students have no direct application login.
- Sensitive database operations are protected.
- Backend services cannot accidentally bypass ownership rules.
- Historical and transactional data remains protected.

Security shall be enforced at the database level in addition to application-level authorization.

---

# 10.2 Security Architecture

The recommended security model is:

```text
User
  ↓
Authentication
  ↓
Authenticated User ID
  ↓
Row-Level Security
  ↓
Teacher Ownership
  ↓
Allowed Records

# Section 11 — Database Seed Data & Initial Configuration

---

## 11.1 Purpose

This section defines the initial data and configuration required for the English Teacher Gamification System to operate correctly after database deployment.

Seed data must contain only system-level or predefined configuration data.

User-generated production data must never be included in the default seed process.

---

# 11.2 Seed Data Principles

The seed system shall follow these principles:

1. Seed data must be deterministic.
2. Seed operations must be repeatable.
3. Seed operations must not create duplicate records.
4. Production user data must not be overwritten.
5. System configuration must have stable identifiers.
6. Seed data must be version-controlled.
7. Development seed data must be separated from production seed data.
8. Sensitive credentials must never be included in seed files.

---

# 11.3 Seed Data Categories

The initial database may contain seed data for:

```text
1. Gamification configuration
2. Point rules
3. XP rules
4. Level thresholds
5. Badge definitions
6. Achievement definitions
7. Homework status definitions
8. Attendance status definitions
9. Payment status definitions
10. System configuration

# Section 12 — Database Migrations & Version Control

---

## 12.1 Purpose

This section defines how database schema changes, functions, triggers, indexes, constraints, RLS policies, and seed configuration are created, versioned, tested, and deployed.

Every database structure change must be reproducible from the repository.

The production database must never depend on undocumented manual changes.

---

# 12.2 Migration Principles

Database migrations shall follow these principles:

1. Every schema change must be version-controlled.
2. Migrations must be executed in a deterministic order.
3. Migrations must be reproducible.
4. Production changes must use migrations.
5. Manual production schema changes are prohibited unless explicitly authorized.
6. Destructive migrations require additional review.
7. Migrations must be tested before production deployment.
8. Migration files must not contain secrets.
9. Applied migrations must not be silently modified.
10. The database schema must remain synchronized with the application code.

---

# 12.3 Migration Directory

Database migrations should be stored in a dedicated directory.

Recommended structure:

```text
database/
└── migrations/
    ├── 001_initial_schema.sql
    ├── 002_core_relationships.sql
    ├── 003_gamification.sql
    ├── 004_journal.sql
    ├── 005_indexes.sql
    ├── 006_integrity_constraints.sql
    ├── 007_functions.sql
    ├── 008_rls.sql
    └── ...

# Section 13 — Backup, Recovery & Disaster Recovery

---

## 13.1 Purpose

This section defines the backup, recovery, restoration, and disaster recovery requirements for the database.

The system must be able to recover from:

- Database failure
- Accidental data deletion
- Application errors
- Failed migrations
- Infrastructure failure
- Storage failure
- Security incidents
- Deployment failures

The recovery strategy must protect both system configuration and teacher-generated data.

---

# 13.2 Backup Principles

Database backups shall follow these principles:

1. Backups must be automated where possible.
2. Production data must be backed up independently of the application server.
3. Backups must be protected from unauthorized access.
4. Backup retention must be defined.
5. Backups must be periodically tested.
6. Recovery procedures must be documented.
7. Backup credentials must never be stored in source code.
8. Critical backups should not depend on the same infrastructure as the primary database.
9. Backup failures must be detectable.
10. The recovery process must be tested before it is needed in production.

---

# 13.3 Backup Scope

Backups should protect:

```text
Database schema
Database records
System configuration
Gamification configuration
Teacher data
Group data
Student data
Attendance
Homework
Payments
Points
XP
Levels
Badges
Achievements
Notes
Activity records


****

# Section 14 — Data Archiving & Long-Term Storage

---

## 14.1 Purpose

This section defines how historical, inactive, or obsolete data is archived and retained without unnecessarily affecting the performance of the active database.

The archive strategy must preserve important historical information while keeping the operational database lightweight and efficient.

---

# 14.2 Archiving Principles

Data archiving shall follow these principles:

1. Historical data must not be deleted merely to improve performance.
2. Archived data must remain recoverable when required.
3. Archiving must preserve data integrity.
4. Archived records must retain their historical meaning.
5. Active application workflows must not depend unnecessarily on archived data.
6. Archiving must not bypass RLS or other security requirements.
7. Archiving operations must be documented and auditable.
8. Archiving must not modify historical business results.
9. User data must not be archived solely because it is old without an appropriate retention policy.
10. Permanent deletion must be treated separately from archiving.

---

# 14.3 Active vs Archived Data

The system should distinguish between:

```text
Active Data
    ↓
Frequently accessed operational data

Archived Data
    ↓
Historical data retained for reference

# Section 15 — Database Monitoring & Observability

---

## 15.1 Purpose

This section defines the monitoring, logging, metrics, alerting, and observability requirements for the production database.

The purpose is to detect:

- Database availability problems
- Slow queries
- Excessive resource usage
- Failed migrations
- Backup failures
- Connection problems
- Storage growth
- Locking and blocking
- Unexpected database errors
- Security-related anomalies

The monitoring system must provide enough information to identify and diagnose database problems without exposing sensitive user data.

---

# 15.2 Monitoring Principles

Database monitoring shall follow these principles:

1. Production database health must be continuously observable.
2. Critical failures must generate alerts.
3. Monitoring must not expose sensitive data.
4. Logs must contain sufficient diagnostic information.
5. Monitoring must have minimal performance overhead.
6. Database metrics must be retained for an appropriate period.
7. Alerts must distinguish critical problems from informational events.
8. Monitoring configuration must be version-controlled where practical.
9. Database monitoring must cover both infrastructure and application-level behavior.
10. Monitoring must support incident investigation.

---

# 15.3 Availability Monitoring

The system should monitor database availability.

At minimum, detect:

```text
Database reachable
Database unavailable
Connection refused
Connection timeout
Authentication failure
Repeated connection failure

# Section 16 — Database Security & Access Control

---

## 16.1 Purpose

This section defines the database security, authentication, authorization, access control, row-level security, credential management, and data protection requirements.

The database must ensure that:

- Teachers can access only authorized data.
- Application services have only required permissions.
- Sensitive credentials are protected.
- Database operations are auditable where required.
- RLS policies prevent cross-teacher data access.
- Production database access is restricted.
- Security controls are applied consistently across active and archived data.

---

# 16.2 Security Principles

Database security shall follow these principles:

1. Least privilege.
2. Defense in depth.
3. Explicit authorization.
4. Default deny where appropriate.
5. No credentials in source code.
6. RLS for tenant/data isolation.
7. Production access must be restricted.
8. Sensitive data must be minimized.
9. Administrative operations must be auditable.
10. Security configuration must be version-controlled where practical.

---

# 16.3 Authentication vs Authorization

Authentication determines:

```text
"Who is this user?"

# Section 17 — Database Performance & Optimization

---

## 17.1 Purpose

This section defines the database performance, query optimization, indexing, pagination, caching, transaction, and scalability requirements.

The database must remain responsive as the number of:

- Teachers
- Groups
- Students
- Lessons
- Attendance records
- Homework records
- Gamification records
- Activity logs

increases over time.

The initial architecture should remain lightweight and should not introduce unnecessary infrastructure complexity.

---

# 17.2 Performance Principles

Database performance shall follow these principles:

1. Queries must retrieve only required data.
2. Appropriate indexes must be used.
3. Large datasets must not be loaded unnecessarily.
4. Pagination must be used for potentially large result sets.
5. N+1 query patterns must be avoided.
6. Expensive calculations should not be repeated unnecessarily.
7. Transactions should remain as short as practical.
8. Database-side filtering should be preferred over loading unnecessary records into the application.
9. Performance optimizations must not bypass security controls.
10. Premature optimization should be avoided.
11. Performance decisions must be based on measurable workload.
12. The simplest architecture that satisfies the performance requirement should be preferred.

---

# 17.3 Performance Targets

The application should establish practical database performance targets.

Initial target:

```text
Normal CRUD operation
    ↓
Fast response under normal workload

Common journal query
    ↓
Target ≤ 500 ms database-side execution

Simple lookup
    ↓
Target ≤ 100 ms database-side execution






















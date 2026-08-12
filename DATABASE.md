DATABASE.md — FINAL DATABASE DOCUMENTATION PROMPT
English Teacher Gamification System
Version: 1.0
Status: Implementation Specification

IMPORTANT IMPLEMENTATION RULE:
This document is the authoritative database specification for the project.
The implementation must follow this document exactly.
Do not invent missing tables, fields, relationships, security rules, business rules, or alternative architecture when a requirement is defined here.
If an implementation detail is genuinely unspecified, choose the simplest PostgreSQL/Supabase-compatible solution and document the decision in the migration or technical notes.

============================================================
SECTION 1 — DATABASE OVERVIEW
============================================================

## 1.1 Purpose

The database is the central persistent data layer of the English Teacher Gamification System.

It shall provide reliable, secure, structured storage for:

- Teacher accounts
- Teacher settings
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
- Import records
- Export records
- Stored file metadata
- System and gamification configuration

PostgreSQL shall be the authoritative source of truth.

## 1.2 Technology

Primary database:

PostgreSQL

Preferred managed platform:

Supabase

Preferred supporting services:

- Supabase Authentication
- Supabase Storage
- Supabase Row Level Security
- Supabase Edge Functions when server-side execution is required

The schema must remain compatible with standard PostgreSQL principles.

## 1.3 Database Philosophy

The database shall prioritize:

1. Data integrity
2. Database-level security
3. Historical preservation
4. Clear relationships
5. Minimal duplication
6. Query efficiency
7. Simple architecture
8. Maintainability
9. Version-controlled migrations
10. Appropriate scalability

## 1.4 Source of Truth

The database is authoritative.

The following must never become the authoritative source:

- Frontend state
- localStorage
- browser session state
- Telegram messages
- cached analytics
- exported files
- generated reports

Derived or cached values must be reproducible from authoritative records.

## 1.5 Project Scale

The initial system shall support:

- Maximum 40 teacher accounts
- Multiple groups per teacher
- Multiple students per group
- Multiple lessons per group
- Long-term academic history
- Long-term attendance history
- Homework history
- Payment history
- Gamification history
- Analytics history
- Activity history

The architecture must not introduce enterprise infrastructure without a real requirement.

## 1.6 Multi-Tenant Ownership

The system uses logical teacher-level multi-tenancy.

Primary ownership hierarchy:

Teacher
  -> Groups
      -> Students
          -> Academic Records

Teacher-owned data must be traceable to the authenticated teacher either directly through teacher_id or through a securely validated ownership relationship.

Frontend filtering alone is never sufficient for tenant isolation.

## 1.7 Historical Data

Historical records with academic, financial, analytical, or gamification value must be preserved.

Important historical records include:

- Attendance
- Homework
- Payments
- Point transactions
- XP transactions
- Level history
- Badges
- Achievements
- Streak history
- Certificates
- Activity logs
- Audit logs

Archiving or deactivating an entity must not unnecessarily destroy historical records.

## 1.8 Authoritative vs Derived Data

Authoritative data represents actual events or user actions.

Examples:

- Attendance event
- Homework evaluation
- Payment
- Point transaction
- XP transaction
- Certificate generation event

Derived data is calculated from authoritative records.

Examples:

- Current points
- Current XP
- Ranking
- Attendance percentage
- Monthly statistics
- Achievement progress
- Trend indicators

Derived data may be cached for performance, but the source records must remain available.

## 1.9 Transactional Integrity

Operations that modify multiple related records must be atomic where appropriate.

Example:

Attendance event
  -> Attendance record
  -> Point transaction
  -> XP transaction
  -> Achievement evaluation
  -> Streak evaluation
  -> Analytics update
  -> Activity log

A failure in a critical transaction must not leave an inconsistent partial state where practical.

## 1.10 Infrastructure Scope

Do not require:

- Microservices
- Kubernetes
- Dedicated database servers
- Redis
- Separate analytics databases
- Message queues

unless future requirements prove they are necessary.

============================================================
SECTION 2 — DATABASE ARCHITECTURE
============================================================

## 2.1 Architecture

Primary architecture:

Teacher
  -> Frontend Application
  -> Supabase Authentication
  -> Supabase API / secure server functions
  -> PostgreSQL
  -> Supabase Storage / external integrations

PostgreSQL remains the central persistent data layer.

## 2.2 Components

### Supabase Authentication

Responsible for:

- Teacher identity
- Login
- Sessions
- Authentication state

Authentication credentials must not be duplicated in application tables.

### PostgreSQL

Responsible for:

- Application records
- Relationships
- Constraints
- Transactions
- Historical records
- Gamification records
- Reporting source data

### RLS

Responsible for:

- Teacher data isolation
- Database-level authorization
- Cross-tenant protection

### Supabase Storage

Responsible for:

- Certificate files
- Certificate templates where stored as files
- Export files
- Import files where required
- Other application-managed files

Relational tables store file metadata and references, not large binary content where Storage is appropriate.

### Server-side Functions

Use Edge Functions or equivalent secure server-side logic for:

- Private credentials
- Telegram integration
- Sensitive external API calls
- Secure file processing
- Operations requiring privileged server execution

### Frontend

Responsible for:

- UI
- Input collection
- Data display
- Requests
- Analytics display
- Gamification display

The frontend must never bypass database security.

## 2.3 Logical Layers

1. Identity
2. Academic Structure
3. Academic Activity
4. Finance
5. Gamification
6. Documents
7. Analytics and Reporting
8. System Activity
9. Configuration

## 2.4 Data Flow

Teacher
  -> Group
  -> Student
  -> Lesson
  -> Attendance / Homework / Payment
  -> Transactions
  -> Gamification
  -> Analytics
  -> Reports

Every important teacher action should remain traceable to the resulting records.

## 2.5 Business Logic Boundary

Database responsibilities:

- Integrity
- Constraints
- Ownership enforcement
- Atomic transactions
- Deterministic low-level calculations
- Required audit records
- Timestamp management

Application/backend responsibilities:

- Complex workflows
- UI workflows
- Telegram message formatting
- External integrations
- Complex orchestration
- Non-critical presentation logic

Gamification rules must remain consistent with GAMIFICATION.md.

============================================================
SECTION 3 — CORE ENTITIES
============================================================

## 3.1 Entity Principles

Every entity must:

1. Have one clear responsibility.
2. Use explicit relationships.
3. Use foreign keys.
4. Preserve historical meaning.
5. Respect teacher ownership.
6. Separate authoritative and derived data.
7. Prevent duplicate authoritative events.
8. Remain PostgreSQL-compatible.
9. Avoid unnecessary complexity.

## 3.2 Identity Entities

### Teacher

Application profile linked to the authenticated Supabase user.

Stores:

- id
- profile information
- language
- account status
- timestamps

### Teacher Settings

Stores teacher-specific application preferences.

## 3.3 Academic Entities

### Group

Teacher-owned teaching group.

Stores:

- Group identity
- Name
- Description
- Level/category if required
- Status
- Schedule metadata if required
- Timestamps

### Student

Student belonging to a teacher and group.

Stores:

- Identity/profile information required by the application
- Group ownership
- Status
- Enrollment metadata
- Timestamps

A student must not have a login account.

### Lesson

Represents a lesson/class session for a group.

Stores:

- Group
- Teacher ownership
- Date/time
- Lesson status
- Topic/notes if required
- Timestamps

### Journal Record

Represents the classroom journal context connecting lesson, group, student, and academic activity.

The final implementation must avoid duplicate authoritative attendance/journal events.

## 3.4 Attendance Entities

### Attendance Record

Stores the student's attendance state for a lesson.

Required statuses:

- present
- absent_with_reason
- absent_without_reason
- late

The exact gamification effects are defined in GAMIFICATION.md.

## 3.5 Homework Entities

### Homework Assignment

Represents homework assigned to a group/student.

### Homework Result / Evaluation

Represents the student's evaluated homework outcome.

The system must preserve the original assignment and evaluation history.

Required homework status concepts must remain consistent with GAMIFICATION.md, including configured statuses such as:

- assigned
- completed
- perfect

## 3.6 Finance Entities

### Payment

Represents a student payment.

Payment records must remain independent from gamification unless explicitly configured.

Payment history must be preserved.

## 3.7 Gamification Entities

The database shall support:

- Point transactions
- XP transactions
- Level definitions
- Student level history/current level
- Rankings
- Badge definitions
- Student badge awards
- Achievement definitions
- Student achievement progress/awards
- Streaks
- Reward definitions
- Reward claims/redemptions where required

Transactions must be traceable to their source event where practical.

## 3.8 Document Entities

- Certificate templates
- Certificates
- Stored file metadata
- Import records
- Export records

## 3.9 Analytics Entities

Analytics should primarily be derived from authoritative records.

Persisted aggregates may be introduced only when justified by performance.

## 3.10 System Entities

- Notifications
- Activity logs
- Audit logs
- Import jobs
- Export jobs
- System events
- Configuration

============================================================
SECTION 4 — COMPLETE TABLE DEFINITIONS
============================================================

## 4.1 Table Definition Standard

Every required table must be documented and implemented with:

- Table name
- Purpose
- Primary key
- Columns
- PostgreSQL data types
- Nullable/non-nullable status
- Default values
- Foreign keys
- Unique constraints
- Check constraints
- Indexes
- Delete behavior
- Update behavior
- Teacher ownership
- Historical behavior
- Audit requirements

No required entity may remain only conceptual.

## 4.2 Required Table Inventory

The implementation must provide an explicit schema for, at minimum, the following tables or clearly documented equivalent normalized structures:

### Identity

- teachers
- teacher_settings

### Academic

- groups
- students
- lessons
- journal_records
- attendance_records
- teacher_notes

### Homework

- homework_assignments
- homework_results

### Finance

- payments

### Gamification

- point_transactions
- xp_transactions
- level_definitions
- student_levels
- ranking snapshots/derived structures only if needed
- badge_definitions
- student_badges
- achievement_definitions
- student_achievements
- streaks
- reward_definitions
- reward_claims if rewards are claimable

### Certificates

- certificate_templates
- certificates

### Analytics / Reporting

- reports
- persisted analytics tables only where justified

### System

- notifications
- activity_logs
- audit_logs
- import_jobs
- export_jobs
- stored_files

### Configuration

- gamification configuration/rules where required
- system configuration where required

If a table is intentionally omitted, the reason and replacement structure must be explicitly documented.

## 4.3 Standard Column Rules

Unless a specific table requires otherwise:

- Primary keys use UUID.
- Primary keys use gen_random_uuid().
- Timestamps use TIMESTAMPTZ.
- created_at is NOT NULL.
- updated_at is NOT NULL where records are mutable.
- Foreign keys use UUID.
- Status fields use controlled values.
- Monetary amounts use NUMERIC with suitable precision/scale.
- Counts use INTEGER.
- Boolean fields use BOOLEAN with explicit defaults.

## 4.4 Teacher Table

teachers:

- id UUID PRIMARY KEY
- full_name TEXT NOT NULL
- email TEXT NULL if duplicated from auth
- language TEXT NOT NULL
- status TEXT NOT NULL
- created_at TIMESTAMPTZ NOT NULL
- updated_at TIMESTAMPTZ NOT NULL

Allowed status:

- active
- suspended
- archived

id must correspond to the authenticated Supabase user ID.

## 4.5 Teacher Settings

teacher_settings:

- id UUID PRIMARY KEY
- teacher_id UUID NOT NULL UNIQUE
- language TEXT NOT NULL
- default_group_id UUID NULL
- notification_enabled BOOLEAN NOT NULL DEFAULT true
- created_at TIMESTAMPTZ NOT NULL
- updated_at TIMESTAMPTZ NOT NULL

default_group_id must reference a group owned by the same teacher.

## 4.6 Required Table Completion Rule

Before implementation is considered complete, every table listed in Section 4.2 must have a full field-level specification.

The AI/database implementer must not invent unspecified business fields silently.

============================================================
SECTION 5 — RELATIONSHIPS & FOREIGN KEYS
============================================================

## 5.1 Relationship Rules

1. Every child must reference an existing parent.
2. Teacher ownership must be preserved across relationships.
3. Cross-teacher relationships are prohibited.
4. Foreign keys must be explicit.
5. Delete behavior must be intentional.
6. Historical records should normally use RESTRICT/soft archival rather than destructive cascading.
7. Foreign key columns used in common queries must be indexed.

## 5.2 Core Relationship Map

teachers
  -> teacher_settings (1:1)
  -> groups (1:N)
  -> students (1:N where direct ownership is stored or derived)
  -> lessons (1:N)
  -> payments (1:N)
  -> certificates (1:N)
  -> certificate_templates (1:N)
  -> teacher_notes (1:N)
  -> activity_logs (1:N)
  -> audit_logs (1:N)
  -> notifications (1:N)
  -> reports (1:N)
  -> import_jobs (1:N)
  -> export_jobs (1:N)
  -> stored_files (1:N)

groups
  -> students (1:N)
  -> lessons (1:N)
  -> homework_assignments (1:N)

lessons
  -> journal_records (1:N)
  -> attendance_records (1:N)

students
  -> attendance_records (1:N)
  -> homework_results (1:N)
  -> payments (1:N)
  -> point_transactions (1:N)
  -> xp_transactions (1:N)
  -> student_levels
  -> student_badges (1:N)
  -> student_achievements (1:N)
  -> streaks (1:N)
  -> certificates (1:N)
  -> teacher_notes (1:N)

## 5.3 Delete Rules

Use conservative deletion policies.

Examples:

- Teacher deletion: normally prohibited or archival.
- Group deletion: archive/deactivate when historical records exist.
- Student deletion: archive/deactivate when history exists.
- Lesson deletion: preserve historical records where required.
- Attendance deletion: prohibited for finalized historical records unless an authorized correction workflow exists.
- Payment deletion: prohibited or tightly controlled.
- Point/XP transaction deletion: prohibited for finalized transactions; use reversal/correction records.
- Audit log deletion: prohibited under normal application operation.

Exact ON DELETE actions must be documented for every FK.

## 5.4 Cross-Tenant Integrity

A record must never be able to reference a parent belonging to another teacher.

Where PostgreSQL constraints alone cannot enforce the complete ownership condition, use secure database functions, triggers, or backend validation together with RLS.

============================================================
SECTION 6 — ROW LEVEL SECURITY & TENANT ISOLATION
============================================================

## 6.1 RLS Requirement

RLS is mandatory for all teacher-owned tables exposed through Supabase.

Teachers may access only their own data.

Students have no direct login and therefore no student RLS access model is required.

## 6.2 RLS Coverage

RLS must cover all applicable tables including:

- teachers
- teacher_settings
- groups
- students
- lessons
- journal_records
- attendance_records
- homework_assignments
- homework_results
- payments
- point_transactions
- xp_transactions
- student_levels
- student_badges
- student_achievements
- streaks
- rewards/reward_claims
- certificates
- certificate_templates
- teacher_notes
- reports
- notifications
- activity_logs
- audit_logs
- import_jobs
- export_jobs
- stored_files

System configuration tables that are not teacher-owned may use controlled read access instead.

## 6.3 Policy Model

For every teacher-owned table define:

- SELECT policy
- INSERT policy
- UPDATE policy
- DELETE policy

Where deletion is prohibited, do not create a DELETE policy.

The ownership condition must resolve through the authenticated user.

Typical ownership path:

auth.uid()
  -> teachers.id
  -> teacher_id
or
auth.uid()
  -> teachers.id
  -> groups.teacher_id
  -> students.group_id
  -> child record

## 6.4 RLS Security Requirements

- Default deny is preferred.
- Frontend filtering is never security.
- Service-role credentials must never be exposed to the browser.
- Privileged functions must be tightly controlled.
- SECURITY DEFINER functions must explicitly validate ownership and search_path.
- Cross-tenant access must be impossible through ordinary authenticated requests.

============================================================
SECTION 7 — INDEXES & QUERY PERFORMANCE
============================================================

## 7.1 Principles

Indexes shall be based on real query patterns.

Required priorities:

1. Journal loading
2. Attendance updates
3. Homework updates
4. Student search
5. Dashboard statistics
6. Rankings
7. Analytics
8. Activity history

## 7.2 Required Index Categories

At minimum evaluate indexes for:

- teacher_id
- group_id
- student_id
- lesson_id
- created_at
- updated_at
- date/time fields
- status fields when selective
- due_date
- payment date
- transaction date

## 7.3 Composite Index Patterns

Evaluate composite indexes such as:

- groups(teacher_id, status)
- students(teacher_id, group_id, status)
- lessons(group_id, lesson_date)
- attendance_records(student_id, lesson_id)
- attendance_records(group_id, lesson_date) where supported by schema
- homework_assignments(group_id, due_date)
- homework_results(student_id, created_at)
- point_transactions(student_id, created_at)
- xp_transactions(student_id, created_at)
- activity_logs(teacher_id, created_at)
- notifications(teacher_id, created_at)

Only create indexes justified by actual access patterns.

## 7.4 Uniqueness and Indexes

Use unique constraints to prevent duplicate authoritative events.

Examples:

- One attendance record per student per lesson.
- One homework result per student per assignment unless the business rule explicitly permits multiple attempts.
- One teacher_settings row per teacher.
- One student badge award per applicable award event where appropriate.
- Stable unique configuration identifiers.

## 7.5 Query Rules

- Select only required columns.
- Use database-side filtering.
- Avoid N+1 queries.
- Paginate large result sets.
- Use keyset/cursor pagination for large histories where beneficial.
- Review expensive queries with EXPLAIN ANALYZE.
- Do not bypass RLS for performance.

============================================================
SECTION 8 — DATA INTEGRITY, CONSTRAINTS & VALIDATION
============================================================

## 8.1 Constraint Hierarchy

Use:

- NOT NULL
- PRIMARY KEY
- FOREIGN KEY
- UNIQUE
- CHECK
- RLS
- Transactional validation
- Backend validation

## 8.2 Required Validation

Required business-state validation includes:

Attendance:

- present
- absent_with_reason
- absent_without_reason
- late

Teacher status:

- active
- suspended
- archived

All status values must use controlled values.

## 8.3 Numeric Validation

Where applicable:

- payment amount >= 0
- points/XP amounts must follow transaction rules
- counts >= 0
- percentages must remain within 0–100
- level numbers must be valid positive integers
- dates must follow business chronology

## 8.4 Duplicate Prevention

Prevent duplicate authoritative records.

Examples:

- duplicate attendance for the same student and lesson
- duplicate payment identifiers where applicable
- duplicate teacher settings
- duplicate badge awards when the award is intended to be unique

## 8.5 Historical Integrity

Historical transactions must not be silently overwritten.

For point/XP corrections, prefer:

original transaction
  -> reversal/correction transaction
  -> audit record

rather than destructive editing.

## 8.6 Timestamp Integrity

created_at is immutable.

updated_at changes only when a mutable record is modified.

Use a centralized timestamp trigger/function where appropriate.

## 8.7 Ownership Validation

A record cannot be inserted or updated if its referenced parent belongs to another teacher.

This must be enforced beyond frontend validation.

============================================================
SECTION 9 — DATABASE FUNCTIONS, TRIGGERS & AUTOMATION
============================================================

## 9.1 Principles

Use database functions/triggers for:

- Integrity
- Atomic deterministic operations
- Shared validation
- Timestamp maintenance
- Security-sensitive checks
- Small deterministic calculations

Keep complex orchestration in the application/backend layer.

## 9.2 Recommended Function Categories

1. Timestamp functions
2. Ownership validation functions
3. Security helper functions
4. Deterministic aggregation functions
5. Gamification transaction helpers where atomicity is required
6. Reporting/query functions where justified

## 9.3 Trigger Candidates

Appropriate trigger candidates include:

- updated_at maintenance
- ownership integrity checks
- immutable audit requirements
- deterministic derived synchronization only where necessary

Do not use triggers for large, opaque business workflows.

## 9.4 Gamification Transaction Rule

Attendance/homework operations that create points and XP must be atomic when the business rules require it.

The exact points and XP rules must come from GAMIFICATION.md.

The database must not contain a second conflicting set of gamification rules.

## 9.5 Function Security

Every privileged function must:

- Validate ownership
- Use explicit privileges
- Avoid exposing sensitive data
- Use a safe search_path where applicable
- Be documented
- Be migration-controlled

## 9.6 Trigger Safety

Triggers must:

- Have one clear purpose
- Avoid recursion
- Avoid hidden side effects
- Be tested
- Be documented

============================================================
SECTION 10 — DATABASE SECURITY ARCHITECTURE
============================================================

## 10.1 Security Model

Security must use defense in depth:

Authentication
  -> Authorization
  -> RLS
  -> Constraints
  -> Secure functions
  -> Restricted infrastructure access
  -> Auditability

## 10.2 Authentication

Supabase Authentication manages teacher identity.

Application tables reference the stable auth user UUID.

Passwords and authentication secrets must not be stored in application tables.

## 10.3 Secrets

Never store in source code:

- Supabase service-role keys
- Telegram bot tokens
- API keys
- Database passwords
- Private credentials

Use environment variables or managed secrets.

## 10.4 Privileges

Use least privilege.

Browser clients must not receive privileged database credentials.

Service-role access must be limited to trusted server-side execution.

## 10.5 Sensitive Data

Store only data necessary for the application.

Do not store unnecessary sensitive personal information.

## 10.6 Security Testing

Before production:

- Test cross-teacher SELECT
- Test cross-teacher INSERT
- Test cross-teacher UPDATE
- Test cross-teacher DELETE
- Test privileged function access
- Test Storage access
- Test archived record access
- Test unauthorized IDs

All must fail appropriately.

============================================================
SECTION 11 — SEED DATA & INITIAL CONFIGURATION
============================================================

## 11.1 Seed Principles

Seed data must be:

- Deterministic
- Repeatable
- Idempotent
- Version-controlled
- Safe for production
- Free of secrets

Production teacher/student data must not be part of default seed data.

## 11.2 Seed Categories

Seed/configuration data may include:

1. Gamification rules
2. Point rules
3. XP rules
4. Level definitions
5. Badge definitions
6. Achievement definitions
7. Homework status definitions
8. Attendance statuses
9. Payment statuses
10. System configuration

## 11.3 Configuration Ownership

System configuration must be clearly separated from teacher-owned data.

If teachers can customize a rule, define whether the rule is:

- global
- teacher-specific
- immutable after activation
- versioned

## 11.4 Seed Separation

Use separate development/test seed data from production configuration.

Do not overwrite production data during seed operations.

============================================================
SECTION 12 — MIGRATIONS & VERSION CONTROL
============================================================

## 12.1 Migration Principles

All database changes must be version-controlled.

No undocumented manual production schema changes.

Migrations must be:

- Ordered
- Reproducible
- Tested
- Deterministic
- Reviewable

## 12.2 Migration Scope

Migrations must include changes to:

- Tables
- Columns
- Foreign keys
- Constraints
- Indexes
- Functions
- Triggers
- RLS policies
- Seed/configuration data

## 12.3 Directory

Recommended:

database/
  migrations/
    001_initial_schema.sql
    002_core_relationships.sql
    003_journal_and_attendance.sql
    004_homework.sql
    005_finance.sql
    006_gamification.sql
    007_indexes.sql
    008_constraints.sql
    009_functions.sql
    010_rls.sql
    011_seed_configuration.sql
    ...

## 12.4 Migration Rules

- Never silently modify an already-applied migration.
- Create a new migration for changes.
- Destructive migrations require review.
- Test migrations against a clean database.
- Test upgrade migrations against a representative existing database.
- Keep application schema and migrations synchronized.

## 12.5 Schema Drift

Production schema must be reproducible from the repository migrations.

Any detected drift must be investigated and resolved.

============================================================
SECTION 13 — BACKUP, RESTORE & DISASTER RECOVERY
============================================================

## 13.1 Scope

Recovery must protect:

- Schema
- Tables
- Constraints
- Functions
- Triggers
- RLS policies
- Configuration
- Teacher data
- Student data
- Attendance
- Homework
- Payments
- Gamification
- Activity history
- Required Storage metadata/files

## 13.2 Backup Principles

- Automated where supported
- Protected from unauthorized access
- Independently recoverable
- Monitored
- Retained according to policy
- Periodically restore-tested

## 13.3 Recovery Objectives

The project must define operational targets for:

RPO:
Maximum acceptable data loss.

RTO:
Maximum acceptable recovery time.

The initial values should be selected according to the project's actual operational needs and documented before production launch.

## 13.4 Restore Testing

A backup is not considered valid until a restore has been tested.

Restore testing must verify:

- Schema
- Data
- Constraints
- RLS
- Functions
- Triggers
- Application connectivity
- Storage references where applicable

## 13.5 Incident Recovery

Recovery procedures must cover:

- Accidental deletion
- Failed migration
- Corruption
- Credential compromise
- Hosting failure
- Operational mistake

============================================================
SECTION 14 — DATA ARCHIVING, RETENTION & DELETION
============================================================

## 14.1 Archiving Principles

Historical data must not be deleted merely to improve performance.

Archived data must:

- Remain recoverable
- Preserve historical meaning
- Respect RLS
- Remain auditable
- Not change historical business results

## 14.2 Active vs Archived

Active data:
Frequently used operational records.

Archived data:
Historical records retained for reference and compliance/business needs.

## 14.3 Soft Deactivation

Where historical records exist, prefer status-based deactivation or archival over destructive deletion.

Examples:

- teacher status
- group status
- student status
- certificate status where applicable

## 14.4 Retention Policy

Retention periods must be defined for:

- Activity logs
- Audit logs
- Notifications
- Import/export records
- Archived records
- Generated files
- Temporary files

Do not invent legal retention periods. Use project requirements and applicable law/policy.

## 14.5 Permanent Deletion

Permanent deletion must be a separate controlled process.

It must:

- Require authorization
- Respect dependencies
- Be auditable
- Avoid accidental destruction of financial/academic history

============================================================
SECTION 15 — MONITORING & OBSERVABILITY
============================================================

## 15.1 Monitoring Scope

Monitor:

- Availability
- Query latency
- Error rates
- Connection failures
- Connection pool usage
- Database size
- Storage growth
- Slow queries
- Locks/blocking
- Failed migrations
- Backup failures
- Unexpected security anomalies

## 15.2 Logging

Logs must provide enough diagnostic information without exposing:

- Passwords
- API keys
- Tokens
- Unnecessary personal data
- Sensitive credentials

## 15.3 Alerts

Critical alerts should cover:

- Database unavailable
- Repeated connection failure
- Backup failure
- Migration failure
- Severe resource exhaustion
- Abnormal error rate
- Storage exhaustion risk

## 15.4 Auditability

Business-critical administrative actions must be traceable through audit/activity records where required.

============================================================
SECTION 16 — ACCESS CONTROL, PRIVILEGES & OPERATIONAL SECURITY
============================================================

## 16.1 Purpose

This section covers operational database access separately from tenant RLS.

RLS answers:

"Which records may this authenticated teacher access?"

Access control answers:

"Which technical identities may perform which database operations?"

## 16.2 Least Privilege

Technical identities must receive only the permissions they require.

Separate, where practical:

- Browser/authenticated client access
- Trusted server-side access
- Administrative/deployment access

## 16.3 Production Access

Direct production database access must be restricted.

Administrative credentials must not be used in frontend code.

## 16.4 Service Role

Supabase service-role credentials bypass normal RLS protections and therefore must only be used in trusted server-side environments.

Never expose them to browser clients.

## 16.5 Storage Security

Storage buckets must have appropriate access policies.

A teacher must not access another teacher's private certificate/export/import files.

File paths should include a secure ownership strategy.

## 16.6 Operational Audit

Significant administrative/security operations should be auditable.

============================================================
SECTION 17 — PERFORMANCE & OPTIMIZATION
============================================================

## 17.1 Principles

1. Retrieve only required data.
2. Use appropriate indexes.
3. Paginate large datasets.
4. Avoid N+1 queries.
5. Keep transactions short where possible.
6. Use database-side filtering.
7. Do not bypass RLS for performance.
8. Measure before optimizing.
9. Prefer the simplest architecture that satisfies workload.

## 17.2 Primary Workloads

Optimize for:

- Journal loading
- Attendance updates
- Homework updates
- Student search
- Dashboard statistics
- Rankings
- Analytics
- Activity history

## 17.3 Performance Targets

Initial engineering targets:

- Simple indexed lookup: target <= 100 ms database execution under normal workload.
- Common journal query: target <= 500 ms database execution under normal workload.

These are engineering targets, not guarantees.

End-to-end application latency must be evaluated separately.

## 17.4 Pagination

Use pagination for:

- Activity logs
- Audit logs
- Point transactions
- XP transactions
- Attendance history
- Homework history
- Payments
- Student lists
- Reports where necessary

Use cursor/keyset pagination for large histories when beneficial.

## 17.5 Aggregation

Do not repeatedly calculate expensive analytics for every request if the same results can be safely cached or aggregated.

However, persisted aggregates must remain derived and rebuildable.

## 17.6 Scalability

The system must comfortably support the initial maximum of 40 teachers without enterprise infrastructure.

Future scaling decisions must be based on measured workload.

============================================================
SECTION 18 — DATABASE MAINTENANCE & LIFECYCLE
============================================================

## 18.1 Maintenance

PostgreSQL maintenance mechanisms should be used appropriately:

- VACUUM
- ANALYZE
- Autovacuum
- Autoanalyze

## 18.2 Growth Monitoring

Monitor growth of:

- Attendance records
- Homework records
- Transactions
- Activity logs
- Audit logs
- Notifications
- Stored files
- Reports

## 18.3 Index Maintenance

Indexes must be reviewed when:

- Query patterns change
- Tables grow significantly
- Write performance degrades
- Duplicate indexes are detected
- Query plans change

## 18.4 Deprecated Schema

Deprecated tables/columns must:

1. Be marked deprecated.
2. Stop receiving new writes.
3. Be migrated where necessary.
4. Remain available until safe removal.
5. Be removed only through migrations.

## 18.5 Maintenance Safety

Maintenance must not:

- bypass RLS
- destroy historical data accidentally
- change historical business results
- break application migrations
- interrupt normal teacher workflows unnecessarily

============================================================
SECTION 19 — DATABASE TESTING & VALIDATION
============================================================

## 19.1 Purpose

The database is not complete until its structure and security have been tested.

## 19.2 Schema Tests

Verify:

- All required tables exist.
- All required columns exist.
- Data types are correct.
- NOT NULL constraints are correct.
- Defaults are correct.
- Foreign keys exist.
- Unique constraints exist.
- Check constraints exist.
- Indexes exist.

## 19.3 Relationship Tests

Verify:

- Valid parent-child records succeed.
- Missing parents fail.
- Cross-teacher relationships fail.
- Duplicate authoritative events fail.

## 19.4 RLS Tests

For at least two teacher identities:

Teacher A must not be able to:

- SELECT Teacher B data
- INSERT into Teacher B-owned relationships
- UPDATE Teacher B data
- DELETE Teacher B data

Teacher B must have the same isolation.

## 19.5 Transaction Tests

Test critical workflows:

Attendance
  -> points
  -> XP
  -> achievement/streak processing
  -> activity log

Homework
  -> evaluation
  -> points
  -> XP
  -> achievement processing
  -> activity log

Payment
  -> payment record
  -> status/statistics
  -> activity log

Certificate
  -> certificate record
  -> file reference
  -> activity log

Critical failures must not leave inconsistent partial data.

## 19.6 Migration Tests

Test:

- Clean installation
- Upgrade from previous migration
- Roll-forward
- Destructive migration safety
- Seed idempotency

## 19.7 Performance Tests

Test representative workloads for:

- Journal loading
- Attendance updates
- Student search
- Homework history
- Rankings
- Dashboard statistics
- Activity logs

============================================================
SECTION 20 — DOCUMENTATION, GOVERNANCE & FINAL ACCEPTANCE
============================================================

## 20.1 Documentation Requirements

The repository must document:

- Schema
- Relationships
- RLS
- Constraints
- Indexes
- Functions
- Triggers
- Migrations
- Seed configuration
- Backup/recovery
- Monitoring
- Maintenance
- Testing

## 20.2 Cross-Document Consistency

DATABASE.md must remain consistent with:

- PROJECT_REQUIREMENTS.md
- GAMIFICATION.md
- API_SPECIFICATION.md
- TECH_STACK.md
- UI_GUIDE.md
- DEVELOPMENT_RULES.md
- DEPLOYMENT.md
- ROADMAP.md

If another document defines a business rule, DATABASE.md must not silently contradict it.

## 20.3 Maximum Teacher Count

The authoritative project limit is:

MAXIMUM TEACHERS = 40

No database documentation or schema constraint may incorrectly use the previous 20-teacher limit.

The database must not artificially limit teacher count to 40 through a database row constraint unless explicitly required; 40 is the intended project capacity, not necessarily a hard SQL constraint.

## 20.4 Final Database Acceptance Criteria

DATABASE.md is considered implementation-ready only when all of the following are true:

[ ] All required entities are defined.
[ ] All required tables are fully specified.
[ ] Every table has a primary key.
[ ] Every required foreign key is defined.
[ ] Delete/update behavior is defined.
[ ] Required NOT NULL constraints are defined.
[ ] Required UNIQUE constraints are defined.
[ ] Required CHECK constraints are defined.
[ ] Required indexes are defined.
[ ] Teacher ownership is defined for every teacher-owned record.
[ ] RLS coverage is defined for every teacher-owned table.
[ ] SELECT/INSERT/UPDATE/DELETE policies are defined where applicable.
[ ] Cross-teacher access is prevented.
[ ] Student login is not required.
[ ] Authentication uses Supabase Auth.
[ ] Service-role credentials are server-side only.
[ ] Storage ownership is secured.
[ ] Historical records are preserved.
[ ] Point and XP transactions are traceable.
[ ] Gamification rules do not conflict with GAMIFICATION.md.
[ ] Seed data is deterministic and idempotent.
[ ] Migrations are version-controlled.
[ ] Backup and restore procedures are documented.
[ ] RPO/RTO targets are documented before production.
[ ] Monitoring and alerting requirements are defined.
[ ] Maintenance requirements are defined.
[ ] Database tests are defined.
[ ] Performance targets are defined.
[ ] The schema supports the intended maximum of 40 teachers.
[ ] Markdown/code blocks are syntactically valid.
[ ] No duplicate/conflicting database sections remain.
[ ] No critical schema decision is left to undocumented AI assumptions.

## 20.5 Final Implementation Rule

The implementation team or AI builder must not consider the database complete merely because the application can run.

The database is complete only when:

1. The schema is fully defined.
2. Relationships are enforced.
3. RLS is enforced.
4. Constraints prevent invalid states.
5. Critical workflows are transactional.
6. Historical records are protected.
7. Migrations reproduce the schema.
8. Backup and recovery are operationally defined.
9. Tests verify security and integrity.
10. The database remains consistent with the other project documents.

END OF DATABASE.md

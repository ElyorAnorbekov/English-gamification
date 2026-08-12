DEPLOYMENT.md — FINAL 20-SECTION IMPLEMENTATION PLAN

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
- DATABASE.md — database architecture and persistence
- UI_GUIDE.md — UI implementation and UX standards
- GAMIFICATION.md — gamification business rules
- API_SPECIFICATION.md — API contracts
- TECH_STACK.md — approved technology stack
- DEVELOPMENT_RULES.md — development and coding standards
- DEPLOYMENT.md — deployment, environments, infrastructure, release, recovery, and operational standards

Deployment principle:
The deployment architecture must be the simplest reliable architecture that satisfies the project's requirements. Do not introduce unnecessary infrastructure, services, or operational complexity.


SECTION 1 — Deployment Architecture & Core Principles

Define the complete deployment architecture.

Include:
- Overall deployment model
- Frontend hosting
- Supabase project
- PostgreSQL
- Authentication
- Storage
- Edge/server functions
- Telegram integration
- Environment separation
- Domain/HTTPS
- Monitoring
- Backup/recovery
- Maximum 40 teachers
- Lightweight infrastructure
- No unnecessary microservices
- Source-of-truth principle
- Completion criteria

The production architecture must remain consistent with TECH_STACK.md.


SECTION 2 — Environments & Environment Separation

Define development, testing, staging, and production environments.

Include:
- Local development
- Test environment
- Staging environment where justified
- Production environment
- Environment-specific configuration
- Environment-specific Supabase projects/configuration where appropriate
- Database isolation
- Storage isolation
- Telegram integration isolation
- Test data isolation
- Production data protection
- Environment promotion rules

Production data must never be used casually for development or testing.


SECTION 3 — Hosting & Frontend Deployment

Define how the frontend application is built and hosted.

Include:
- Approved hosting approach
- Build process
- Production build
- Static/dynamic deployment requirements
- Environment variables
- HTTPS
- Custom domain where applicable
- SPA/route handling if applicable
- Asset caching
- CDN behavior where provided by the host
- Deployment previews where useful
- Rollback strategy
- Hosting limitations
- Free/lightweight hosting preference

The hosting solution must be compatible with TECH_STACK.md.


SECTION 4 — Supabase & PostgreSQL Deployment

Define the deployment of the backend platform and database.

Include:
- Supabase project configuration
- PostgreSQL
- Authentication
- Storage
- RLS
- Database extensions where required
- Database functions
- Triggers
- Indexes
- Constraints
- Database configuration
- Project settings
- Production access controls

Supabase/PostgreSQL must remain the authoritative persistence layer.


SECTION 5 — Database Migrations & Schema Deployment

Define the production database migration process.

Include:
- Version-controlled migrations
- Migration order
- Migration validation
- Development migration testing
- Staging migration testing where applicable
- Production migration procedure
- Destructive migration policy
- Data migration policy
- Rollback/recovery considerations
- Migration failure handling
- Migration history
- Schema synchronization
- No undocumented manual production schema changes

All migrations must be reproducible from the repository.


SECTION 6 — Authentication, Authorization & RLS Deployment

Define production security configuration.

Include:
- Supabase Authentication
- Teacher accounts
- Maximum 40 teachers
- Session configuration
- Authentication redirects
- Account status
- RLS policies
- Teacher ownership
- Service-role access
- Backend permissions
- Storage permissions
- No student login
- Production authorization testing
- Cross-teacher access testing

Security configuration must remain consistent with DATABASE.md and API_SPECIFICATION.md.


SECTION 7 — Storage & File Deployment

Define production file-storage configuration.

Include:
- Supabase Storage
- Buckets
- Bucket access policies
- Certificate files
- Certificate templates
- Homework files
- Import files
- Export files
- File metadata
- File naming/path conventions
- Signed URLs where appropriate
- File size limits
- Allowed file types
- Cleanup policy
- Backup considerations
- Access testing

Storage permissions must prevent cross-teacher access.


SECTION 8 — Edge Functions, Server Functions & API Deployment

Define deployment of server-side functions and APIs.

Include:
- Supabase Edge Functions where applicable
- Function organization
- Environment variables
- Secrets
- Authentication context
- RLS interaction
- Service-role usage
- External API communication
- Telegram integration
- Error handling
- Timeouts
- Retry behavior
- Idempotency
- Logging
- Function versioning
- Deployment validation

No secret credential may be exposed to the frontend.


SECTION 9 — Telegram Integration Deployment

Define production deployment for Telegram reporting.

Include:
- Telegram Bot API
- Bot credentials
- Secret storage
- Target group/channel configuration
- Teacher/group reporting rules
- Message generation
- Delivery status
- Retry handling
- Failure handling
- Rate considerations
- Timeout handling
- Idempotency where required
- Logging
- Test vs production Telegram destinations

Telegram must remain an output integration and never become the source of truth.


SECTION 10 — Environment Variables, Secrets & Configuration

Define all production configuration management requirements.

Include:
- Environment variables
- Public configuration
- Private configuration
- Supabase URL
- Public/anon/publishable key as appropriate
- Service-role secret
- Telegram credentials
- Storage configuration
- API configuration
- Application URLs
- Authentication redirect URLs
- Secret rotation
- `.env.example`
- No secrets in Git
- No secrets in frontend bundles
- Missing configuration behavior

Secrets must be managed through the hosting/platform secret mechanism rather than source code.


SECTION 11 — CI/CD & Automated Deployment

Define continuous integration and deployment.

Include:
- Repository-based deployment
- Automated checks
- Type checking
- Linting
- Formatting
- Unit tests
- Integration tests
- Build validation
- Migration validation
- Deployment gates
- Preview builds where appropriate
- Staging deployment where justified
- Production approval
- Deployment logs
- Failed deployment handling
- Rollback process

CI/CD must remain lightweight and must not introduce unnecessary tooling.


SECTION 12 — Release Management & Versioning

Define how application releases are prepared and deployed.

Include:
- Release preparation
- Versioning strategy
- Feature completion
- Bug fixes
- Database migration readiness
- API compatibility
- UI compatibility
- Gamification rule changes
- Release notes
- Changelog updates
- Pre-release checklist
- Production release
- Post-release verification
- Rollback decision criteria

Major business-rule or schema changes require additional validation.


SECTION 13 — Backup, Restore & Disaster Recovery

Define production recovery architecture.

Include:
- Automated database backups where supported
- Backup retention
- Point-in-time recovery where available
- Backup protection
- Storage/file recovery
- Configuration recovery
- Migration recovery
- Accidental deletion recovery
- Database corruption recovery
- Infrastructure failure recovery
- Restore testing
- Recovery procedures
- Recovery documentation
- Recovery responsibilities

Define practical recovery objectives appropriate for the project's scale without unnecessary enterprise infrastructure.


SECTION 14 — Monitoring, Logging & Observability

Define production monitoring.

Include:
- Application availability
- Database availability
- API/function availability
- Authentication failures
- Database errors
- Slow queries
- Storage usage
- Function failures
- Telegram failures
- Backup failures
- Deployment failures
- Resource usage
- Error logging
- Alerting
- Diagnostic information
- Sensitive-data protection in logs

Monitoring must provide enough information to diagnose failures without exposing private data.


SECTION 15 — Performance & Production Optimization

Define production performance requirements.

Include:
- Production build optimization
- Code splitting
- Lazy loading
- Asset optimization
- Caching
- API payload optimization
- Database query efficiency
- Index usage
- Pagination
- Journal optimization
- Ranking optimization
- Analytics optimization
- Avoiding N+1 queries
- Avoiding unnecessary requests
- Avoiding unnecessary re-renders
- Resource limits
- Performance monitoring

The Dynamic Journal Core must remain responsive under realistic teacher workloads.


SECTION 16 — Security Hardening & Production Access

Define production security hardening.

Include:
- HTTPS
- Secure authentication configuration
- RLS verification
- Least privilege
- Service-role key protection
- Secret protection
- Storage policy verification
- Dependency security
- Input validation
- File security
- Secure headers where appropriate
- CORS configuration where applicable
- Production admin access
- Database access restrictions
- Auditability
- Security incident response
- No frontend-only security assumptions

Production security must be tested before release.


SECTION 17 — Deployment Testing & Verification

Define mandatory pre-production and post-deployment testing.

Include:
- Authentication testing
- Teacher isolation testing
- RLS testing
- Database migration testing
- CRUD testing
- Journal testing
- Attendance testing
- Homework testing
- Payment testing
- Gamification testing
- Ranking testing
- Analytics testing
- Certificate testing
- Storage testing
- Telegram testing
- Error handling
- Mobile/responsive testing
- Performance testing
- Backup/restore testing where applicable

Testing must use realistic teacher workflows and must not rely only on happy-path scenarios.


SECTION 18 — Rollback, Failure Recovery & Incident Response

Define how failed deployments and incidents are handled.

Include:
- Deployment failure
- Migration failure
- Application regression
- Database issue
- Authentication failure
- Storage failure
- Edge Function failure
- Telegram failure
- Configuration error
- Security incident
- Rollback decision
- Application rollback
- Migration recovery
- Data recovery
- Communication
- Incident logging
- Post-incident review

Never perform a destructive rollback that silently destroys authoritative historical data.


SECTION 19 — Operational Maintenance & Lifecycle Management

Define ongoing production operations.

Include:
- Dependency updates
- Security updates
- Database maintenance
- Storage cleanup
- Log retention
- Backup verification
- Migration maintenance
- Deprecated feature handling
- Deprecated dependency removal
- Environment-variable review
- Access review
- Performance review
- Capacity review
- Monitoring review
- Documentation updates
- Scheduled maintenance where required

Maintenance must not unnecessarily interrupt teacher workflows.


SECTION 20 — Final Deployment Checklist, Governance & Acceptance

Define the final production acceptance standard.

Pre-deployment checklist:
- Build passes
- Tests pass
- Type checks pass
- Lint checks pass
- Environment variables verified
- Secrets verified
- Database migrations verified
- RLS verified
- Storage policies verified
- Authentication verified
- API verified
- Gamification verified
- Journal verified
- Telegram verified
- Backup verified
- Monitoring verified
- HTTPS verified
- Rollback procedure known

Post-deployment verification:
- Application loads successfully
- Teacher login works
- Teacher data isolation works
- Groups load correctly
- Journal works
- Attendance updates correctly
- Homework works
- Payments work
- Gamification transactions work
- Rankings work
- Analytics work
- Reports work
- Certificates work
- Telegram reporting works
- Errors are handled correctly
- Performance is acceptable

Governance:
- Deployment configuration is documented.
- Infrastructure changes are version-controlled where practical.
- Production changes are reproducible.
- No undocumented production infrastructure is introduced.
- No secret is committed to the repository.
- No manual database change bypasses migration governance.
- Deployment architecture must remain consistent with TECH_STACK.md.
- Database deployment must remain consistent with DATABASE.md.
- UI deployment must remain consistent with UI_GUIDE.md.
- Gamification deployment must remain consistent with GAMIFICATION.md.
- API deployment must remain consistent with API_SPECIFICATION.md.
- Development processes must remain consistent with DEVELOPMENT_RULES.md.

Final acceptance criteria:

Production deployment is considered complete only when:
- The application is deployable through a reproducible process.
- Development and production environments are appropriately separated.
- Frontend hosting is configured.
- Supabase/PostgreSQL is configured.
- Database migrations are reproducible.
- Authentication is secure.
- RLS is verified.
- Storage is secure.
- Server-side functions are deployed securely.
- Telegram integration is configured securely.
- Secrets are protected.
- CI/CD or an equivalent controlled deployment process is defined.
- Backups and recovery procedures are defined.
- Monitoring and logging are operational.
- Performance is acceptable.
- Security hardening is complete.
- Rollback and incident procedures are documented.
- Production workflows have been tested.
- The system remains lightweight and appropriate for maximum 40 teachers.
- No unnecessary infrastructure has been introduced.
- The deployment architecture does not contradict any authoritative project document.
- The application is practical and reliable for real classroom use.

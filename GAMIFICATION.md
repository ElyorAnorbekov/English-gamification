GAMIFICATION.md — FINAL 20-SECTION IMPLEMENTATION PLAN

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
- Database source of truth
- UI must remain consistent with PROJECT_REQUIREMENTS.md, DATABASE.md, and UI_GUIDE.md


SECTION 1 — Gamification Architecture & Core Principles

Define the complete gamification architecture and its purpose.

Include:
- Purpose of gamification
- Teacher-first classroom usage
- Student motivation without unnecessary complexity
- Maximum 40 teacher accounts
- Group-based gamification
- Student-level progress
- Database as the source of truth
- Separation of authoritative transactions and derived statistics
- Consistency with PROJECT_REQUIREMENTS.md
- Consistency with DATABASE.md
- Consistency with UI_GUIDE.md
- No conflicting business rules
- Maintainability
- Scalability
- Completion criteria


SECTION 2 — Gamification Entities & Data Model

Define all core gamification entities and their responsibilities.

Include:
- Students
- Groups
- Point transactions
- XP transactions
- Levels
- Monthly levels
- Rankings
- Badges
- Achievements
- Achievement progress
- Streaks
- Rewards
- Gamification events
- Configuration/rules
- Historical records

Define:
- Authoritative entities
- Derived entities
- Relationships
- Ownership
- Historical preservation
- Entity dependencies

All persistent entities must remain compatible with DATABASE.md.


SECTION 3 — Points System

Define the complete points architecture.

Include:
- Purpose of points
- Point transaction model
- Positive points
- Negative points where explicitly allowed
- Source/event of each transaction
- Reason/category
- Manual teacher adjustments
- Automatic point awards
- Point history
- Point reversal/correction
- Idempotency
- Duplicate prevention
- Auditability
- Current point calculation
- Group-level point visibility
- Student-level point visibility
- Historical point preservation

Critical rule:
Points must be generated according to explicit business rules and must not be invented by the UI.


SECTION 4 — Attendance Gamification Rules

Define all gamification effects related to attendance.

Attendance states:
- Present
- Absent with reason
- Absent without reason
- Late

Include:
- Point effects
- XP effects
- Streak effects
- Achievement effects
- Correction behavior
- Recalculation behavior
- Duplicate-event prevention
- Historical transaction preservation
- Teacher correction workflow
- Edge cases

All attendance rules must remain consistent with PROJECT_REQUIREMENTS.md and the Dynamic Journal Core.


SECTION 5 — Homework Gamification Rules

Define all gamification effects related to homework.

Homework statuses:
- Assigned
- Completed
- Perfect

Include:
- Point effects
- XP effects
- Achievement effects
- Streak effects where applicable
- Evaluation changes
- Re-evaluation behavior
- Correction/reversal behavior
- Duplicate prevention
- Homework history
- Sequential homework workflow
- File-related events where relevant

The exact scoring rules must be explicitly defined and must not be duplicated inconsistently in UI_GUIDE.md.


SECTION 6 — XP System

Define the complete XP architecture.

Include:
- Purpose of XP
- XP transaction model
- XP sources
- Attendance XP
- Homework XP
- Other approved XP sources
- Manual XP adjustments if allowed
- XP history
- XP correction/reversal
- Current XP calculation
- XP thresholds
- Level interaction
- Monthly reset behavior if applicable
- Historical XP preservation
- Duplicate prevention
- Idempotency

XP must remain separate from points unless a specific business rule explicitly connects them.


SECTION 7 — Level System

Define the complete level architecture.

Include:
- Level definitions
- Level numbering
- XP thresholds
- Level progression
- Level calculation
- Monthly level system
- Level reset rules
- Level history
- Promotion
- Demotion if applicable
- Boundary conditions
- Same-XP tie handling
- Historical level records
- Current level calculation
- Level display requirements

Levels must be deterministic and reproducible from authoritative data.


SECTION 8 — Monthly Gamification Cycle

Define the monthly gamification lifecycle.

Include:
- Monthly period definition
- Start of month
- End of month
- Monthly XP handling
- Monthly level calculation
- Monthly rankings
- Monthly badges
- Monthly achievements
- Monthly statistics
- Previous-month history
- New-month initialization
- Recalculation
- Late corrections
- Time-zone handling
- Year/month boundaries

The monthly cycle must not destroy historical records.


SECTION 9 — Rankings & Leaderboards

Define ranking and leaderboard logic.

Include:
- Group leaderboard
- Student ranking
- Monthly ranking
- Current ranking
- Ranking calculation
- Ranking sort order
- Tie-breaking rules
- Equal-score behavior
- Ranking position changes
- Historical rankings
- Teacher-only visibility
- Group-level scope
- Privacy considerations
- Empty ranking states

Rankings must be derived from authoritative gamification data.


SECTION 10 — Badges

Define the badge system.

Include:
- Badge definitions
- Badge categories
- Badge requirements
- Badge eligibility
- Automatic awarding
- Manual awarding if explicitly allowed
- Duplicate prevention
- Badge history
- Badge rarity where applicable
- Badge visibility
- Group/student display
- Revocation/correction behavior
- Historical preservation

Badges must have deterministic criteria and must not depend on arbitrary UI behavior.


SECTION 11 — Achievements & Achievement Progress

Define the achievement system.

Include:
- Achievement definitions
- Achievement criteria
- Progress tracking
- Automatic evaluation
- Completion state
- Completion timestamp
- Re-evaluation
- Historical progress
- Duplicate completion prevention
- Achievement rewards
- Achievement categories
- Student progress display
- Group statistics

Achievement logic must be compatible with DATABASE.md and UI_GUIDE.md.


SECTION 12 — Streaks

Define streak mechanics.

Include:
- Streak definition
- Qualifying events
- Daily/lesson-based logic where applicable
- Attendance streaks
- Homework streaks if explicitly supported
- Streak start
- Streak continuation
- Streak break
- Streak correction
- Monthly boundaries
- Historical streaks
- Current streak
- Longest streak
- Time-zone rules
- Duplicate-event prevention

Streaks must use clearly defined qualifying events and must not be inferred inconsistently by different parts of the application.


SECTION 13 — Rewards & Recognition

Define the rewards system.

Include:
- Reward definitions
- Reward categories
- Eligibility
- Automatic rewards
- Teacher-awarded rewards if allowed
- Reward history
- Redemption status if applicable
- Duplicate prevention
- Reward visibility
- Group-level reporting
- Student-level history
- Relationship with points, XP, badges, and achievements

Rewards must not introduce financial or external obligations unless explicitly approved by project requirements.


SECTION 14 — Gamification Configuration & Rules Engine

Define how gamification rules are configured and maintained.

Include:
- Point rules
- XP rules
- Level thresholds
- Badge rules
- Achievement rules
- Streak rules
- Reward rules
- Rule activation/deactivation
- Rule versioning
- Effective dates
- Configuration ownership
- Default system configuration
- Teacher-specific configuration only where explicitly supported
- Validation
- Conflict prevention

Configuration must be centralized so the application does not contain duplicated hardcoded business rules.


SECTION 15 — Gamification Transactions, Idempotency & Corrections

Define transaction integrity.

Include:
- Point transactions
- XP transactions
- Gamification events
- Event identifiers
- Idempotency keys
- Duplicate prevention
- Transaction atomicity
- Reversal transactions
- Corrections
- Recalculation
- Failed operation recovery
- Audit trail
- Source event references
- Transaction timestamps
- Historical immutability where appropriate

A correction should preserve history rather than silently overwriting authoritative transactions.


SECTION 16 — Dynamic Journal Integration

Define how gamification integrates with the Dynamic Journal Core.

Include:
- Attendance action → gamification event
- Homework action → gamification event
- Inline point updates where allowed
- XP updates
- Immediate UI feedback
- Optimistic UI safety
- Transaction confirmation
- Error rollback
- Duplicate-event prevention
- Journal refresh behavior
- Historical consistency
- Teacher correction workflow
- Performance requirements

The Journal must remain fast while gamification processing remains accurate and transactional.


SECTION 17 — Analytics, Statistics & Reporting

Define gamification analytics.

Include:
- Current points
- Current XP
- Level
- Monthly level
- Ranking
- Badges
- Achievements
- Streaks
- Rewards
- Group statistics
- Student statistics
- Monthly statistics
- Trends
- Participation metrics
- Progress indicators
- Report-ready data

Derived analytics must be reproducible from authoritative records and remain consistent with DATABASE.md and UI_GUIDE.md.


SECTION 18 — Gamification UI, Notifications & Teacher Experience

Define how gamification appears in the UI.

Include:
- Student progress
- Group leaderboard
- Points display
- XP display
- Level display
- Badge display
- Achievement progress
- Streak display
- Reward display
- Notifications
- Success feedback
- Correction feedback
- Loading states
- Empty states
- Error states
- Permission-aware behavior

UI behavior must follow UI_GUIDE.md and must never contain conflicting gamification rules.


SECTION 19 — Security, Permissions, Auditability & Data Integrity

Define security and integrity requirements for gamification data.

Include:
- Teacher ownership
- Group-level isolation
- Row Level Security compatibility
- Authorized teacher actions
- No student login
- Secure manual adjustments
- Audit logs
- Activity logs
- Historical preservation
- Input validation
- Constraint validation
- Unauthorized modification prevention
- Secure server-side operations
- Protection against duplicate requests
- No trust in frontend-only authorization

All security requirements must remain consistent with DATABASE.md.


SECTION 20 — Performance, Testing, Governance & Final Acceptance

Define final gamification implementation standards.

Performance:
- Efficient transaction processing
- Efficient ranking queries
- Efficient monthly calculations
- Pagination where necessary
- Avoid unnecessary recalculation
- Avoid N+1 queries
- Optimize journal-triggered operations
- Appropriate indexes
- Lightweight architecture

Testing:
- Point calculation tests
- XP calculation tests
- Attendance rule tests
- Homework rule tests
- Level threshold tests
- Monthly cycle tests
- Ranking tie tests
- Badge eligibility tests
- Achievement tests
- Streak tests
- Reward tests
- Correction/reversal tests
- Idempotency tests
- RLS/security tests
- Realistic teacher workflow tests

Governance:
- Rules must be documented
- Business rules must be version-controlled
- Changes must be migration/configuration controlled where required
- No undocumented production rule changes
- No duplicated conflicting rules
- PROJECT_REQUIREMENTS.md remains the product authority
- DATABASE.md remains the data/persistence authority
- GAMIFICATION.md remains the gamification business-rule authority
- UI_GUIDE.md remains the UI implementation authority

Final acceptance criteria:

The gamification system is complete only when:
- All defined rules are deterministic
- Points are accurate
- XP is accurate
- Levels are accurate
- Monthly cycles are accurate
- Rankings are deterministic
- Badges are correctly awarded
- Achievements are correctly evaluated
- Streaks are correctly calculated
- Rewards are correctly handled
- Corrections preserve history
- Duplicate transactions are prevented
- Teacher ownership is enforced
- RLS requirements are satisfied
- Dynamic Journal integration is reliable
- Analytics are reproducible
- UI behavior is consistent
- Performance is acceptable
- Security is enforced
- Tests cover critical business rules
- The system works in realistic classroom workflows
- No rule conflicts with PROJECT_REQUIREMENTS.md, DATABASE.md, or UI_GUIDE.md


<!--
  Sync Impact Report
  ===================
  Version change: 1.0.0 -> 2.0.0 (Phase IV constitution)

  Modified principles:
  - P3: "Monolithic Architecture" -> "Containerized Kubernetes Architecture"
  - P4: "Technology Stack Compliance" -> expanded with Phase IV stack

  Added sections:
  - P11: Container Image Standards
  - P12: Kubernetes Deployment Standards
  - P13: AIOps Integration
  - P14: Helm Chart Management

  Removed sections: None (P1-P10 retained)

  Templates requiring updates:
  - .specify/templates/plan-template.md ✅ no changes needed (generic)
  - .specify/templates/spec-template.md ✅ no changes needed (generic)
  - .specify/templates/tasks-template.md ✅ no changes needed (generic)

  Deferred items: None
-->

# Project Constitution

**Project Name:** AI-Powered Todo Chatbot (Phase IV: Local Kubernetes Deployment)

**Version:** 2.0.0

**Ratification Date:** 2026-01-22

**Last Amended Date:** 2026-01-29

---

## Preamble

This constitution establishes the foundational principles, technical standards, and governance
rules for the AI-Powered Todo Chatbot project. Phase IV extends the application with local
Kubernetes deployment via Minikube, Docker containerization with multi-stage builds, Helm chart
packaging, and AIOps tooling (Gordon, kubectl-ai, kagent). All Phase III features MUST remain
functional. All development activities, architectural decisions, and implementations MUST adhere
to these principles.

---

## Principles

### P1: AI-Driven Development (AIDD)

**Statement:** 100% of code MUST be generated through AI-driven development using Claude Code.

**Rules:**
- No manual code writing is permitted; all code is generated via AI specifications
- Specifications MUST be refined iteratively until correct output is achieved
- Every code change MUST be traceable to a specification or prompt
- Human developers act as architects and reviewers, not code writers

**Rationale:** AIDD ensures consistency, reduces human error, and demonstrates the viability
of AI-assisted software development at scale.

---

### P2: Spec-Driven Development

**Statement:** All features MUST be developed using Spec-Kit Plus methodology with formal
specifications preceding implementation.

**Rules:**
- Every feature MUST have a spec.md before implementation begins
- Plans (plan.md) MUST document architectural decisions
- Tasks (tasks.md) MUST be testable and traceable to specifications
- Prompt History Records (PHR) MUST capture all significant interactions
- Architectural Decision Records (ADR) MUST document significant technical choices

**Rationale:** Spec-driven development creates auditable, reproducible, and maintainable
software while enabling AI agents to operate effectively within defined boundaries.

---

### P3: Containerized Kubernetes Architecture

**Statement:** The application MUST be containerized with Docker and deployed to a local
Kubernetes cluster via Minikube.

**Rules:**
- Single repository with `/frontend`, `/backend`, and `/k8s` (or Helm chart) folders
- Three main deployments: Frontend (Next.js), Backend (FastAPI + MCP server),
  Database (Neon external connection or PostgreSQL pod)
- Services MUST provide internal communication between pods
- ConfigMaps MUST store non-sensitive configuration
- Secrets MUST store sensitive data (API keys, JWT secret, DB credentials)
- Ingress MUST provide external access to the application
- Helm chart MUST package all Kubernetes resources
- All Phase III features MUST work identically in containerized deployment

**Rationale:** Kubernetes deployment demonstrates production-readiness and enables zero
downtime deployments, scaling, and operational excellence.

---

### P4: Technology Stack Compliance

**Statement:** All implementations MUST use the prescribed technology stack without deviation.

**Frontend Stack:**
- Next.js 16+ with App Router (required)
- Tailwind CSS + custom CSS for styling
- TypeScript for type safety

**Backend Stack:**
- Python FastAPI for API services
- SQLModel as ORM layer
- Neon Serverless PostgreSQL for persistence
- OpenAI Agents SDK for AI capabilities
- Official MCP SDK (Python) for tool integration

**Deployment Stack (Phase IV):**
- Docker with multi-stage builds for containerization
- Docker AI (Gordon) via Docker Desktop 4.53+
- Kubernetes via Minikube (minimum 4GB RAM, 2 CPUs)
- Helm Charts for package management
- AIOps: kubectl-ai, kagent

**Rules:**
- No alternative frameworks or libraries without ADR approval
- Version constraints MUST be respected
- All dependencies MUST be explicitly declared

**Rationale:** Stack consistency ensures predictable behavior, simplified debugging, and
cohesive AI code generation.

---

### P5: Authentication & Security

**Statement:** All user interactions MUST be authenticated and all API endpoints MUST be
secured with JWT tokens.

**Authentication Requirements:**
- Better Auth integration with email verification
- Signup requires: email, name, password
- Email verification system (accept fake emails, verify format)
- Verified email stored in Neon DB for reminder notifications
- JWT token-based API security for all protected endpoints

**Security Rules:**
- MUST prevent SQL injection via parameterized queries (SQLModel)
- MUST validate and sanitize all user inputs
- MUST use HTTPS in production
- Secrets MUST be stored in environment variables, never in code
- JWT tokens MUST have appropriate expiration times
- Kubernetes Secrets MUST be used for sensitive data in cluster

**Rationale:** Security is non-negotiable; authentication protects user data and enables
personalized features like reminders.

---

### P6: AI Chat Interface Standards

**Statement:** The AI assistant MUST be implemented as a separate page with persistent
conversation history.

**Interface Requirements:**
- Dedicated AI Assistant page (not embedded in dashboard)
- OpenAI ChatKit integration with Agents SDK
- Left side: Active chat interface
- Right sidebar: Chat history from Neon DB
- Conversation state persisted across sessions in database

**Technical Requirements:**
- Stateless backend architecture
- Database-persisted conversation state
- Real-time message updates
- Graceful error handling for AI failures

**Rationale:** Separation of chat from dashboard improves UX focus; persistence enables
continuity and context retention.

---

### P7: MCP Server Implementation

**Statement:** Exactly 5 MCP tools MUST be implemented using the official MCP SDK for task
operations.

**Required Tools:**
1. `add_task` - Create task with title, description, reminder, date, day
2. `delete_task` - Remove task by ID
3. `update_task` - Modify existing task details
4. `mark_as_completed_task` - Toggle task completion status
5. `view_task` - Retrieve tasks with filtering support

**Rules:**
- All tools MUST be implemented using official MCP SDK (Python)
- Tools MUST validate inputs before database operations
- Tools MUST return structured responses for AI consumption
- Error handling MUST provide actionable feedback

**Rationale:** MCP tools enable the AI agent to perform task management operations on behalf
of users, creating a natural language interface.

---

### P8: Visual Design Excellence

**Statement:** The application MUST deliver a visually stunning dark theme with purple
accents and exceptional animations.

**Design Requirements:**
- Black and purple color theme throughout
- Landing page: Left-aligned header text, right side high-quality image
- High-quality thematic images throughout the application
- Exceptional CSS animations on landing page
- Dashboard: Purple accents complementing black theme
- Smooth, complementary animations on dashboard

**Rules:**
- Animations MUST not impact performance (60fps target)
- Images MUST be optimized for web delivery
- Design MUST maintain visual hierarchy and readability
- Animations MUST enhance UX, not distract

**Rationale:** Visual excellence differentiates the product and demonstrates attention to
detail in AI-generated applications.

---

### P9: Task Reminder System

**Statement:** The application MUST support email-based task reminders with user-defined
scheduling.

**Requirements:**
- Task model MUST include reminder fields: date, day, time
- UI MUST provide intuitive reminder input controls
- Backend service MUST check and trigger reminders
- Reminders MUST be sent via email to users verified address

**Rules:**
- Reminder metadata MUST be stored in the task model
- Backend MUST have a reliable scheduler for reminder checks
- Failed reminder attempts MUST be logged and retried
- Users MUST be able to modify or cancel reminders

**Rationale:** Reminders increase task completion rates and provide value beyond basic
todo functionality.

---

### P10: Quality & Accessibility

**Statement:** All code MUST meet quality standards and accessibility requirements.

**Quality Standards:**
- Clean, maintainable code structure
- Comprehensive error handling with user-friendly messages
- Type safety via TypeScript (frontend) and type hints (backend)
- No dead code or unused dependencies

**Accessibility Requirements:**
- WCAG 2.1 AA compliance required
- Keyboard navigation support
- Screen reader compatibility
- Sufficient color contrast ratios
- Focus indicators on interactive elements

**Responsive Design:**
- Mobile-first approach
- Breakpoints: mobile, tablet, desktop
- Touch-friendly targets (minimum 44x44px)

**Rationale:** Quality and accessibility ensure the application serves all users effectively
and maintains long-term maintainability.

---

### P11: Container Image Standards

**Statement:** All Docker images MUST use multi-stage builds and meet size and security
constraints.

**Rules:**
- Frontend image MUST be < 500MB
- Backend image MUST be < 300MB
- Multi-stage builds MUST separate build dependencies from runtime
- Images MUST NOT contain secrets, credentials, or `.env` files
- Images MUST use non-root users for runtime
- `.dockerignore` MUST exclude unnecessary files (node_modules, .git, etc.)
- Each image MUST include a health check endpoint

**Rationale:** Optimized images reduce deployment time, minimize attack surface, and
improve resource utilization in the cluster.

---

### P12: Kubernetes Deployment Standards

**Statement:** All Kubernetes resources MUST follow production-ready deployment patterns.

**Rules:**
- Every deployment MUST define liveness and readiness probes
- Every deployment MUST specify CPU and memory resource requests and limits
- Rolling update strategy MUST be used (maxSurge: 1, maxUnavailable: 0)
  to enable zero downtime deployments
- Horizontal Pod Autoscaler MUST be configured (ready to enable)
- Graceful shutdown MUST be handled (preStop hooks, SIGTERM handling)
- All pods MUST log to stdout/stderr for cluster log aggregation
- ConfigMaps MUST be used for non-sensitive environment configuration
- Secrets MUST be used for API keys, JWT secrets, and database credentials

**Infrastructure Requirements:**
- Minikube cluster with minimum 4GB RAM, 2 CPUs
- MUST work on Windows, macOS, and Linux
- All kubectl commands MUST be documented for manual fallback

**Rationale:** Production-ready patterns ensure reliability, observability, and the ability
to perform zero downtime deployments.

---

### P13: AIOps Integration

**Statement:** AI-powered operations tools MUST be integrated for intelligent cluster
management.

**Required Tools:**
- Docker AI (Gordon) for intelligent Docker image building and troubleshooting
- kubectl-ai for natural language Kubernetes operations
- kagent for cluster analysis and optimization recommendations

**Rules:**
- AIOps tools MUST be used where applicable for troubleshooting
- Manual kubectl commands MUST be documented as fallback
- AI-generated recommendations MUST be reviewed before applying
- All AIOps interactions SHOULD be recorded in PHRs when significant

**Rationale:** AIOps tools reduce operational complexity and demonstrate AI-driven
infrastructure management alongside AI-driven development.

---

### P14: Helm Chart Management

**Statement:** A Helm chart MUST package all Kubernetes resources for the application.

**Rules:**
- Chart MUST include templates for all deployments, services, ConfigMaps, Secrets,
  and Ingress
- Values file MUST externalize all configurable parameters
- Chart MUST support environment-specific value overrides
- Chart MUST include NOTES.txt with post-install instructions
- Chart version MUST follow semantic versioning

**Rationale:** Helm charts provide reproducible, version-controlled deployment packaging
that simplifies installation and upgrades.

---

## Governance

### Amendment Procedure

1. Propose amendment via ADR with rationale
2. Review impact on existing specifications and implementations
3. Update constitution with version increment
4. Propagate changes to dependent templates
5. Document in Sync Impact Report

### Versioning Policy

Constitution follows semantic versioning:
- **MAJOR (X.0.0):** Backward-incompatible principle changes or removals
- **MINOR (X.Y.0):** New principles or significant expansions
- **PATCH (X.Y.Z):** Clarifications, wording fixes, non-semantic updates

### Compliance Review

- All specifications MUST reference relevant principles
- Code reviews MUST verify principle adherence
- Deviations require explicit ADR with justification
- Quarterly reviews assess principle effectiveness

---

## Constraints

### Phase IV Scope

The following are IN SCOPE for Phase IV:
- Docker containerization with multi-stage builds
- Kubernetes deployment via Minikube
- Helm chart packaging
- AIOps tool integration (Gordon, kubectl-ai, kagent)
- Health checks, resource limits, rolling updates
- Zero downtime deployment capability

### Explicit Exclusions

The following are OUT OF SCOPE:
- Cloud-hosted Kubernetes (EKS, GKE, AKS)
- CI/CD pipeline automation beyond local deployment
- Service mesh (Istio, Linkerd)
- External monitoring stacks (Prometheus, Grafana) beyond basic probes
- Multi-cluster or federation

### Development Constraints

- All code generated via Claude Code (no manual coding)
- Specifications MUST be refined until correct output
- No external API integrations beyond prescribed stack
- No premium/paid third-party services without approval
- All Phase III features MUST pass verification before Phase IV work begins

---

## Appendix A: File Structure

```
/
├── frontend/           # Next.js application
│   └── Dockerfile      # Multi-stage build
├── backend/            # FastAPI application
│   └── Dockerfile      # Multi-stage build
├── k8s/                # Raw Kubernetes manifests (optional)
├── helm/               # Helm chart
│   └── obsidianlist/
│       ├── Chart.yaml
│       ├── values.yaml
│       └── templates/
├── specs/              # Feature specifications
│   └── <feature>/
│       ├── spec.md
│       ├── plan.md
│       └── tasks.md
├── history/
│   ├── prompts/        # PHR records
│   │   ├── constitution/
│   │   ├── general/
│   │   └── <feature>/
│   └── adr/            # Architecture Decision Records
├── .specify/
│   ├── memory/
│   │   └── constitution.md
│   └── templates/
└── .env                # Environment variables (NOT in images)
```

---

## Appendix B: Success Metrics

| Metric | Target |
|--------|--------|
| AI Code Generation | 100% |
| WCAG Compliance | AA Level |
| Animation Performance | 60fps |
| API Response Time | < 500ms p95 |
| Test Coverage | > 80% |
| Frontend Image Size | < 500MB |
| Backend Image Size | < 300MB |
| Pod Startup Time | < 30s |
| Zero Downtime Deploy | Yes |
| Health Check Response | < 5s |

---

*This constitution is the authoritative source for project governance. All team members,
AI agents, and automated systems MUST operate within these boundaries.*

# addendum-platform0.md

# Platform0 Addendum: Security-by-Default Implementation Patterns

This addendum demonstrates how Platform0, a Docker-first developer platform starter kit, implements PCI DSS defensive frameworks as built-in architectural patterns rather than retrofitted compliance measures.

## Platform0 Philosophy

Platform0 operates on the principle that security controls should be invisible to developers while being comprehensive and auditable for security teams. The platform provides:

- **Security by default**: All services start with authentication, audit logging, and operational endpoints configured
- **Contract-driven compliance**: CI pipelines enforce security policies (P0/P1/P2) before deployment
- **Evidence generation**: SBOM, vulnerability scans, and redacted audit logs produced automatically
- **Stack agnostic**: Python and Go reference implementations demonstrate portability

## Framework Implementation Patterns

### Authentication & Authorization (PCI DSS 8.x)

**Platform0 Implementation:**

```yaml
# docker-compose.yml - Authentication enforced at platform level
services:
  api:
    environment:
      - AUTH_MODE=static  # never 'none' in production (P0-001)
      - AUTH_TOKENS_FILE=/run/secrets/auth_tokens
    secrets:
      - auth_tokens
```

**Policy Enforcement:**

- P0-001: AUTH_MODE=none prohibited in production (CI gate)
- All privileged actions require authenticated identity
- Audit events include authenticated user context

**Benefit:** Developers cannot accidentally deploy unauthenticated APIs. Authentication is platform-level, not service-level responsibility.

### Audit Logging for Insider Threats (PCI DSS 10.x)

**Platform0 Implementation:**

```python
# Python SDK pattern - automatic audit emission
from platform0 import audit

@audit.privileged_action(action="state.transition")
def transition_state(context: RequestContext, machine_id: str, event: str):
    # Business logic here
    # Audit events emitted automatically:
    # - Request timestamp, authenticated user
    # - Action attempted (success/denied)
    # - Redacted sensitive data
    pass
```

**Policy Enforcement:**

- P0-002: Privileged actions must emit audit events (CI validation)
- P0-003: Sensitive data must be redacted (contract tests validate)
- Audit events persist to immutable storage (NATS JetStream)

**Benefit:** Audit logging is decorator-driven. Developers mark privileged operations; platform handles event structure, emission, and storage.

### Data Encryption (PCI DSS 3.x, 4.x)

**Platform0 Implementation:**

```yaml
# All inter-service communication over TLS
services:
  api:
    networks:
      - backend
  database:
    volumes:
      - db_data:/var/lib/postgresql/data  # encrypted volume
    environment:
      - POSTGRES_SSL_MODE=require
```

**Standards:**

- TLS 1.2+ required for all network communication
- Database connections require SSL
- Secrets managed through Docker secrets or external KMS
- MinIO storage configured with server-side encryption

**Benefit:** Encryption is infrastructure configuration, not application code. Developers work with plaintext; platform handles encryption transparently.

### System Hardening (PCI DSS 2.x)

**Platform0 Implementation:**

```docker
# Reference Dockerfile with hardening built-in
FROM python:3.11-slim

# Non-root user (security baseline)
RUN useradd -m -u 1000 appuser
USER appuser

# Minimal attack surface - no compilers, no shell tools
# Only runtime dependencies installed

EXPOSE 8080
HEALTHCHECK CMD curl -f [http://localhost:8080/healthz](http://localhost:8080/healthz) || exit 1
```

**Standards:**

- Non-root containers by default
- Minimal base images (slim, alpine, or distroless)
- No unnecessary packages or development tools in production images
- Health checks and readiness probes standard

**Benefit:** Hardening patterns baked into reference Dockerfiles. Developers copy secure-by-default templates.

### Vulnerability Management (PCI DSS 6.x)

**Platform0 CI Integration:**

```yaml
# .github/workflows/contract-harness.yml
- name: SBOM Generation
  run: |
    syft sut:dev -o spdx-json > sbom.spdx.json
    
- name: Vulnerability Scan
  run: |
    grype sbom:./sbom.spdx.json --fail-on high
    
- name: Upload Evidence
  run: |
    # Evidence package: SBOM + scan results + test results
    tar czf evidence-$ github.sha .tar.gz sbom.spdx.json grype-report.json
```

**Policy Enforcement:**

- P1-001: SBOM required for all production deployments
- P1-002: High/Critical vulnerabilities block deployment
- P0-004: Emergency patches deploy within SLA (documented procedure)

**Benefit:** Vulnerability scanning integrated into CI. Developers receive immediate feedback; security team gets evidence packages automatically.

### Incident Response & Monitoring (PCI DSS 10.x, 12.10)

**Platform0 Observability Stack:**

```yaml
services:
  # OpenTelemetry for traces, metrics, logs
  otel-collector:
    image: otel/opentelemetry-collector
    
  # Prometheus for metrics
  prometheus:
    image: prom/prometheus
    
  # Jaeger for distributed tracing
  jaeger:
    image: jaegertracing/all-in-one
    
  # Grafana for visualization
  grafana:
    image: grafana/grafana
```

**Standard Endpoints:**

- `/healthz` - Liveness probe
- `/readyz` - Readiness probe
- `/metrics` - Prometheus metrics
- `/version` - Service version and build info

**Benefit:** Observability is platform infrastructure. Services emit structured logs and metrics; centralized systems aggregate and alert.

### Policy-as-Code (PCI DSS 12.x)

**Platform0 Policy Gates:**

```bash
#!/bin/bash
# [policy-check.sh](http://policy-check.sh) - CI enforcement

# P0 policies: MUST pass for any deployment
if grep -q 'AUTH_MODE=none' [docker-compose.prod](http://docker-compose.prod).yml; then
    echo "FAIL: P0-001 - AUTH_MODE=none prohibited in production"
    exit 1
fi

# P1 policies: MUST pass for production branches
if [[ "$BRANCH" == "main" ]] && [ ! -f sbom.spdx.json ]; then
    echo "FAIL: P1-001 - SBOM required for production deployment"
    exit 1
fi

# P2 policies: WARNING only (technical debt tracked)
if ! grep -q 'rate_limit' nginx.conf; then
    echo "WARN: P2-001 - Rate limiting recommended"
fi
```

**Policy Levels:**

- **P0**: Security fundamentals (auth, audit, redaction) - hard fail
- **P1**: Production requirements (SBOM, scans, tests) - fail on release branches
- **P2**: Best practices (rate limiting, caching) - warning only

**Benefit:** Security policies enforced by CI, not manual review. Shift-left approach catches issues in development.

## Implementation Timeline with Platform0

Using Platform0 significantly accelerates PCI DSS implementation:

**Traditional Approach:**

- 6-12 months to build secure API infrastructure
- 3-6 months additional for audit logging, monitoring, compliance
- Significant security expertise required

**Platform0 Approach:**

- **Week 1**: Deploy Platform0 stack (Docker Compose)
- **Week 2-3**: Implement business logic using SDK patterns
- **Week 4**: CI pipeline with policy gates
- **Month 2-3**: Production deployment with evidence generation
- **Ongoing**: Continuous compliance through automated checks

## Real-World Example: State Machine API

Platform0 includes a reference State Machine API demonstrating all defensive frameworks:

**Authentication:** All state transitions require authenticated user

**Authorization:** Role-based access to machines (owner vs. operator)

**Audit Logging:** Every state change emits audit event with before/after states

**Idempotency:** Duplicate requests return cached response (prevents double-processing)

**Encryption:** All data at rest encrypted, TLS in transit

**Monitoring:** Metrics for transition rates, error rates, latency

**Hardening:** Non-root container, minimal image, health checks

**Vulnerability Management:** SBOM generated, scanned, and archived per release

**Policy Enforcement:** CI gates prevent deployment of non-compliant code

**Testing:** Contract tests validate security properties (auth required, audit emitted, idempotency works)

## Platform0 as PCI DSS Accelerator

Platform0 implements 8 of the 12 PCI DSS domains as platform capabilities:

1. ✅ **Network Security** - Segmentation via Docker networks, TLS everywhere
2. ✅ **Secure Configuration** - Hardened Dockerfiles, non-root containers
3. ✅ **Data Protection** - Encryption at rest and in transit
4. ✅ **Vulnerability Management** - SBOM, scanning, CI gates
5. ❌ **Access Control** - Application-specific (framework patterns provided)
6. ✅ **Monitoring & Testing** - OpenTelemetry, Prometheus, Grafana, Jaeger
7. ❌ **Security Policy** - Organization-specific (templates provided)
8. ✅ **Software Security** - Secure SDLC, contract tests, policy-as-code

The remaining domains (access control, security policy, incident response, physical security) require organization-specific implementation, but Platform0 provides reference patterns and documentation.

## Getting Started with Platform0

Platform0 is open source and designed for rapid adoption:

**Repository:** [`github.com/yourorg/platform0`](http://github.com/yourorg/platform0) (example - update with actual URL when published)

**Quick Start:**

```bash
# Clone and start local environment
git clone [https://github.com/yourorg/platform0](https://github.com/yourorg/platform0)
cd platform0
docker compose up

# Access services
# API: [http://localhost:8080](http://localhost:8080)
# Grafana: [http://localhost:3000](http://localhost:3000)
# Jaeger: [http://localhost:16686](http://localhost:16686)
# Prometheus: [http://localhost:9090](http://localhost:9090)
```

**Documentation:**

- Quick Start Guide: Prototype to production in 4 weeks
- Architecture Standards: Manifesto and compliance hooks
- Complete Test Scripts: Copy-paste contract testing
- Deployment Guides: Cloud Run, Kubernetes, ECS

## Conclusion

Platform0 demonstrates that PCI DSS compliance doesn't require sacrificing developer velocity. By implementing security as platform infrastructure rather than application responsibility, organizations achieve:

- **Faster time-to-market**: Secure defaults eliminate security rework
- **Lower security debt**: Policy-as-code prevents non-compliant deployments
- **Reduced risk**: Automated evidence generation proves compliance continuously
- **Developer focus**: Engineers build features, not security infrastructure

The defensive frameworks in this document describe *what* to build. Platform0 provides *how* to build it, with production-ready patterns and CI/CD integration that makes security invisible to developers and transparent to auditors.
# CrowdShield Data Privacy & Ethics

## Purpose

CrowdShield is intended to support public safety while minimizing unnecessary collection of personal information.

## Current prototype

The current repository primarily uses simulated crowd data and application events. It does **not** process a live CCTV feed.

### Data used

- Simulated crowd metrics
- Scenario state
- Operational events
- Operator actions
- Timestamps and action outcomes
- Incident-report information entered through the prototype UI

### Not collected by default

- Names or identity documents
- Facial recognition data
- Raw CCTV/video footage
- Individual-level movement histories
- Identifiable geolocation histories

## Public imagery and future CCTV integration

If connected to CCTV or other imagery, privacy should be built into the pipeline:

```text
Camera
  |
  v
Local/edge processing
  |
  v
Aggregate crowd features
  |
  +--> discard unnecessary raw imagery
  |
  v
Risk analysis
```

Preferred outputs are crowd-level features such as density, occupancy, movement speed, flow conflict and bottleneck level. Face recognition and persistent individual tracking should not be required.

## Data minimization

Collect only information needed to detect crowd conditions, support operator decisions, audit safety actions and evaluate system performance.

Prefer aggregated metrics and event labels over raw personal content.

## Voice commands

Voice input is potentially sensitive. Raw transcripts should not be retained unless there is a documented operational reason, lawful basis, access control, encryption and retention policy.

## Incident reports

Collect only information needed to understand and respond to an incident. Production deployments should provide clear notice about data handling.

## Retention

The current prototype uses in-memory backend storage.

Before production deployment, define retention periods, deletion procedures, legal requirements and authorized access. Retention should be as short as practical.

## Security

Production deployment should use HTTPS/TLS, secure secret management, strong authentication, role-based access control, encrypted storage, audit logs, rate limiting, input validation and regular security review.

The current backend demonstrates several of these patterns but is not a production security system.

## Human oversight

CrowdShield is a decision-support system. High-impact interventions should remain subject to authorized human review. Operators should be able to reject or override recommendations.

## Fairness and non-discrimination

Risk analysis should be based on crowd-safety signals rather than identity characteristics. The system should not be used to profile individuals, discriminate against groups, infer sensitive attributes or perform unnecessary surveillance.

## Fail-safe behavior

If sensors, connectivity or prediction confidence become unreliable, the system should clearly indicate degraded status rather than presenting uncertain results as facts.

## Governance

Before real-world deployment, the responsible authority should complete a privacy and legal review covering applicable Indian data-protection requirements, CCTV/public-imagery rules, data sharing, retention, access control, incident response and vendor/cloud responsibilities.

## Current limitations

This document describes design principles and future safeguards. It is not a legal compliance certification.

## Future privacy improvements

- Edge-based video analytics
- No face recognition by default
- Short-lived or zero-retention raw imagery
- Aggregated feature transmission
- Role-based access
- Privacy impact assessment
- Formal retention/deletion workflows

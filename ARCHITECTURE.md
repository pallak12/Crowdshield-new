# CrowdShield Architecture

## 1. System Overview

CrowdShield is a web-based crowd-safety decision-support prototype. The current implementation combines a browser-based simulation and dashboard with an optional Node.js/Express backend stub.

```text
Crowd simulation / operator input
        |
        v
Metrics + scenario state
        |
        v
Risk status + rule-based recommendations
        |
        +-------------------+
        |                   |
        v                   v
Dashboard / mobile UI   Operator actions
                            |
                            v
                      Backend client
                            |
                            v
                     Express API stub
```

## 2. Frontend Components

- `index.html` — main dashboard, controls, reporting interface and mobile-friendly views.
- `styles.css` — responsive visual styling and dashboard layout.
- `config.js` — application constants, thresholds, simulation settings and optional backend configuration.
- `app.js` — initialization, simulation loops, metrics, risk status and recommendation logic.
- `state.js` — central application state.
- `ui-updates.js` — dashboard metrics, alerts, logs, recommendations and mobile displays.
- `events.js` — UI, scenario, voice and incident-report interactions.
- `voice-commands.js` — supported operator command parsing and action mapping.
- `canvas-renderer.js` — digital-twin-style venue and crowd visualization.
- `particle-system.js` — crowd particle simulation.
- `backend-client.js` — optional API calls for logs, actions and recommendations.

### Important implementation note

The current `calculateAIRecommendations()` function is a **rule-based decision layer**. It should not be described as a trained ML model.

## 3. Backend

The `backend/` directory contains a minimal Express backend stub with:

- Helmet security headers
- CORS origin restrictions
- Rate limiting
- Bearer-token authorization
- Request validation
- Environment-based configuration

It is a prototype integration layer, not a production event-processing platform.

## 4. API

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/log` | Receive structured event/log data |
| POST | `/api/action` | Receive whitelisted operator action requests |
| GET | `/api/recommendations` | Return recommendation payloads |

Prototype event/action data is stored in memory.

## 5. Risk and Recommendation Logic

The current risk layer uses simulated crowd metrics, thresholds and scenario conditions.

Examples include:

- High stampede-likelihood metric → recommend security deployment
- Blockage scenario → recommend closing a gate
- Panic scenario → recommend broadcast/evacuation
- Surge scenario → recommend redirecting crowd flow

This is appropriate for a competition prototype and simulation, but it is not equivalent to a trained predictive ML model.

## 6. Data Flow

```text
Simulation / user input
        |
        v
app.js + state.js
        |
        +--> metric calculation
        +--> risk status
        +--> recommendation rules
        |
        v
ui-updates.js
        |
        +--> dashboard
        +--> mobile view
        +--> alerts
        +--> recommendations

Operator action
        |
        v
voice-commands.js / events.js
        |
        v
backend-client.js
        |
        v
POST /api/action or POST /api/log
        |
        v
Express backend stub
```

## 7. Third-Party APIs / Libraries

Frontend:
- Canvas API
- Browser Web Speech API
- `fetch`
- Lucide icons via CDN

Backend:
- Express
- Helmet
- CORS
- express-rate-limit
- dotenv

## 8. Security

The prototype uses bearer-token authorization, configured CORS origins, rate limiting, input validation, environment variables for secrets, and human confirmation for operational actions.

Real deployment would additionally require identity management, role-based access control, encrypted storage, audit infrastructure, secret rotation and monitoring.

## 9. Privacy Architecture

The current prototype does not ingest live CCTV imagery.

For future real deployment:

```text
CCTV / sensors
      |
      v
Edge processing
      |
      v
Crowd-level features only
(density, velocity, flow conflict, occupancy)
      |
      +----> discard unnecessary raw/identifiable imagery
      |
      v
Risk prediction service
      |
      v
Operator dashboard
```

The system should avoid face recognition and unnecessary individual tracking.

## 10. Mobile / Citizen Interface

The repository includes a mobile-friendly UI and incident-reporting flow. A production citizen application would additionally require authenticated APIs, reliable notifications, location-consent controls and resilient connectivity.

## 11. Scalability Path

A production architecture could replace the prototype backend with persistent storage, an event/message queue, real-time updates, edge inference nodes, cloud/district deployment, horizontal API scaling and centralized observability.

These are future deployment components, not claims about the current prototype.

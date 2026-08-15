# CrowdShield

## AI-Assisted Early Warning & Mitigation Prototype for Crowd Safety

CrowdShield is a web-based prototype for monitoring simulated crowd conditions, identifying elevated-risk situations, and helping operators choose timely interventions. It combines a digital-twin-style venue simulation, crowd metrics, rule-based risk scoring, operator recommendations, voice commands, incident reporting, and a security-focused backend stub.

> **Prototype status:** The current system is a functional simulation and decision-support prototype. It does not yet perform live CCTV/video inference or use a trained machine-learning model for stampede prediction.

## Problem

Large public gatherings can develop dangerous congestion quickly. CrowdShield explores a proactive approach: monitor crowd conditions continuously, identify abnormal patterns, surface risk early, and provide actionable recommendations to human operators.

## What the prototype demonstrates

- Digital-twin-style venue visualization with moving crowd particles
- Crowd density and movement metrics
- Risk status and stampede-likelihood indicators
- Simulated blockage, panic and surge scenarios
- Operator recommendations for security deployment, gate control, evacuation and crowd redirection
- Voice-driven operator commands
- Citizen/mobile-friendly incident reporting UI
- Backend logging and action-request integration
- Security controls including bearer-token authorization, CORS and rate limiting
- Privacy-by-design documentation and human-in-the-loop operation

## Architecture

```text
Operator / Citizen UI
        |
        v
Frontend modules
(state, events, simulation, UI, voice)
        |
        v
Risk & recommendation logic
        |
        +----------------------+
        |                      |
        v                      v
Dashboard / mobile UI    backend-client.js
                               |
                               v
                         Express backend
                               |
                    +----------+----------+
                    |                     |
                 /api/log             /api/action
                    |                     |
                    +----------+----------+
                               |
                        in-memory prototype storage
```

See [ARCHITECTURE.md](ARCHITECTURE.md).

## Tech stack

- HTML5 / CSS3
- Vanilla JavaScript
- Canvas API
- Browser Web Speech API
- Node.js + Express
- Helmet, CORS, express-rate-limit and dotenv

## Run locally

### Frontend

From the repository root:

```bash
python -m http.server 8000
```

Open `http://localhost:8000`.

### Optional backend

```bash
cd backend
npm install
```

Create `.env` from `.env.example`, set a strong `API_TOKEN`, then:

```bash
npm start
```

Never commit real secrets.

## Important prototype limitations

The current system should not be presented as a production emergency-response platform.

- Crowd data is simulated rather than obtained from live CCTV/sensors.
- Risk scoring and recommendations are implemented through frontend metrics, thresholds and scenario rules; they are not a trained ML prediction model.
- Backend event/action storage is in memory.
- Production deployment would require persistent storage, stronger identity/role management, monitoring, fail-safe controls and validated prediction models.
- Real public-imagery deployment would require a privacy-preserving video-processing pipeline.

## Documentation

- [Architecture](ARCHITECTURE.md)
- [Data Privacy & Ethics](DATA_PRIVACY.md)
- [Deliverables](DELIVERABLES.md)
- [Pitch Deck](PITCH_DECK.md)

## Competition alignment

| Criterion | CrowdShield response |
|---|---|
| Innovation & Originality | Digital-twin-style simulation, scenario-based risk analysis, actionable interventions and voice control |
| Technical Feasibility | Lightweight web stack plus modular Express backend |
| User Friendliness | Operator dashboard, clear risk states, recommendations, voice controls and mobile-friendly UI |
| Data Ethics & Privacy | Data minimization, human review, secure backend pattern and documented safeguards |

## Future direction

1. Add real-time CCTV/edge analytics that outputs crowd-level features without retaining identifiable imagery.
2. Train and validate an explainable risk-prediction model using density, velocity, flow conflict and bottleneck features.
3. Add persistent encrypted storage and role-based operator accounts.
4. Add resilient offline/low-connectivity operation.
5. Validate recommendations with crowd-safety experts before real-world deployment.

## License

MIT, if the repository includes the corresponding `LICENSE` file.

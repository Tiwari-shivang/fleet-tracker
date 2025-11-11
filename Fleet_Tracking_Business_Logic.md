# Real-Time Fleet Tracking Dashboard - Business Logic

## 1. Business Objectives

### Key Outcomes
- **Higher On-Time Rate**: Real-time monitoring enables proactive delay alerts.
- **Lower Costs**: Reduced idling, optimized routes, and early detection of technical issues.
- **Improved Safety**: Identify risky driver behavior.
- **Faster Exception Handling**: Centralized alerts for quick interventions.
- **Enhanced Planning**: Aggregate metrics for performance analysis.

### Dataset Foundation
- The simulator provides **5 unique trips** across scenarios (long haul, urban, cancelled, etc.).
- Events are timestamped and structured for chronological simulation.
- Over **27 event types** enable deep operational insights.

---

## 2. User-Centric Design

### Personas
| Role | Goal |
|------|------|
| Fleet Manager | High-level view of fleet performance |
| Dispatcher | Monitor real-time issues and resolve quickly |
| Customer Support | Provide accurate ETA & trip history |
| Driver Manager | Analyze safety metrics & patterns |

### Core Workflows
1. **Live Exceptions Panel** – Fuel low, device error, trip delays.
2. **Interactive Map** – Vehicle state, route, and status visualization.
3. **Trip Timeline** – Progress %, dwell times, refuel and violation history.
4. **Fleet Metrics** – Trip completion rates, violation density, fuel efficiency.
5. **Playback Simulation** – Real-time trip replay with speed controls.

---

## 3. Business Logic and Rules

### 3.1 Event Processing
- Process events **chronologically** (sorted by timestamp).
- Remove duplicates via unique `event_id`.
- Compute derived states (progress %, ETA, etc.) as events stream.

### 3.2 Trip State Machine
| From | To | Trigger Event |
|------|----|----------------|
| Planned | In-Progress | `trip_started` |
| In-Progress | Paused | `vehicle_stopped` |
| Paused | Refueling | `refueling_started` |
| Refueling | In-Progress | `refueling_completed` |
| In-Progress | Completed | `trip_completed` |
| Any | Cancelled/Error | `trip_cancelled` / `device_error` |

### 3.3 Calculations
- **Progress %** = (Distance Travelled / Planned Distance) × 100  
- **ETA** = Remaining Distance / Avg Speed ± Delay Factors  
- **Safety Score** = Weighted speed & violation penalties  
- **Signal Health** = Downtime ratio (signal lost duration / trip duration)  
- **Fuel Anomaly** = Unexpected fuel level increase without refuel event  

### 3.4 Alerts
1. Imminent SLA breach (ETA delay).
2. Speeding or repeated violations.
3. Signal lost > 2 minutes.
4. Fuel below threshold (<15%).
5. Battery low (predicted failure before trip end).
6. Device malfunction detected.

---

## 4. Dashboard Architecture

### Layout
- **Left**: Alerts/Exceptions panel.  
- **Center**: Real-time map (clustered markers).  
- **Right**: Trip detail with progress bar & event list.

### Widgets
- Trip Progress Ring (0–100%)
- Fleet Completion Cohorts (50%, 80%, 100%)
- Violation Trends Chart
- Fuel & Battery Gauges
- Playback Controller (1×, 5×, 10×)

---

## 5. Competitive Benchmark

### Compared with Market Leaders
| Competitor | Strength | Gaps You Can Fill |
|-------------|-----------|------------------|
| **Zomato/Blinkit** | Real-time driver map, instant alerts | Lacks explainable ETA & trip playback |
| **Fleetio / Samsara** | Robust analytics | Complex UI for small teams |
| **Your Solution** | Action-first alerts, explainable ETA, simulated playback | Simple, intuitive & transparent |

---

## 6. Technical Overview

- **Data Flow**: Event Stream → State Engine → UI Store → Components  
- **Performance**: Handle 10,000+ events efficiently using virtualized rendering.  
- **Simulation Engine**: Emit events per timestamp interval using `setInterval()` or streaming API.  
- **Responsive Design**: Works seamlessly on mobile and desktop.

---

## 7. Success Metrics

| Metric | Target |
|--------|---------|
| Dashboard Load Time | < 2 seconds |
| Event Stream Delay | < 1 second |
| Alert Detection Accuracy | > 95% |
| Trip Playback Lag | < 200ms |
| User Satisfaction | > 90% (feedback survey) |

---

## 8. Privacy & Compliance
- Mask exact GPS coordinates in public dashboards.
- Store driver and vehicle info securely.
- Access control by role.

---

## 9. Rollout Plan

| Phase | Focus |
|-------|--------|
| Week 1–2 | MVP: Map + Exceptions + Playback |
| Week 3–4 | Alert Engine & Trip Cohorts |
| Week 5–6 | Safety & Fuel Analytics |
| Week 7–8 | Heatmaps & Route Optimization |

---

## 10. End user for this application
The end users of this real-time fleet tracking dashboard will be:

Fleet Managers: Oversee all trips, monitor performance, and identify operational bottlenecks.

Dispatchers / Control Room Staff: Track live vehicle movement, detect issues (fuel, signal, delays), and coordinate quick fixes.

Driver Supervisors: Review driver behavior, safety violations, and efficiency metrics.

Customer Support Teams: Access live trip progress and provide accurate ETAs to clients.

Logistics Analysts / Management: Analyze fleet trends, utilization, and optimize route planning.

## 11. Key Takeaway
A **real-time, action-driven, user-friendly fleet dashboard** improves operational reliability, safety, and decision-making while providing an intuitive and explainable view for all stakeholders.

# VoyageAI Navigator – Requirements

## Project Overview
VoyageAI Navigator is a browser-based, agentic-AI travel planner built for VOYAGEHACK 4.0. Five cooperating agents match destinations, forecast cost, assess safety, estimate carbon and order daily routes. It needs no backend and stores data only in `localStorage`.

## Problem Statement
| Challenge | Effect on travellers |
|---|---|
| Information overload | Hours lost comparing tabs and reviews |
| Budget uncertainty | Overspending, trips cut short |
| Poor planning | Backtracking, wasted days |
| Sustainability concerns | Carbon cost is invisible |
| Safety risks | Risk checks skipped or inconsistent |

## Solution Description
A single-page app where the user enters destination (optional), budget, days and travel style. The agents run in sequence, show their reasoning, and combine into one plan with a trip score, itinerary, cost breakdown, risk level and carbon estimate.

## Functional Requirements
**Travel Planning**
- FR-TP-1: User can enter an optional destination with autocomplete over 20 built-in destinations.
- FR-TP-2: User selects days (1–14) and one of seven travel styles.
- FR-TP-3: "Generate plan" runs all five agents and shows their progress.

**Budget Management**
- FR-BM-1: App accepts a budget of 100–100,000 USD and rejects other values.
- FR-BM-2: App forecasts total cost as daily cost × days.
- FR-BM-3: App shows a five-part breakdown (stay, food, transport, activities, buffer) as a donut chart and states the surplus or shortfall.

**AI Recommendation Engine**
- FR-AI-1: Destinations are scored on style match, budget fit and safety.
- FR-AI-2: App shows the top match and three alternatives.
- FR-AI-3: A trip score (0–100) combines match, budget fit, safety and eco rating.

**Risk Assessment**
- FR-RA-1: Safety score maps to Low, Medium or Elevated risk.
- FR-RA-2: Each level shows a plain-language alert.

**Carbon Footprint**
- FR-CF-1: App shows estimated round-trip CO2 in kg.
- FR-CF-2: App assigns an A–C eco rating and shows tips.

**Itinerary Generator**
- FR-IG-1: Stops are grouped by area and spread across the chosen days.
- FR-IG-2: Days with no stops show a free-day suggestion.

**Persistence and export**
- FR-PE-1: User can save, print and download a trip as JSON.
- FR-PE-2: Theme choice and saved trips persist on the device.

## Non-Functional Requirements
- **Performance:** first load under 2 s on 4G; plan generated in under 3 s; single file under 60 KB.
- **Security:** all inputs validated and stripped of markup characters; no `innerHTML`; strict Content-Security-Policy; safe `JSON.parse` with `try/catch`; no network calls or tracking.
- **Accessibility:** WCAG 2.1 AA – semantic landmarks, labelled inputs, skip link, visible focus, keyboard-only use, live regions, contrast ≥ 4.5:1, reduced-motion support.
- **Scalability:** destination data is a plain array that can be swapped for an API; agents are independent functions that can become LLM calls.
- **Maintainability:** one file, commented dataset, consistent naming, documented in README.

## User Stories
1. As a first-time traveller, I want to enter a budget and days so that I get a trip I can afford.
2. As a backpacker, I want Budget-style matches so that I find low-cost destinations.
3. As a family planner, I want Family-style matches so that activities suit children.
4. As an adventure seeker, I want outdoor-heavy suggestions so that my trip is active.
5. As a luxury traveller, I want high-end destinations so that comfort is prioritised.
6. As an eco-conscious user, I want a carbon estimate so that I can compare impact.
7. As a cautious traveller, I want a risk level so that I know what to watch for.
8. As a time-poor user, I want a full itinerary in one click so that I skip hours of research.
9. As a user with a destination in mind, I want autocomplete so that I can pick it quickly.
10. As a user who typed a wrong place, I want a clear error so that I know how to fix it.
11. As a user over budget, I want to see the shortfall so that I can cut days or change destination.
12. As a user comparing options, I want alternatives so that I can choose with confidence.
13. As a screen-reader user, I want labelled inputs and announced results so that I can plan independently.
14. As a keyboard-only user, I want visible focus and a skip link so that I can navigate without a mouse.
15. As a night-time user, I want dark mode so that the screen is comfortable.
16. As a privacy-minded user, I want no sign-up and local-only storage so that my data stays mine.
17. As a returning user, I want saved trips so that I can revisit plans.
18. As a group organiser, I want to print or export JSON so that I can share the plan.
19. As a judge, I want to see agents working step by step so that I understand the innovation.

## Acceptance Criteria
- **AC-1** Given a valid budget, days and style, when I press Generate plan, then five agent cards update in order and a plan appears.
- **AC-2** Given a budget below 100 or above 100,000, when I submit, then an error is announced and no plan is generated.
- **AC-3** Given an unknown destination, when I submit, then an error explains how to fix it.
- **AC-4** Given a plan, when the cost exceeds my budget, then the summary states the exact shortfall.
- **AC-5** Given a plan, when I press Save trip, then it appears under Show saved trips after a reload.
- **AC-6** Given a plan, when I press Download JSON, then a valid JSON file downloads.
- **AC-7** Given I press Tab from page load, then the skip link appears first and every control shows focus.
- **AC-8** Given reduced-motion is enabled, then counters and agent steps appear without animation.
- **AC-9** Given I enter `<script>` in the destination box, then it is stripped and nothing executes.
- **AC-10** Given a 360 px screen, then no horizontal page scroll occurs.

## Future Enhancements
Live LLM agents; live flights, weather and advisories; multi-city routes; group budgets; booking partners; offline PWA; multilingual UI; user-supplied destination lists.

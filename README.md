# TrainingPeaks (trainingpeaks)

TrainingPeaks is an endurance-athlete training platform for cyclists, runners, triathletes, and their coaches - used to plan structured workouts, track completed activities, analyze fitness with TSS/CTL/ATL and power/heart-rate/pace zones, log metrics, and manage coach-athlete relationships. The TrainingPeaks Partners API (Public API) is an OAuth 2.0, JSON/HTTPS REST API at `api.trainingpeaks.com` (sandbox at `api.sandbox.trainingpeaks.com`) that lets approved third parties read and write athlete profiles, planned and completed workouts, structured workout files, metrics, nutrition, events, routes, and coach data on behalf of a user.

**API access is partner-gated.** Developers must apply for credentials at [api.trainingpeaks.com/request-access](https://api.trainingpeaks.com/request-access) and are individually evaluated; TrainingPeaks states it is not accepting API requests for personal use. Despite the gated access, the full API surface is publicly documented on the [PartnersAPI GitHub wiki](https://github.com/TrainingPeaks/PartnersAPI/wiki). Endpoint paths, methods, and OAuth scopes in this entry are **confirmed** against that wiki; request/response schemas are **modeled** from the wiki object pages because live reference responses require partner credentials and an authorized user.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/trainingpeaks/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/trainingpeaks/refs/heads/main/apis.yml)

## Tags

- Fitness
- Endurance Training
- Workouts
- Coaching
- Sports
- Health
- Wearables

## Timestamps

- **Created:** 2026-07-03
- **Modified:** 2026-07-03

## APIs

### TrainingPeaks Athlete API

Retrieve the authenticated athlete's profile (`athlete:profile`) and their (deprecated) heart-rate, power, and speed training zones. The profile identifies the athlete and whether they are premium or basic, which governs what workout data is returned across the rest of the API.

- **Human URL:** [Athlete Get Profile](https://github.com/TrainingPeaks/PartnersAPI/wiki/Athlete-Get-Profile)
- **Base URL:** `https://api.trainingpeaks.com`

### TrainingPeaks Workouts API

Read planned and completed workouts by date range, create and update planned workouts (`workouts:plan`), fetch a workout by id, delete workouts, and poll for changes since a date. Covers both the athlete's own workouts and, for coach tokens, an athlete's workouts by athlete id.

- **Human URL:** [Workouts Get](https://github.com/TrainingPeaks/PartnersAPI/wiki/Workouts-Get)
- **Base URL:** `https://api.trainingpeaks.com`

### TrainingPeaks Workout Details API

Premium-only analytics for completed workouts - sample-level details (`workouts:details`), mean-max power/pace/HR curves, and time-in-zones breakdowns. Also posts a coach comment to a workout. Requires a premium athlete and an uploaded workout file, otherwise returns 403 or 204.

- **Human URL:** [Workouts Get Details](https://github.com/TrainingPeaks/PartnersAPI/wiki/Workouts-Get-Details)
- **Base URL:** `https://api.trainingpeaks.com`

### TrainingPeaks Workout of the Day API

Retrieve the athlete's Workout of the Day (upcoming planned workouts for a date) and download the structured workout file for a planned workout in fit, erg, mrc, zwo, or json format for delivery to head units and smart trainers (`workouts:wod`).

- **Human URL:** [Workout Of The Day Get](https://github.com/TrainingPeaks/PartnersAPI/wiki/Workout-Of-The-Day-Get)
- **Base URL:** `https://api.trainingpeaks.com`

### TrainingPeaks Metrics API

Read and write athlete wellness/body metrics (weight, HRV, resting heart rate, sleep, and more) by metric id, by date range, or per athlete id for coaches, and create new metric entries (`metrics:read` and `metrics:write`). Date-range metrics reads require a premium athlete.

- **Human URL:** [v2 Metrics Get](https://github.com/TrainingPeaks/PartnersAPI/wiki/v2-Metrics-Get)
- **Base URL:** `https://api.trainingpeaks.com`

### TrainingPeaks Nutrition API

Get, create, update, and delete an athlete's nutrition log entries (`nutrition:read` and `nutrition:write`). Nutrition reads by date range are a premium-athlete restricted endpoint.

- **Human URL:** [Athlete Get Nutrition](https://github.com/TrainingPeaks/PartnersAPI/wiki/Athlete-Get-Nutrition)
- **Base URL:** `https://api.trainingpeaks.com`

### TrainingPeaks Coach API

For coach-authorized tokens (`coach:athletes`) - list the coach's athletes, read the coach profile, manage assistant coaches and their athlete rosters, and read athletes' training zones. Coach tokens then drive the per-athlete-id variants of the workouts and metrics endpoints.

- **Human URL:** [Coach Get Athletes](https://github.com/TrainingPeaks/PartnersAPI/wiki/Coach-Get-Athletes)
- **Base URL:** `https://api.trainingpeaks.com`

### TrainingPeaks File Upload API

Upload a completed device/activity file (.FIT, .TCX, or .PWX) to an athlete's account via the asynchronous `POST v3/file` endpoint (`file:write`). Synchronous upload was deprecated in June 2023; uploads are processed asynchronously and matched against the athlete's calendar.

- **Human URL:** [File Upload Asynchronous](https://github.com/TrainingPeaks/PartnersAPI/wiki/File-Upload-Asynchronous)
- **Base URL:** `https://api.trainingpeaks.com`

### TrainingPeaks Events and Routes API

Read the athlete's next event and events by date, create new events (`events:read` and `events:write`), and read or create GPS routes for an athlete (`routes:read` and `routes:write`) that structured and planned workouts can be associated with.

- **Human URL:** [Event Create](https://github.com/TrainingPeaks/PartnersAPI/wiki/Event-Create)
- **Base URL:** `https://api.trainingpeaks.com`

### TrainingPeaks Webhooks API

Early Access CRUD for webhook subscriptions (`webhook:read-subscriptions` and `webhook:write-subscriptions`). Subscribe to `workout-created`, `workout-updated`, and `workout-deleted` events per athlete; TrainingPeaks then POSTs an event notification to your WebhookUrl. Outbound HTTP callbacks, not a WebSocket.

- **Human URL:** [Webhook Create Subscription](https://github.com/TrainingPeaks/PartnersAPI/wiki/Webhook-Create-Subscription)
- **Base URL:** `https://api.trainingpeaks.com`

## Authentication

OAuth 2.0 authorization code flow. Each application is assigned a `client_id`, `client_secret`, and a fixed set of scopes.

- **Authorize:** `https://oauth.trainingpeaks.com/OAuth/Authorize` (sandbox: `oauth.sandbox.trainingpeaks.com`)
- **Token / Refresh:** `https://oauth.trainingpeaks.com/oauth/token`
- **Deauthorize:** `https://oauth.trainingpeaks.com/oauth/deauthorize`

Access tokens are short-lived (`expires_in` seconds) and refreshed with the `refresh_token` grant. Scopes are not inclusive (e.g. `workouts:details` does not include `workouts:read`). An official Python OAuth example is at [TrainingPeaks/tp-public-api-auth](https://github.com/TrainingPeaks/tp-public-api-auth).

## Common Properties

- [GitHub Organization](https://github.com/TrainingPeaks)
- [LinkedIn](https://www.linkedin.com/company/trainingpeaks)
- [Website](https://www.trainingpeaks.com)
- [Documentation](https://github.com/TrainingPeaks/PartnersAPI/wiki)
- [Plans](plans/trainingpeaks-plans-pricing.yml)
- [Rate Limits](rate-limits/trainingpeaks-rate-limits.yml)
- [Fin Ops](finops/trainingpeaks-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com

# Pomodoro slice — my specification

Complete and commit this before application code. The scope below is provided; your request/response schemas, component plan and tests must make it executable.

## User story

Describe the focused user need and the smallest successful journey:

## Lab requirements

- One user and at most one active session; no login or database.
- FastAPI backend and React frontend, with in-memory storage and a documented restart reset.
- Default session duration is 25 minutes. Accept an integer duration from 1 to 3600 seconds so manual checks can use a five-second session. Reject booleans/noninteger/invalid durations with a validation error.
- The backend records an aware UTC start time and deadline and is the source of truth for state. The client displays time remaining without making an API call every second. Document its refresh/reconciliation strategy.
- Session states are active, stopped and completed. Stopping before the deadline produces stopped; reaching the deadline produces completed. Reconcile expired sessions before returning state or allowing another start.
- A second start while a session is active returns a conflict. Stop on an existing stopped/completed session is idempotent; an unknown session returns not found.
- History includes all sessions. “Completed today” means sessions completed on the current UTC date, using the deadline as completion time; stopped sessions do not count. Make the UTC label visible.
- The UI supports start, early stop, countdown, history and completed-today stats, with loading/empty/error states. Browser refresh should recover the active session from the API.

## API plan

Use this small route set; define the exact schemas, IDs, status codes and examples before coding.

| Route | Purpose | Request | Success shape/status | Failure shapes/status |
|---|---|---|---|---|
| POST /sessions | Start a session | | | |
| GET /sessions | Read history and active state | | | |
| POST /sessions/{id}/stop | Stop/reconcile a session | | | |
| GET /stats | Read completed-today statistics | | | |

Specify consistent field names and timestamp formatting. Explain how an expired session becomes completed when no browser is connected. Define the response after a backend restart so the frontend can recover without pretending the previous session still exists.

## Component and client plan

Name the components and their separate modules, state owners, props/events and API calls. Describe where fetch/error handling lives. Keep the structure small enough to explain.

## Acceptance examples and tests

Describe normal start, early stop, expiry with a controlled clock, duplicate start, unknown ID, repeat stop, invalid duration, empty history, UTC date boundary, refresh recovery and backend-unavailable behavior. Include at least one browser-to-API-to-render trace.

## Configuration and run plan

Record backend/frontend commands and ports, API URL configuration, CORS origin, test commands and the in-memory limitation. This app needs no model API key.

## Implementation increments

For each increment, list the first failing test and the intended behavior. Record spec/test/implementation commits in your reflection as you work.

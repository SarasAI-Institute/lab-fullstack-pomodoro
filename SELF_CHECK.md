# Full-stack self-check

## API and tests

- Tests cover session creation, invalid inputs, duplicate active sessions, stop, idempotent stop and unknown IDs.
- Controlled-clock tests cover completion and UTC-day statistics without real-time sleeps.
- Stopped sessions do not count as completed, and state/history agree across endpoints.
- The suite actually collects and passes tests; preserve real red-before-green commits.

## Browser journey

1. With both processes running, start a short session. Observe the successful request in Network and verify that the displayed session corresponds to its response.
2. Refresh while it is active. The timer recovers from the API rather than restarting a new local timer.
3. Stop early. Confirm the stopped session appears in history and does not increase completed-today statistics.
4. Start a five-second session, allow it to expire and refresh/read the API. Confirm completed state and the correct completed-today count.
5. Try to create a second active session. Confirm the API rejects it and the interface shows an understandable result without creating duplicate state.
6. Stop the backend and trigger a request. Verify a visible recoverable error, then restart it and recover. The reset history should be understandable because storage is in memory.

Check keyboard-operable controls, readable state, sensible narrow-screen layout and visible loading/empty states. Attractive styling cannot substitute for real API behavior.

## Explain and reproduce

- Trace one action through the React handler, API client, FastAPI route, stored state, response and rendered result, using your actual names.
- Verify a clean copy with only the committed files and documented install/run steps. Exclude local environments and installed dependencies from Git; commit dependency manifests and the frontend lockfile.
- Record what you verified, what remains incomplete and any chosen timebox outcome honestly.

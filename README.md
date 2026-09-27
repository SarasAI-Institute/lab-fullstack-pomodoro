# Module 5 mini-lab — Full-stack Pomodoro

Build a small local focus timer with FastAPI and React. Practice turning a spec into a tested backend, building a usable interface and debugging a real request across both halves.

## Scope

Deliver one coherent flow: start a session, display the countdown, stop or complete it, and show history/statistics from the API. Keep authentication, databases, notifications, elaborate themes and cloud deployment outside the core. In-memory state resets on a backend restart; make that visible in the documentation.

This starter supplies planning documents and Python dependency files, not a finished app. You create the backend and frontend. There is no mandatory one-hour deadline. You may choose a personal timebox and record what was completed and what remained.

## Local setup

Download **Code → Download ZIP** from this repository and extract it into a new folder, or clone it if you already use Git. Open that folder in your editor. Use Python 3.12 and Git, with the Codex or Claude Code setup you established in Module 1. No Codespaces, devcontainer or shared API key is needed.

From the lab folder, create and activate a virtual environment:

| Platform | Create | Activate |
|---|---|---|
| macOS / Linux | `python3 -m venv .venv` | `source .venv/bin/activate` |
| Windows PowerShell | `py -3.12 -m venv .venv` | `.venv\Scripts\Activate.ps1` |

All subsequent Python commands use `python` in that active environment. If you downloaded a ZIP, initialize a local Git repository and commit the supplied starter before working. If you cloned it, retain the starter commit. Commit small changes as you go.

For the frontend, also use the course's Node 22.12+ and npm setup. Check `node --version` and `npm --version` before starting.

Install the backend development dependencies from the repository root:

```sh
python -m pip install -r backend/requirements-dev.txt
```

## Tasks

1. **Specify the slice.** Complete and commit [spec.md](spec.md), including endpoint shapes, session states, a component plan and failure behavior. Use the requirements there to keep the app small and consistent.
2. **Build the backend test-first.** Write a failing API test for the first increment, then implement the smallest passing behavior. Continue through start, read, stop/completion and stats. Control time in tests instead of sleeping until a timer expires.
3. **Verify the API directly.** Once you have implemented `backend/main.py` with an `app`, run it from the root with `python -m uvicorn backend.main:app --reload`. Check http://localhost:8000/docs and keep real request/response examples.
4. **Build the frontend.** After committing the spec, scaffold React with Vite, then implement the component plan. Use an API client module and real requests; displayed sessions and stats must come from the backend. Commit the npm lockfile. Styling is secondary to readable controls and clear state.
5. **Connect and debug.** Verify an action in the browser Network panel and backend output. Configure development CORS/API URLs deliberately; show loading and recoverable error states. Use [SELF_CHECK.md](SELF_CHECK.md).
6. **Hand off locally.** Update this README with your actual install, test and two-process run instructions. Check them from a clean copy, and record a full request trace and the observed outcome in REFLECTION.md.

Frontend scaffold commands, from the root (run only after the spec is committed):

```sh
npm create vite@latest frontend -- --template react
cd frontend
npm install
npm run dev
```

Follow any runtime compatibility requirement reported by the generator. Use the frontend address printed by Vite; if its port changes, update the allowed origin/API configuration accordingly. Keep the backend running in a second terminal with its virtual environment active.

Backend tests, once authored, run from the root with `python -m pytest backend/tests`. The backend server command will not work until you create the application; this is expected at the initial handoff.

Useful planning prompt: “Review my spec for ambiguous session-state transitions and API mismatches. Propose the smallest first failing backend test. Do not generate the frontend yet.”

Optional extension: document and verify a reproducible full-stack container run. Cloud accounts, paid services and deployment credentials are not prerequisites for this mini-lab.

## Working with your coding assistant

Use either taught tool; this lab does not require two independent builds. Read the task yourself, supply relevant context, ask for one bounded step, inspect the diff and verify the result. Record a few real decisions in [REFLECTION.md](REFLECTION.md). Try an explanation or hypothesis before requesting implementation. Prompt examples are starting points to adapt, not answers to paste blindly.

This is **ungraded practice**. Keep your work and reflection; there is no submission, mandatory time limit or capstone credit. Apply the method separately to your ongoing PromptLab project. A working mini-lab does not replace capstone evidence.

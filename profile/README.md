<p align="center">
  <img src="../assets/logo.png" alt="Codify wordmark" width="420">
</p>

---

## Codify

Codify is an internal competitive programming platform used by the PSBB Siruseri Coding Club to run coding competitions in the school computer lab.

The system focuses on simplicity, reliability, and fast admin workflows rather than automated judging or large contest infrastructure.

Students write Python solutions directly in the browser, test them using a Pyodide interpreter, and submit them for manual review by admins. XP is awarded for accepted solutions, and a live leaderboard tracks performance during competitions.

This project is intentionally lightweight and purpose-built for small school events.

---

## What This Platform Does

Codify supports the entire workflow for small internal coding competitions.

Students can:

- View the current competition problem
- Write Python code in a browser editor
- Test ideas with a browser-based Python interpreter
- Submit solutions for review
- View submission history
- Track progress on the leaderboard

Admins can:

- Review submissions manually
- Approve or reject solutions
- Award XP
- Control when the competition is open
- Monitor student activity during events

---

## Who This Platform Is For

Codify is designed specifically for:

**Students** - Participating in internal coding competitions - Practicing problem solving in a controlled environment

**Admins** - Running competitions during club sessions - Reviewing student solutions quickly

**Teachers and club leads** - Supervising coding events - Managing participants and competition flow

The system is not designed for public competitions or open registration.

---

## Competition Flow

A typical coding competition using Codify works like this:

Admin enables competition ↓ Students sign in ↓ Students read problem statement ↓ Students write Python code ↓ Students test code in Pyodide interpreter ↓ Students submit solution ↓ Admins review submission ↓ XP awarded if accepted ↓ Leaderboard updates ↓ Admin disables competition

---

## Student Experience

Students interact with only a few focused screens.

**Competition Page** - Problem statement - Code editor - Submit button - Submission history

**Python Interpreter** - Pyodide-based browser Python runtime - Quick testing environment - No backend execution required

**Leaderboard** - Real-time ranking - XP based scoring - Competition standings

The interface is intentionally minimal so students focus on solving problems rather than navigating the app.

---

## Admin Experience

Admins manage competitions through a simple control interface.

Admins can:

- Review pending submissions
- Approve or reject solutions
- Track student submissions
- Enable or disable competitions
- Monitor leaderboard standings
- View registered users

Admin access is controlled through a hardcoded allowlist of school email addresses.

---

## Architecture Overview

Codify uses a serverless Cloudflare-based architecture designed for simplicity and reliability.

```
Student Browser │ │ Python Code ▼ Pyodide Interpreter (Browser Only) │ │ API Requests ▼ Cloudflare Worker API │ ├── Cloudflare D1 (Database) └── Cloudflare KV (Competition State)
```

**Key Design Decisions**

- Student Python code never runs on the backend
- Execution happens entirely inside the browser
- Backend handles only API logic and persistence
- Competition state is controlled using KV toggles

---

## Technology Stack

**Frontend** React, Vite, TailwindCSS, shadcn/ui

**Backend** Cloudflare Workers (TypeScript)

**Database** Cloudflare D1 (SQLite)

**Global State** Cloudflare KV

**Authentication** Clerk

**Browser Python** Pyodide

All infrastructure runs on the Cloudflare platform.

---

## Repository Structure

```
frontend/ React application
worker/ Cloudflare Worker API
database/ D1 database migrations
shared/ Shared types and utilities
docs/ Project documentation
logos/ Brand assets used in README
```

---

## Core Principles

Codify is built around a few core ideas.

**Simplicity first** The system should be easy to understand and maintain.

**Manual review over automated judging** Admins evaluate submissions directly instead of relying on complex judging systems.

**Internal tool** The platform is designed for small competitions within a school environment.

**Cloudflare-native** All infrastructure runs on the Cloudflare platform.

**Safe execution** Student Python code runs only inside the browser using Pyodide.

---

## Security Model

Several safeguards ensure the system stays safe for school use.

- Only approved school email accounts may sign in
- Admin privileges come from a hardcoded allowlist
- Python code never executes on the backend
- Competitions can be disabled instantly
- Students cannot access admin tools

---

## Deployment

Codify is deployed entirely on Cloudflare infrastructure.

**Frontend:** Cloudflare Pages  
**API:** Cloudflare Workers  
**Database:** Cloudflare D1  
**Competition State:** Cloudflare KV

---

## Development Notes

When contributing to this project, prioritize:

- Clear UI flows
- Minimal admin complexity
- Straightforward APIs
- Readable code
- Small predictable database changes

Avoid introducing unnecessary abstractions or complexity.

The goal is to keep Codify simple, stable, and easy to run during real competitions.

---

## In One Sentence

Codify is a lightweight internal coding competition platform that allows students to solve Python problems and admins to review and score them quickly during live school events.

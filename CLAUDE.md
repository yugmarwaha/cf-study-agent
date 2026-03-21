# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Development
npm run dev          # Start local dev server (Vite + Cloudflare Workers)

# Build & Deploy
npm run deploy       # Build and deploy to Cloudflare Workers

# Code Quality
npm run check        # Run format + lint + TypeScript check (run before committing)
npm run lint         # oxlint
npm run format       # oxfmt
npm run types        # Regenerate TypeScript types from wrangler config
```

## Architecture

This is a full-stack AI chat agent running on Cloudflare Workers with a React frontend.

**Entry points:**
- `src/server.ts` — Cloudflare Worker + Durable Object (`ChatAgent`). Handles WebSocket connections, AI streaming, tool execution, task scheduling, and MCP server management.
- `src/app.tsx` — React 19 chat UI. Connects to the agent via `useAgent()` / `useAgentChat()` hooks over WebSocket.
- `src/client.tsx` — React DOM entry point.

**Key concepts:**

- `ChatAgent` extends `AIChatAgent<Env>` (from the `agents` package) and runs as a Durable Object with SQLite-backed persistent state. One instance per user/session.
- The agent uses the Kimi-K2.5 model via Workers AI (`env.AI` binding).
- Tools follow three patterns:
  1. **Server auto-execute** — runs immediately server-side (e.g., `getWeather`)
  2. **Client-side** — returned to the browser for execution (e.g., `getUserTimezone`)
  3. **Approval-gated** — requires explicit user approval before running (e.g., `calculate`)
- `@callable()` decorated methods on `ChatAgent` can be invoked from the React client directly (e.g., `addServer`, `removeServer`).
- Task scheduling uses the `agents` SDK's `this.schedule()` / `this.getSchedules()` / `this.cancelSchedule()` methods. Scheduled tasks execute via `executeTask()` and broadcast results to connected clients.
- MCP servers connect via OAuth; the OAuth callback URL is registered in `onStart()`.

**Routing (`wrangler.jsonc`):**
- `/agents/*` and `/oauth/*` are handled by the Worker first (not served as static assets).
- Everything else is served from the `public/` directory (SPA).

**AI SDK:** Uses Vercel AI SDK (`streamText`, `tool`) with `workers-ai-provider` for the Workers AI binding. To switch models or providers, update the `model` and provider import in `src/server.ts`.

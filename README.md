# CS Study Agent

An AI-powered computer science study assistant built on Cloudflare Workers using the [Agents SDK](https://developers.cloudflare.com/agents/). It helps university students understand CS concepts, generate practice problems, and schedule study reminders — all through a real-time chat interface.

**Live demo:** [cf-study-agent.yugmarwaha987.workers.dev](https://cf-study-agent.yugmarwaha987.workers.dev/)

## Features

- **Concept explanations** — Ask about any CS topic (data structures, algorithms, OS, networking, databases, ML, systems programming) and get clear, structured explanations with examples
- **Practice problem generation** — Generate practice questions by topic, difficulty (easy/medium/hard), and type (conceptual, coding, multiple-choice, short-answer)
- **Study reminders** — Schedule one-time, delayed, or recurring (cron) reminders to stay on track
- **Image input** — Drop or paste images (diagrams, code screenshots) and ask questions about them
- **MCP server support** — Connect external tool servers via OAuth for extended capabilities
- **Dark/light mode** — Cloudflare Kumo UI with theme toggle
- **Persistent chat** — Messages are stored in SQLite via Durable Objects; conversations survive disconnects

## Tech Stack

- **Runtime:** Cloudflare Workers + Durable Objects
- **AI Model:** Kimi K2.5 via Workers AI (no API key required)
- **Frontend:** React 19 + Tailwind CSS + Cloudflare Kumo components
- **AI SDK:** Vercel AI SDK (`streamText`, `tool`)
- **Build:** Vite + Wrangler

## Quick Start

```bash
git clone <your-repo-url>
cd cf-study-agent
npm install
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) to start studying.

### Example prompts

- **"Explain how a hash map works"** — get a structured concept explanation
- **"Give me a medium difficulty question on binary trees"** — generate a practice problem
- **"What's the difference between TCP and UDP?"** — compare concepts
- **"Remind me in 30 minutes to review linked lists"** — schedule a study reminder
- Drop a diagram and ask **"What data structure is this?"** — image understanding

## Project Structure

```
src/
  server.ts    # ChatAgent Durable Object — AI streaming, tools, scheduling, MCP
  app.tsx      # React chat UI with Kumo components
  client.tsx   # React DOM entry point
  styles.css   # Tailwind + Kumo styles
```

## Commands

```bash
npm run dev       # Start local dev server (Vite + Cloudflare Workers)
npm run deploy    # Build and deploy to Cloudflare Workers
npm run check     # Run format + lint + TypeScript check
npm run lint      # oxlint
npm run format    # oxfmt
```

## Deploy

```bash
npm run deploy
```

Your agent goes live on Cloudflare's global network. Messages persist in SQLite, streams resume on disconnect, and the agent hibernates when idle.

## License

MIT

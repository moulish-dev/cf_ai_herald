
```markdown
# cf_ai_herald

> A voice-enabled AI briefing agent built on Cloudflare. Herald briefs you on what matters — weather, schedule, tasks — concisely and in order of importance.

🔗 **Live demo:** [https://cf-ai-herald.moulishb1.workers.dev/]

---

## What it does

Herald is a chief-of-staff style AI agent. Ask it to "brief me" and it pulls together everything available — current weather, your scheduled tasks, timezone context — into a single prioritised summary. It also accepts voice input: speak your query and Herald transcribes and responds.

## How it maps to the assignment requirements

| Requirement | Implementation |
|---|---|
| LLM | Llama 3.3 70B via Cloudflare Workers AI (`@cf/meta/llama-3.3-70b-instruct-fp8-fast`) |
| Workflow / coordination | Cloudflare Durable Objects via the Agents SDK — schedules, state, and message persistence all run inside a single `ChatAgent` Durable Object |
| User input via chat or voice | Chat UI (Kumo components) + voice input via `MediaRecorder` → Whisper transcription (`@cf/openai/whisper-tiny-en`) |
| Memory / state | `this.setState()` persists user preferences (name, city) across sessions; chat history persists in SQLite via `maxPersistedMessages` |

## Features

- **Herald persona** — briefing-first system prompt, structured output, no filler
- **Voice input** — record audio in-browser, transcribed on-device via Whisper on Workers AI
- **Real weather** — live data from Open-Meteo (no API key required)
- **Task scheduling** — one-time, delayed, and cron reminders with broadcast notifications
- **MCP support** — connect external tools via the MCP client
- **Dark/light mode** — Cloudflare Kumo design system

## Running locally

```bash
git clone https://github.com/moulish-dev/cf_ai_herald
cd cf_ai_herald
npm install
npm run dev
```

Open [http://localhost:5173](http://localhost:5173)

Try these prompts:
- **"Brief me"** — full situational summary
- **"What's the weather in London?"** — live weather via Open-Meteo
- **"Remind me in 10 minutes to check my email"** — scheduled task
- **Click the mic button** — speak your query instead of typing

## Deploying

```bash
npm run deploy
```

## Project structure

```
src/
  server.ts    # ChatAgent — tools, scheduling, voice transcription, state
  app.tsx      # Chat UI with voice input button
  client.tsx   # React entry point
  styles.css   # Tailwind + Kumo styles
PROMPTS.md     # AI prompts used during development
```

## Stack

- [Cloudflare Workers AI](https://developers.cloudflare.com/workers-ai/) — Llama 3.3 + Whisper
- [Cloudflare Agents SDK](https://developers.cloudflare.com/agents/) — Durable Objects, chat, scheduling
- [Kumo UI](https://developers.cloudflare.com/style-guide/) — Cloudflare design system
- [Open-Meteo](https://open-meteo.com/) — free weather API

## Author

Built by [Moulishwaran Balaji](https://github.com/moulish-dev) for the Cloudflare internship assignment.
```

---

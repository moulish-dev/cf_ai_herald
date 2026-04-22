# PROMPTS.md — AI prompts used during development of cf_ai_herald

This file documents the prompts used with Claude (claude.ai) during the
development of this project, as required by the Cloudflare AI assignment.

---

## 1. Project scaffolding

**Prompt:**
> I'm building a Cloudflare AI internship assignment project using the
> cloudflare/agents-starter template. The project should be a voice-enabled
> AI briefing agent called Herald. What should my checklist be to go beyond
> the template and meet all four requirements: LLM, workflow/coordination,
> voice input, and memory/state?

**What it produced:**
A prioritised checklist mapping each assignment requirement to concrete
implementation steps, identifying voice input as the key differentiator.

---

## 2. System prompt — Herald persona

**Prompt:**
> Rewrite the system prompt for a herald persona — an AI that briefs the
> user on what matters, concisely and in order of importance. It should
> behave like a chief of staff: filter noise, surface signal, lead with
> the most actionable information. No filler phrases.

**What it produced:**
The Herald system prompt now in server.ts, including the Behaviour, Tools,
Scheduled tasks, and Identity sections.

---

## 3. Voice input wiring

**Prompt:**
> Help me wire voice input into my app.tsx. I want a mic button that records
> via MediaRecorder, converts to base64, sends to the transcribeAudio tool
> on the server which uses Whisper on Workers AI, then feeds the transcript
> back as a chat message.

**What it produced:**
The full voice input implementation: state variables, handleVoiceInput
callback, mic/stop/spinner button in the input bar, and the system prompt
instruction for handling [audio:BASE64] messages.

---

## 4. Real weather API

**Prompt:**
> Replace the random-data weather stub in server.ts with a real
> implementation using Open-Meteo. It should geocode the city name first,
> then fetch current temperature, weather condition, windspeed and humidity.
> No API key should be required.

**What it produced:**
The two-step Open-Meteo implementation (geocoding + weather fetch) now
in the getWeather tool.

---

## 5. README

**Prompt:**
> Write a production-quality README.md for cf_ai_herald. It should have a
> live link at the top, a clear one-paragraph description, an explicit table
> mapping the project to each of the four Cloudflare assignment requirements,
> features list, local run instructions, and stack section.

**What it produced:**
The current README.md.

---

## Iteration notes

- Initial syntax error in the system prompt (mismatched backtick) was
  caught and fixed with Claude's help
- Voice input uses [audio:BASE64] message convention to trigger the
  transcribeAudio tool — a pattern suggested during the wiring session
- Open-Meteo was chosen over other weather APIs specifically because it
  requires no API key, keeping the project zero-config to run locally
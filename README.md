# AETHER AI

A Node.js/Express AI chat website with a responsive browser interface.

## Project files

- `index.html`, `style.css`, `app.js` — frontend, served from the repository root
- `server.js` — Express API, Groq chat proxy, English Wikipedia search, and text-file reader
- `.env.example` — local environment-variable template

## Run locally

1. Install Node.js 20 or newer.
2. Clone/download this repository and open its folder in a terminal.
3. Run `npm install`.
4. Copy `.env.example` to `.env` and add your own Groq API key from [Groq Console](https://console.groq.com/keys).
5. Run `npm start` and open `http://localhost:3000`.

Keep `.env` private; never commit an API key. On Render, set `GROQ_API_KEY` (and optionally `GROQ_MODEL`) in the service's Environment settings.

## What works

- Chat responses through the Groq API when a valid key/model is configured
- English Wikipedia article search (not broad web search)
- Up to 10 browser-local conversation threads, keeping up to 40 messages per thread (not account-based or synced; saved message text is capped at 12,000 characters)
- Browser-provided speech recognition and speech synthesis where supported
- Text/code file reading: TXT, MD, CSV, JSON, JS, HTML, CSS, XML, LOG; 2 MB upload cap and at most 30,000 characters sent with a chat request
- Code assistance and image-prompt drafting through chat; image files are not generated

## Important limitations and privacy

This is a small public demo, not a complete production service. There is no sign-in, account system, server-side chat database, or cross-device history. Up to 10 recent chats are kept in the current browser's local storage, with up to 40 messages per thread and saved text capped at 12,000 characters per message; anyone using the same browser profile may be able to see them. Starting a new chat keeps prior saved local threads, but clearing browser storage removes them.

Chat prompts and any attached text included in a question are sent from this server to Groq to generate a reply. Do not submit passwords, secrets, or sensitive personal information. Search queries go to the English Wikipedia API. Voice input/output uses the browser's speech features.

The built-in API throttles are per-process and reset when the server restarts; for multiple instances, use a shared rate-limit store. Public deployment should also use an approved provider budget/usage limit and monitor logs. This repository does not include a general web-search provider, image-generation service, authentication, or cloud database; those require separately selected services/credentials and configuration. Render's free instance may sleep when idle, so its first response can be delayed.

## Model configuration

The default model is `openai/gpt-oss-20b`. If it is unavailable for your Groq account, check [Groq's model list](https://console.groq.com/docs/models) and set `GROQ_MODEL` in `.env` or Render Environment settings to a currently available chat model.

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
- Intent-led studio workspace with Assistant, Wikipedia-grounded Research, Code, Writing, Learn and Plan modes; response-style selection remains separate
- Conversation-first layout with the animated orbital logo, responsive phone three-dot drawer, work-mode strip and accessible Toolbox tabs
- The main search field submits ordinary questions to AETHER; prefix a query with `wiki:` to search English Wikipedia. Research mode fetches up to five English Wikipedia results to ground its answer and cite the supplied links; it is not broad web or live-news research
- Up to 10 browser-local conversation threads, keeping up to 40 messages per thread (not account-based or synced; saved message text is capped at 12,000 characters)
- Find saved chats by matching titles or message text while retaining Share, Markdown Download, confirmed Delete and current-chat Clear behavior
- Export/import bounded local JSON chat backups to manually move history between browser profiles or devices; import merges by thread ID and keeps the 10 most recently updated threads
- Stop an in-progress response; stopping preserves any partial reply, and the server aborts its upstream request when the browser disconnects
- Optional local assistant context (up to 2,000 characters) and explicit opt-in to include it with new prompts; it remains in this browser until the user clears it
- Browser-provided speech recognition and speech synthesis where supported
- Six response styles: Balanced, Quick, Deep dive, Tutor, Builder, and Creative
- Default formatting favors concise prose and ordinary punctuation: simple factual answers avoid unnecessary headings, hashtags, dash lists, numbered lists, and divider lines; structured formats remain available when requested or useful
- Focus mode hides the side panels; responses and code blocks have copy controls; the current thread can be exported as Markdown
- Text/code file reading: TXT, MD, CSV, JSON, JS, HTML, CSS, XML, LOG; 2 MB upload cap and at most 30,000 characters sent with a chat request
- Toolbox utilities: arithmetic calculator with a safe parser, unit conversion (length, mass, temperature, digital storage, time), and a local Text Lab (counts, case/spacing cleanup, duplicate-line removal, JSON formatting, copy, and send-to-chat)
- The calculator, converter, and Text Lab run locally in the browser; their contents are not uploaded unless the user explicitly sends text to chat
- Saved chats have a right-click or ⋯ menu for Share (native share sheet, with clipboard fallback), Markdown Download, and confirmed Delete; Clear removes the current conversation and unsent draft after confirmation while preserving other saved chats
- Code assistance and image-prompt drafting through chat; image files are not generated

## Important limitations and privacy

This is a small public demo, not a complete production service. There is no sign-in, account system, server-side chat database, or cross-device history. Up to 10 recent chats are kept in the current browser's local storage, with up to 40 messages per thread and saved text capped at 12,000 characters per message; anyone using the same browser profile may be able to see them. Starting a new chat keeps prior saved local threads, but clearing browser storage removes them.

Chat prompts and any attached text included in a question are sent from this server to Groq to generate a reply. Do not submit passwords, secrets, or sensitive personal information. Search queries go to the English Wikipedia API. Voice input/output uses the browser's speech features.

Work-mode, response-style, language, and optional assistant-profile instructions are added to the request sent to Groq. Profile context is included only after the user enables its checkbox in Settings; it is capped at 2,000 characters and is stored locally. Chat and backup exports are generated locally in the browser. Focus mode, work mode, response style, and local preferences are saved only in the current browser profile. The Toolbox calculator, converter, and Text Lab process content in the current browser tab; use “Send to chat” only when you want text submitted to Groq.

Saved chat history remains in this browser only, unless the user chooses to download and manually import a backup. Backup files contain conversation text; keep them private. Import accepts only AETHER JSON backups up to 6 MB, at most 10 chats, 40 messages per chat, and 12,000 characters per message. Share acts only after the user selects it and uses the browser’s share sheet when available, otherwise it copies the transcript. Clear and Delete ask for confirmation and affect only the selected/current chat; other saved conversations are kept.

The built-in API throttles are per-process and reset when the server restarts; for multiple instances, use a shared rate-limit store. Public deployment should also use an approved provider budget/usage limit and monitor logs. This repository does not include a general web-search provider, image-generation service, authentication, or cloud database; those require separately selected services/credentials and configuration. Render's free instance may sleep when idle, so its first response can be delayed.

## Model configuration

The default model is `openai/gpt-oss-20b`. If it is unavailable for your Groq account, check [Groq's model list](https://console.groq.com/docs/models) and set `GROQ_MODEL` in `.env` or Render Environment settings to a currently available chat model.

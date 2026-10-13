# AETHER AI

A futuristic dark navy / cyan / violet AI assistant starter website.

## Files
- `public/index.html` — page structure
- `public/style.css` — responsive UI design
- `public/app.js` — browser interactions
- `server.js` — API server, AI chat, Wikipedia search, text-file upload
- `.env.example` — environment variable template

## Run on Windows
1. Install Node.js LTS from https://nodejs.org/
2. Extract this ZIP and open the `AETHER-AI` folder.
3. Click the folder address bar, type `cmd`, press Enter.
4. Run `npm install`
5. Copy `.env.example` to `.env`.
6. Get an API key at https://aistudio.google.com/apikey and put it in `.env`:
   `GROQ_API_KEY=your_private_key`
7. Run `npm start`
8. Open http://localhost:3000

Keep `.env` private; never upload it to GitHub.

## Features in this starter
- Groq API-backed chat, when configured
- Multilingual prompts
- Browser voice recognition where supported
- Browser spoken replies
- Local browser chat history
- Wikipedia search helper (not full general web search)
- Upload and analyze text/code files up to 2 MB
- Code generation via chat
- Image prompt helper (actual image generation is not connected yet)

## Important limitations
This is a starter project, not a finished production service. PDF/DOCX extraction, real image generation, full web search, accounts, cross-device cloud memory, and public deployment are not included. Browser history is local to the current browser. A Node/Express backend needs a Node-compatible host or conversion to serverless functions; static hosting alone will not run `server.js`. Free API and hosting tiers have limits.


## Groq model configuration

The default model is `openai/gpt-oss-20b`. If that model is unavailable in your Groq account, check current model IDs at https://console.groq.com/docs/models and set `GROQ_MODEL` to an available chat model in `.env` or your hosting environment.

# Lecture Hub

A lightweight static lecture portal built with HTML, CSS, and vanilla JavaScript. It is ready for GitHub Pages or Vercel: deploy this folder as a static site with no build step.

## API

The site uses the configured Google Apps Script web app in `api.js`. Lecture records are never hard-coded. The helper requests `lectures`, `allLectures`, `settings`, `stats`, and `logs`; it posts `login`, `adminLogin`, `visit`, `log`, and `updateSettings` requests when the backend supports them.

The Apps Script endpoint should return JSON, preferably `{ success: true, data: ... }`, although the client also accepts a direct object/array and common `result` payloads. Login responses may use `success`, `authenticated`, `valid`, or `status: "success"`.

## Deploy

- **GitHub Pages:** push these files to a repository and select the main branch/root in Pages settings.
- **Vercel:** import the repository and choose the default static deployment. No framework preset or build command is needed.

The visitor password is `NOTES` (case-insensitive) and access is session-only; no password is stored in localStorage. It is validated in the static site so visitors can enter even if the Apps Script service is unavailable. This is a convenience gate only: a password embedded in a static website cannot secure private material. Admin authentication remains controlled by the backend.

## Chatbot

The chatbot uses Pollinations' free, public OpenAI-compatible endpoint (`https://text.pollinations.ai/openai`). It is called directly from the browser with no API key, no WebGPU requirement, and no browser extension requirement. This replaces the prior large in-browser WebLLM model, which did not run in many browsers.

The chatbot keeps a built-in learning and lecture-search fallback. If the public AI service is busy or offline, users still receive a useful response instead of seeing a failed or stuck chat.

Because this is a shared public service, do not send passwords, personal information, or private lecture content to the chatbot. For a production site with guaranteed capacity and private data handling, use a paid server-side AI provider instead.

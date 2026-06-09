# Pratyush Ingale — Mission Control Portfolio

Interactive portfolio site: dark mission-control theme, two playable games, and an AI agent (real LLM with graceful client-side fallback).

## Structure
```
├── index.html      # Entire site — HTML, CSS, JS in one file
├── api/
│   └── chat.js     # Vercel serverless function (Groq LLM)
└── README.md
```

## Features
- **Boot sequence** — orchestrator-style startup animation (skippable, respects reduced-motion)
- **Audit-log experience timeline** — career as verified log entries
- **4 live project cards** with status indicators
- **Hallucination Hunter** — guess which facts about Pratyush are real vs AI-hallucinated
- **Spot the Anomaly** — 45-second fraud-analyst mini game
- **PRATYUSH-AGENT chat** — real LLM via Groq free tier; if the API is down or rate-limited, an embedded keyword-retrieval fallback answers instead. The bot never breaks.

## Deploy to Vercel (free)

1. Push this folder to a GitHub repo (e.g. `portfolio`):
```bash
cd portfolio_site
git init
git add index.html api/chat.js README.md
git commit -m "Mission control portfolio"
git remote add origin https://github.com/PratyushIngale14/portfolio.git
git push origin master
```

2. Go to **vercel.com** → sign in with GitHub → **Add New Project** → import the repo → Deploy. No build settings needed (it auto-detects the static file + api folder).

3. Get a **free Groq API key** at **console.groq.com** → API Keys → Create.

4. In Vercel: Project → **Settings → Environment Variables** → add:
   - Name: `GROQ_API_KEY`
   - Value: your key
   
   Then **Redeploy** (Deployments → ⋯ → Redeploy).

5. Done. Site is live at `your-project.vercel.app`.

## Testing the chatbot
- With the key set: answers come from Llama 3.3 70B with Pratyush's full profile as context.
- Without the key (or if rate-limited): the front-end silently falls back to built-in answers. Try asking about CHG, LedgerMind, visa status, or the café story.

## Customizing
- All facts live in two places: the `FALLBACK_KB` array in `index.html` and the `PROFILE` string in `api/chat.js`. Update both when your profile changes.
- Game content: `hhData` (Hallucination Hunter statements) and `anNormals`/`anAnomalies` (transaction feed) in `index.html`.

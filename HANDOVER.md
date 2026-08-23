# Handover — Digital Guide / Halil Şahin showcase site

Read `/Users/halil/.claude/projects/-Users-halil-Desktop-halil-lebenslauf/memory/digital-guide-showcase.md` and `halil-user-profile.md` first — full history there. This file is the short "what's open" version.

## State
- Live: https://digital-guide-showcase.vercel.app
- Repo: https://github.com/halilsahn-hue/digital-guide-showcase (public, `main` branch)
- File: `index.html` in this directory — single self-contained page, no build step. Vercel project already linked (`vercel link` done, scope `hals-projects-a1f48ca2`). Deploy with:
  ```
  git add -A && git commit -m "..." && git push
  vercel deploy --prod --yes
  ```

## Open items — ask Halil, don't fabricate
1. **WhatsApp CTA links are placeholder.** Every `href="https://wa.me/message"` (header, hero buttons, footer) needs his real number: `https://wa.me/<countrycode><number>`.
2. **No LinkedIn / CV link.** Hero and footer intentionally omit these — add only if Halil gives real URLs.
3. **"Agentic Development Lab" case study** (Claude/Codex/DeepSeek/OpenHands/OpenCode) is grounded only in the `DeepClaude` repo, which is a modest Claude Code → DeepSeek routing wrapper — smaller than the multi-agent-harness framing implies. Confirm with Halil whether Codex/OpenHands/OpenCode are actually wired in, or soften the copy.
4. **No live/public link** for: Agentic Development Lab, Web Intelligence Pipeline, Visual QA Engine (all internal tools / private repos). If Halil later makes any of these public or gives a demo URL, add a `case-link`/card link.

## How content is structured
- Everything text-visible goes through the `translations` JS object (`en`/`de`/`tr`) keyed by `data-key` attributes on the elements. Adding any new visible text = add the element with a `data-key` + add that key to all three language blocks, or it silently won't translate (falls back to whatever's hardcoded in the HTML, which is English).
- Default language is EN (browser-detected, `localStorage` key `dg_lang` persists user choice).
- Project cards are grouped into `.sector[data-sector="..."]` sections (`featured`, `products`, `ai`, `devtools`, `client`); the tab filter JS just toggles `.is-hidden` on these — `Experiments`, `How I Work`, `About` sections are outside this system and always visible.
- Status badges (`st-production` / `st-prototype` / `st-client` / `st-extension` / `st-internal` / `st-rnd`) are a deliberate honesty signal — don't relabel a demo as Production.

## Method for re-auditing project links later
Repos rot — a couple came back to life this session after being dead last time, others are still down. Before trusting any homepage URL again:
```
gh repo list halilsahn-hue --limit 200 --json name,homepageUrl,pushedAt --source
# then curl -s -o /dev/null -w "%{http_code}" on each homepageUrl
```
Drop anything not returning 200 (or explain a 401 if it's intentionally gated).

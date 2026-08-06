# Elevated Vision AI Growth Agent — PRD

**Tagline:** Your AI marketing employee for local businesses
**Status:** Test version (v0.1) — client-side demo
**Owner:** Elevated Vision

## 1. Problem
Small businesses don't know:
- Why they're not ranking on Google
- What to post on social media
- Whether AI tools (ChatGPT, Gemini, Claude) recommend them
- Which SEO fixes actually matter

## 2. Solution
An AI agent that acts as a 24/7 marketing consultant: scans a business's online presence, scores its marketing health, and generates a ready-to-use action plan (SEO fixes, content calendar, blog ideas, social captions, review responses).

## 3. Full product vision (features)
- Scan Google Business Profile
- Scan website
- Scan Facebook/Instagram/TikTok
- Analyze competitors
- Grade AI visibility (what ChatGPT/Gemini/Claude say about the business)
- Generate a 30-day content calendar
- Create social posts
- Generate blogs
- Suggest keywords
- Monitor reviews
- Create QR codes
- Marketing Health Score
- Automated task nudges ("Post this Reel tomorrow", "Respond to these 4 Google reviews", "Your competitor just outranked you")

## 4. Test version scope (what's built today)
A single-page demo app where the user manually enters:
- Business name, industry, city/area, website (optional), and a short description of the business and its goal

The app calls the Claude API live and returns:
- Marketing Health Score (with reasoning)
- SEO recommendations
- 30-day content calendar
- Review response drafts (positive + negative example)
- Blog ideas
- Social captions
- Homepage improvement suggestions
- An "AI visibility" note (directional — how discoverable the business likely is to AI assistants)
- Print/export to PDF via the browser

## 5. Explicitly NOT in this version
- No live scan of the actual website (would require a server-side fetch/scraper — browser CORS blocks this client-side)
- No live Google Business Profile or Places data (requires a Google Cloud project with billing enabled)
- No social media scanning (Instagram/TikTok/Facebook scraping of accounts you don't own violates their ToS — needs owned-account API access instead)
- No real competitor analysis (needs Google Custom Search API or similar)
- No persistent storage, accounts, or task reminders yet
- The "AI visibility" score is a simulated estimate, not a verified live check against ChatGPT/Gemini

## 6. Why this scope for the test version
The goal was a working, shareable demo buildable with $0 upfront and no backend, to validate the report quality and the score/report UX before investing in scanning infrastructure. Every excluded feature above is a scoped "v0.2" item, not a dropped idea.

## 7. Tech (test version)
- Single self-contained HTML/JS file, no build step
- Styled to Elevated Vision brand (cream #f2eddb, taupe #62574e, Poppins)
- Calls Anthropic's Messages API directly from the browser (model: claude-sonnet-4-6)
- Hosted as a Claude.ai artifact for the public demo link

## 8. Path to v0.2 (real scanning)
| Feature | Free/low-cost path |
|---|---|
| Website scan | Google PageSpeed Insights API (free) + a small server-side scraper (Cheerio) |
| Google Business Profile / competitors | Google Places API (New) — billing must be enabled, but low request volume with minimal fields stays within free monthly allowance |
| Search visibility | Google Custom Search JSON API — 100 free queries/day |
| Social scanning | Only for accounts the client connects/owns, via each platform's official Graph API |
| Backend | Needed once you add live scanning — Supabase (free tier) + a hosted function (Vercel free tier) to get around browser CORS limits |

## 9. Success criteria for the test version
- Runs a full input → report cycle in under 30 seconds
- Report reads as genuinely useful/actionable to a real small business owner (validate on 2-3 existing Elevated Vision clients)
- Score and recommendations feel consistent across similar inputs (not wildly random run-to-run)

## 10. Next steps
1. Run the test version on 2-3 real EV clients, collect feedback on report usefulness
2. Prioritize which v0.2 scanning feature to add first based on what feels most "fake" in the demo
3. Decide on pricing model once real scanning is in place ($49-99/mo subscription range under consideration)

# WKJ-Phishing

> Interactive phishing email awareness training · 钓鱼邮件找茬训练

[简体中文](README.md) | **English**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A fully static, single-page training tool: read a simulated email, mark whatever you find suspicious with your own judgement, then go through the debrief point by point — what the clue was, why it deserves suspicion, and what to do next. It does not simulate real attacks and collects no data. It does one thing: break "spot phishing emails" from a slogan into individual, practicable judgements.

## Try it online

**[https://keji-wang.github.io/wkj-phishing/](https://keji-wang.github.io/wkj-phishing/)**

No sign-up, no backend, no tracking — everything loads with the page itself. The training interface is currently in Chinese.

## Screenshots

| Desktop · Home | Desktop · Marking risks |
|---|---|
| ![Desktop home](docs/screenshots/desktop-landing.webp) | ![Desktop practice](docs/screenshots/desktop-practice.webp) |

| Desktop · Debrief | Mobile · Training |
|---|---|
| ![Desktop result](docs/screenshots/desktop-result.webp) | ![Mobile](docs/screenshots/mobile-practice.webp) |

## How a session works

1. **Pick** a single email by scenario, or start the full set (ordered easy → hard).
2. **Mark**: tap any text, button, link or sender address you find suspicious; tap again to unmark.
3. **Submit**: the tool never hints whether a mark is right — everything is revealed only after submission.
4. **Debrief**: every risk point comes with "why it's dangerous" and "the right move", labelled by signal type:
   - **Hard evidence** (blue): objectively verifiable facts — lookalike domains, unknown bank accounts, demands for one-time codes;
   - **Social tactic** (orange): psychological pressure — fake urgency, secrecy demands, borrowed authority.
5. **Next steps**: each email ends with 2–3 concrete handling suggestions (verification channels, escalation paths).
6. **Retry** anytime; individual emails can be skipped.

## Scoring

The scoring is designed to reward careful reading and precise marking, not blind clicking:

- Hits score by severity (low +1 / medium +2 / high +3 / critical +4);
- Tapping a non-risk area costs **-1 point** (floored at 0 per email), with the rule disclosed before answering;
- Misses don't deduct points but are fully revealed;
- "Skip" is scored against the same weight scale, keeping totals comparable.

## Run locally

```bash
git clone https://github.com/Keji-Wang/wkj-phishing.git
cd wkj-phishing

# any static server works
python -m http.server 8000
# or
npx serve .

# open http://localhost:8000
```

Opening `index.html` directly also works — there are no external API dependencies.

## Deployment

Pushes to `main` are published automatically via GitHub Pages (repo Settings → Pages → Deploy from branch). Any static host works too:

```bash
docker run -d -p 80:80 -v $(pwd):/usr/share/nginx/html:ro nginx:alpine
```

## Maintaining content

All exercises live in the `EMAILS` array inside `index.html`, one object per email:

```javascript
{
  id: 'e001',
  scenario: 'urgency',          // scenario key, defined in SCENARIOS
  difficulty: 3,                // 1-5; the full set is sorted by this
  title: 'Exercise name',
  fromRiskId: 'e001-rX',        // optional: makes the sender address a markable risk point
  email: {
    subject: '...',
    from: { name: 'Display name', email: 'sender@example.net' },
    to: 'victim@example.com',
    date: '2026-05-28 16:32',
    body: `<p>Body HTML. <span class="risk-point" data-risk-id="e001-r1">suspicious text</span></p>`,
    attachments: []             // optional: [{ name: 'x.pdf', size: '245KB' }]
  },
  riskPoints: [
    {
      id: 'e001-r1',            // must match data-risk-id in the body
      type: 'evidence',         // 'evidence' | 'tactic'
      label: 'Risk label',
      severity: 'high',         // low | medium | high | critical (weight)
      explanation: 'Why it is dangerous',
      correctAction: 'The right move'
    }
  ],
  nextSteps: ['Handling advice 1', 'Handling advice 2']   // optional
}
```

Notes:

- Markable text is wrapped as `<span class="risk-point" data-risk-id="...">text</span>`; CTA buttons use `<a class="email-cta risk-point">`;
- Every risk point `id` needs a matching `data-risk-id` in the body, otherwise it cannot be selected;
- New scenarios require a matching entry in `SCENARIOS`.

## Design trade-offs

- **No hover hints**: underline-on-hover hands out the answers, reducing training to "select everything". Desktop and mobile share one identical tap-to-mark interaction — think first, then tap.
- **A gentle cost for false taps**: zero feedback leaves users unsure whether a tap registered; heavy penalties discourage exploration. -1 point plus a light toast gives feedback while making brute-force clicking pointless.
- **Evidence vs tactics**: separating verifiable facts (lookalike domains) from psychological pressure (fake urgency) avoids teaching people to condemn a single surface cue as malicious.
- **Feedback reaches "what to do next"**: every point explains why it's dangerous and the right move; every email ends with handling advice. The goal is not the score but remembering the judgement and the response.
- **A deliberately small feature set**: no admin panel, no accounts, no AI generation, no analytics, no data collection. It is a practice page you can simply hand to trainees — all content ships in a single file.

## Current limitations

- The exercise set (6 emails, 48 risk points) is embedded in `index.html`; splitting the data into its own file may be warranted as content grows;
- No progress or score history is stored (resets on refresh) — a deliberate privacy trade-off;
- The interface is currently Chinese-only.

## License

[MIT](LICENSE) © Jeffrey Wang

---

⚠️ **Disclaimer**: this tool is for security education and training only. All email content is fictional. Do not use it for any unlawful purpose.

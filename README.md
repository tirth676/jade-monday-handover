# Jade — Monday Morning Handover

**Call Hero Hackathon · UTS · 30 Sep 2026**

A voice-assisted Monday-morning screen for a clinic owner. It turns the weekend calls Jade (Call Hero's AI receptionist) answered into the few decisions the owner needs to make before 8:30. The goal is to clear it in 90 seconds.

> *"Jade answered 31 calls. This screen turns 3 cancellations into 3 saved patients — in one tap each."*

## The problem
Jade answers every call over the weekend, but on Monday at 8:00 the owner is left with 31 call logs and 90 seconds. Reading a report doesn't help her; she needs triage.

## What it does
| Feature | Description |
|---|---|
| ✦ **Ask Jade** | A spoken summary of about 86 words covering everything that matters |
| ▶ **Full voice briefing** | Jade reads out each item and highlights its card on screen as she speaks |
| 🎤 **Ask anything** | Type or speak a question such as "What's urgent?", "Any cancellations?" or "Who needs a callback?" |
| 🔴 **Do now** | Urgent pain, plus complaints that are escalating (repeat callers) |
| ♻️ **Fill freed slots** | Matches each cancelled slot automatically to a patient who couldn't get in, with urgency ranked first |
| 👉 **Delegate** | Follow-ups that reception can take on, each with one tap |
| 📋 **Heads-up** | Notes for the week: anxious patients, upsell interest, priority visits |
| 💡 **Insight** | Spots demand patterns, e.g. early-week demand exceeding capacity |

## Key insight
Three cancellations freed up slots, and three people wanted appointments and couldn't get one. Jade can't connect the two, but this screen does:

| Freed slot | Matched to | Why |
|---|---|---|
| Mon 9:00, Dr Foster | Peter Young | Urgent pain, so he can be seen **today** |
| Tue 11:00, Dr Foster | David Miller | Said he'd "try somewhere else" |
| Thu 14:00, Dr Bennett | Grace Scott | Called twice and asked to join the waitlist |

## How it works
- None of the output is hard-coded. Classification, grouping of repeat callers, slot matching and the summary are all computed from `data/weekend-calls.json`.
- Voice output uses the Web Speech API (`speechSynthesis`), preferring an Australian English voice.
- Voice input uses `webkitSpeechRecognition` with the `en-AU` locale (Chrome).
- The whole app is one `index.html` with no dependencies and no build step.

## Run locally
Open `index.html` in Chrome. That's all.

## Deploy
- **Vercel:** `npx vercel --prod`
- **Netlify:** drag the folder onto <https://app.netlify.com/drop>
- **GitHub Pages:** Settings → Pages → Deploy from branch → `main` / root

## Roadmap
- Send real SMS offers through Twilio when "Send offer" is tapped
- A "Teach Jade" button: the owner writes a rule once, and Jade escalates less each week
- Generate the summary with an LLM, and use a natural voice via ElevenLabs/Vapi
- Live integration with the clinic's practice management system (e.g. Cliniko)

## Structure
```
├── index.html              # full app (UI + logic + voice)
├── data/weekend-calls.json # challenge dataset (also embedded in index.html)
└── README.md
```

Built by Tirth Patel for the Call Hero Hackathon.

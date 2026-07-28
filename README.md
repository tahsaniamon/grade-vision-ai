<div align="center">

# 👁️ Grade Vision AI

**Read the script. Suggest the mark.**

AI-assisted handwriting grading for teachers — point your phone at a script, let AI read and suggest a mark in your own grading style. You stay in control.

Built for **Intra-IUB Hackathon · Programming Week Summer 2026** by **Koba Samsu Hackathon Team **

[Live Demo](#) · [Report Bug](../../issues) · [Request Feature](../../issues)

</div>

---

## 🧩 The Problem

Teachers spend hours re-reading handwritten scripts after every exam — grading is slow, inconsistent when tired or rushed, and leaves no record of *why* a mark was given. Grade Vision AI turns that stack of papers into a live, AI-assisted grading session: point your phone at each script, and get a transcribed reading, a suggested mark, and the reasoning behind it — in seconds, in your own grading style.

## ✨ Features

| | |
|---|---|
| 📷 **Phone as camera** | Scan a QR code — your phone becomes a live overhead scanner. No app, no cable, no dedicated hardware. |
| 🧮 **OpenCV cleanup** | Every frame is deskewed, perspective-corrected, and contrast-boosted in the browser before it reaches the AI. |
| ✨ **Gemini-powered reading** | Google Gemini transcribes the handwriting and evaluates the answer against the question. |
| 🎓 **Learns your style** | Upload a few previously graded scripts (or just correct a few AI suggestions) and it adapts to how *you* mark. |
| 📝 **Reasoned suggestions** | Every suggested mark comes with what was right, what was missing, and which concepts were skipped — not just a number. |
| ✅ **You decide** | Accept, override, or type your own mark. The AI assists; it never has final say. |
| 📊 **Gradebook & CSV export** | Every session's results land in a dashboard you can review and export. |

## 🛠️ Tech Stack

- **Frontend:** Single-file HTML/CSS/JS — no build step, no framework
- **AI:** Google Gemini 2.0 Flash (vision + language, called directly from the browser)
- **Computer Vision:** OpenCV.js (WASM) — runs entirely client-side
- **Backend:** Firebase (Authentication, Firestore, Realtime Database for the phone↔desktop camera relay)
- **Animation:** GSAP + ScrollTrigger (inlined, no CDN dependency)
- **Hosting:** Vercel

No server to maintain. Everything except the Gemini API call runs in the browser.

## 🚀 How It Works

1. **Set up once** — enter your subject and grading preferences; optionally upload a few old graded scripts.
2. **Connect your phone** — scan a QR code; your phone's camera streams live to your laptop.
3. **Capture & analyse** — OpenCV cleans the frame, Gemini reads and grades it, all in a couple of seconds.
4. **Accept, adjust, next** — confirm the AI's mark or type your own, save, move to the next script.

## 📦 Getting Started

This is a single static HTML file — there is no build step.

### Run locally
```bash
git clone https://github.com/<your-username>/grade-vision-ai.git
cd grade-vision-ai
# open index.html directly in a browser, or serve it:
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Configure Firebase
1. Create a project at [console.firebase.google.com](https://console.firebase.google.com)
2. Enable **Authentication** (Email/Password + Google), **Firestore**, and **Realtime Database**
3. Copy your web app config into the `firebaseConfig` block near the top of `index.html`
4. Publish `firestore.rules` and `database.rules.json` from this repo to your project's Rules tabs

### Add your Gemini key
Open the deployed app → **Setup** step → **Add your API key**. Get a free key at [aistudio.google.com/apikey](https://aistudio.google.com/apikey). The key is stored only in your browser — never committed to this repo.

### Deploy
```bash
npx vercel --prod
```
Or connect this repo at [vercel.com/new](https://vercel.com/new) for automatic deploys on every push.

## 📁 Repository Structure

```
grade-vision-ai/
├── index.html            # the entire application
├── firestore.rules       # Firestore security rules
├── database.rules.json   # Realtime Database security rules
├── vercel.json           # Vercel routing config
└── README.md
```

## 🔒 Privacy & Security

- Scripts and camera frames never leave the browser except for the direct call to Google's Gemini API.
- Each teacher's grading profile, sessions, and results are scoped to their own Firebase account (see `firestore.rules`).
- The Realtime Database camera relay is deliberately open (`gva_live/{sessionId}`) so a phone can stream to a desktop without a separate login — the trade-off is that a guessed session ID could read/write that live node. Fine for a pilot; tighten before wider deployment.

## 🗺️ Roadmap

- [ ] Move the Gemini call behind a lightweight backend to keep API keys off the client entirely
- [ ] Batch grading — queue multiple scripts before reviewing
- [ ] Multi-teacher classrooms and shared question banks

## 👥 Team

Built by ** Kuba Samsu ** for the Intra-IUB Hackathon, Programming Week Summer 2026, IUB Programming Club.

## 📄 License

MIT — see [LICENSE](LICENSE).

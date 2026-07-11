# NEXUS // CHANDAN

**An interactive digital identity — not a portfolio template.**

A single-file, dependency-free web experience for Chandan Nayak: cinematic boot sequence, a living animated background, a 3D skills galaxy, an AI "digital twin" that answers recruiter questions, immersive project case studies, a working terminal, and a hidden `sudo` easter egg.

Built with vanilla HTML, CSS, and JavaScript. No framework, no build step, no bundler — clone it and open it.

---

## ✨ Features

| Section | What it does |
|---|---|
| **Boot Sequence** | Terminal-style typed boot log, animated percentage counter, glitch effects, fade into the app |
| **Living Background** | Canvas-based neural particle network + animated aurora gradients + subtle parallax grid, all mouse-reactive |
| **Custom Cursor** | Magnetic hover on interactive elements, color shifts per section |
| **Floating Dock** | macOS-style navigation dock with magnetic hover, auto-hide on scroll, active-section highlighting |
| **Hero** | Cinematic typography, typed rotating role titles, CSS 3D floating orb |
| **AI Digital Twin** | A local chat assistant that answers natural questions ("Tell me about SepsisAlert," "Why should we hire him?") from a structured résumé data object |
| **Skills Galaxy** | Skills rendered as a real rotating 3D sphere (drag to orbit) instead of progress bars |
| **Project Case Studies** | Click-through modals: problem, architecture, stack, screenshots, challenges, lessons learned. SepsisAlert includes an animated AWS pipeline (IoT → Kinesis → Lambda → SageMaker → Bedrock → Alert) |
| **Experience + World Map** | Timeline of education/work plus an SVG map of where the work has happened |
| **Achievement Museum** | Certifications and milestones as a visual grid |
| **GitHub Signal** | Live fetch of public repo count, followers, and account age via the GitHub REST API |
| **Terminal** | A working command line — `about`, `projects`, `skills`, `resume`, `contact`, `whoami`, `clear` — plus a hidden `sudo hire chandan` command that triggers full hacker mode (Matrix rain overlay) |
| **Résumé Downloads** | Three tailored résumé variants (Cloud, AI, Security) generated and downloaded client-side |

---

## 🚀 Getting Started

No installation required.

```bash
git clone https://github.com/<your-username>/nexus-chandan.git
cd nexus-chandan
open nexus-chandan.html   # macOS
# or just double-click the file, or drag it into a browser
```

To develop with live reload, serve it locally instead of using `file://`, since the GitHub stats fetch and some fonts behave better over `http://`:

```bash
npx serve .
# or
python3 -m http.server 8000
```

Then visit `http://localhost:8000/nexus-chandan.html`.

### Deploying

It's a static file — deploy it anywhere that serves static HTML:

- **GitHub Pages**: push to a repo, enable Pages on the `main` branch, point it at `nexus-chandan.html` (rename to `index.html` for a root deploy)
- **Vercel / Netlify**: drag-and-drop deploy, zero config
- **Any static host / S3 bucket**: just upload the file

---

## 🎨 Customization

Everything content-related lives in **one place**: the `resumeData` and `resumeVariants` objects near the top of the `<script>` tag at the bottom of `nexus-chandan.html`. Edit those and the entire site updates — no need to touch markup or CSS.

```js
const resumeData = {
  name: "...",
  roles: [...],        // rotating hero subtitle
  whyHire: "...",       // AI twin's answer to "why hire him"
  skills: [...],        // powers the 3D skills galaxy
  projects: [...],      // powers project cards + case study modals
  timeline: [...],      // experience timeline
  mapLocations: [...],  // world map dots
  achievements: [...],  // achievement museum grid
  githubUsername: "..."
};

const resumeVariants = { cloud: `...`, ai: `...`, security: `...` };
```

### What's placeholder right now

This repo ships with **sample content** so the experience isn't empty out of the box. Before publishing, replace:

- [ ] `resumeData.projects` — only **SepsisAlert** is real; `CloudSentinel`, `PacketGuard`, and `CodeMesh` are placeholders and should be replaced or removed
- [ ] `resumeData.timeline` — sample education/work dates
- [ ] `resumeData.achievements` — sample certifications, marked `(sample)`
- [ ] `resumeData.githubUsername` — set to your real GitHub handle so the live stats widget resolves
- [ ] Contact details in the `#contact` section (email, LinkedIn, location)
- [ ] `resumeVariants` — swap the generated `.txt` placeholders for links to real PDF résumés
- [ ] Project modal **screenshot tiles** (`.screen-ph` divs) — swap for real `<img>` tags once you have screenshots

### Adding a new project

Add an object to `resumeData.projects`:

```js
{
  id: "my-project",
  tag: "Category · Stack",
  title: "Project Name",
  short: "One-sentence summary shown on the card.",
  stack: ["Tech", "Tech", "Tech"],
  problem: "What problem this solves and why it mattered.",
  architecture: "generic",   // or "pipeline" for an animated flow diagram like SepsisAlert
  lessons: "What you learned / what was hard."
}
```

### Adding a skill node

```js
{ n: "Skill Name", c: "cloud" }  // c: "cloud" | "ai" | "security" | "dev"
```

---

## 🗂 Project Structure

```
nexus-chandan.html   # the entire site: markup, styles, and logic in one file
README.md            # this file
```

Kept intentionally as a single file for zero-dependency portability — fork it, host it anywhere, no build pipeline to maintain.

---

## 🛠 Tech Notes

- **No frameworks** — vanilla JS, CSS custom properties, canvas 2D for the particle/neural background, CSS 3D transforms (fibonacci-sphere distribution) for the skills galaxy
- **Fonts**: Space Grotesk (display), Inter (body), JetBrains Mono (terminal/data) via Google Fonts
- Respects `prefers-reduced-motion`
- Custom cursor disables itself on touch devices
- GitHub stats use the public, unauthenticated GitHub REST API (`api.github.com/users/<handle>`) — rate-limited to 60 requests/hour per IP; falls back gracefully if the request fails

---

## 🔐 Easter Egg

Open the terminal section and type:

```
sudo hire chandan
```

---

## 📄 License

Personal portfolio project. Feel free to fork the structure and mechanics for your own site — please swap out the name, content, and résumé data rather than deploying it as-is.

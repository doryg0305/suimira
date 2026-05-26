# Suimira

**A live AR makeup mirror for Asian faces.**

Bring a filtered selfie of how you want to look — Suimira reverse-engineers it into step-by-step makeup placement projected onto your live face, with markers that follow your face in real-time as you turn your head.

> **Status**: v3.2 MVP shipped (May 2026). Solo-built using Claude (Anthropic) as engineering proxy. Pre-revenue, pre-incorporated. Validating with first ground-truth dataset.

---

## Why

Existing beauty AR tools (Perfect Corp, Meitu, GlowUp, ModiFace) focus on **virtual try-on** — projecting a look onto your face. None of them teach you how to **actually paint** the makeup yourself with honest awareness of what's achievable vs filter-only.

Suimira's positioning:

- **Reverse engineering**, not preset library: you bring the target, we figure out the steps.
- **Asian-first** face geometry calibration: existing tools default to Western face structure.
- **Honest realism**: distinguish makeup-achievable effects from filter-only (eye enlargement, pixel-blur skin) — a layer no competitor offers.

---

## What's built (v3.2, May 2026)

- **Live AR markers** — overlay highlight / contour / blush / eyeshadow / lip zones on your live webcam feed, markers follow face mesh in real-time.
- **4 makeup preset library** — 🍑 Korean warm pink sparkle / 🍓 coral tinted lip / ❄️ K-pop clean / 💧 bare-face glow.
- **Step-by-step tutorial mode** — pro-grade placement based on professional makeup artist reference (e.g., under-eye triangle highlight that beginners miss).
- **Marker shape upgrade** (v3.2): triangle highlight, wrap-around curves for nose contour, cream-blob shapes — designed to look like how pros actually paint, not abstract dots.
- **Ground-truth dataset #1**: 11 paired photos of founder (bare face / Meitu filter / actual makeup outcome) for filter-to-recipe calibration.

## Tech stack

| Layer | Tech |
|---|---|
| Face mesh detection | MediaPipe Face Landmarker (478 points, GPU delegate) |
| Rendering | HTML5 Canvas (no WebGL/Three.js dependency) |
| Markers | Triangle gradient fill / quadratic curve wrap / cream-blob ellipse / multi-point stroke |
| Mode switching | Upload photo (IMAGE runner) + Live webcam (VIDEO runner) |
| Deployment | Static — works in any browser, runs entirely client-side. No server, no data upload. |

## Try it

**Live demo**: [link coming after GitHub Pages deploy]

Or run locally:

```bash
git clone https://github.com/[your-username]/suimira.git
cd suimira
python3 -m http.server 8000
# open http://localhost:8000/
```

> ⚠️ Live webcam mode requires HTTPS (browser security). Localhost works; for mobile or sharing with friends, deploy to GitHub Pages / Cloudflare Pages / Vercel (all free, all HTTPS).

## Version history

| Version | Date | Highlights |
|---|---|---|
| v0 | 2026-05-21 | Single-canvas POC, sparse dot markers, live webcam mode |
| v1 | 2026-05-22 | Layer toggle (highlight / contour / blush) + step mode + detailed advice panel |
| v2 (deprecated) | 2026-05-25 | 3-panel filter pipeline experiment — abandoned (heavy filter overlay obscured marker positioning; pivoted back to v1 architecture) |
| **v3.0** | 2026-05-25 | v1 architecture + 4 preset chips + live tracking restored |
| **v3.1** | 2026-05-25 | Added eyeshadow / lip zones + pro-grade highlight positions (under-eye triangle, brow bone, forehead T) |
| **v3.2** | 2026-05-25 | Marker shape upgrade — triangle / wrap-curve / cream-blob (more anatomically truthful) |

Snapshots of every version live in `snapshots/` — never overwritten.

## Roadmap

Near (2-6 weeks):
- **Filter-vs-reality detection** — accept user-uploaded filter photo as target, classify which deltas are makeup-achievable vs filter-only. (Dataset designed for this; rule-based v1 first, then small classifier.)
- **3D occlusion handling** — markers currently bleed onto ears/hair at extreme side angles. MediaPipe's `z` axis exists; need to use it.
- **More presets** based on additional ground-truth pairs (rock smoky, wedding bridal, office natural).

Mid (3-6 months):
- Mobile-optimized standalone app (iOS first).
- Calibrated under-eye triangle / cheek apple shape per face geometry.
- 1000+ photo extended dataset with Asian face region annotations.

Long (6-12 months):
- WebGL shader pipeline for true 60fps mobile performance (current canvas runs ~25fps).
- Brand partnerships (color matching to actual product SKUs).

## Founder

**Dory Kuo** — UCLA BS Cognitive Science (GPA 3.72) → cancer research at UCLA David Geffen School of Medicine → Operations & Growth Analyst at Generation Next Fertility (Manhattan IVF clinic). Currently founding Suimira (Aug 2025 – present).

Built Suimira solo using Claude (Anthropic) as engineering proxy — partnership model: founder brings product taste + Asian beauty domain + dataset curation, Claude brings code-generation speed.

LinkedIn: [linkedin.com/in/dory-kuo](https://www.linkedin.com/in/dory-kuo/)
Email: doryg0305@gmail.com

## License

POC code in this repository is open source for review/research/learning purposes. Branding (Suimira name, logo, dataset images) reserved.

---

*If you're a Computer Vision / WebGL engineer interested in beauty tech for Asian markets — get in touch.*

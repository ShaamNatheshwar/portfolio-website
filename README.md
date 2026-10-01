# Shaamnatheshwar Sasikumar — Portfolio Website

A cinematic, single-page developer portfolio built with **HTML + Tailwind + Three.js + GSAP**. No build tools, no framework — just open `index.html` and it runs.

> **DevOps · Cloud · Observability** — Chennai, India
> AWS SAA-C03 · RHCSA · CKA

![Hero](https://img.shields.io/badge/stack-HTML%20·%20Tailwind%20·%20Three.js%20·%20GSAP-0B0B0F?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)
![No build](https://img.shields.io/badge/build-none-success?style=for-the-badge)

---

## ✨ Features

- **Interactive 3D particle field** rendered with Three.js — 5,000 points on a Gaussian-distributed sphere, custom GLSL shaders, soft additive blending.
- **Cursor-reactive cloud** — particles within 150 units of the mouse are pulled toward the cursor; the rest sway on a sin/cos noise field.
- **Generative line network** — ~880 line segments connect pre-paired particles and breathe with the field as it morphs.
- **Scroll miracle** — `ScrollTrigger` ties the camera zoom and field rotation to scroll progress so the 3D scene and hero text move in lockstep.
- **Cinematic text reveals** — every headline is split per-character and rolls in with a staggered skew-y animation; body copy uses a blur-to-focus transition.
- **Terminal-style cards** for experience and education, complete with the macOS-style traffic-light bar.
- **Magnetic buttons** that follow the cursor within a clamped radius.
- **Custom glow cursor** with `mix-blend-mode: screen` and a film-grain overlay (CSS only, zero image assets).
- **Fully responsive** and tab-switch aware (animation pauses when the tab is hidden to save battery).

---

## 🚀 Run Locally

### Option 1 — Just open the file

The site is a single static HTML file. Most things work by double-clicking it:

```bash
# macOS
open index.html

# Linux
xdg-open index.html

# Windows
start index.html
```

> ⚠️ Some browsers block `file://` requests for CDN scripts. If fonts or 3D don't appear, use Option 2.

### Option 2 — Local web server (recommended)

Any static server works. Pick one:

```bash
# Python 3 (already installed on macOS / most Linux)
python3 -m http.server 8000

# Node.js
npx serve .

# PHP
php -S localhost:8000

# Go
go run -e .
```

Then open **http://localhost:8000** in your browser.

That's it. No `npm install`, no `npm run build`, no bundler.

---

## 🛠 Customize

Everything you might want to tweak lives in `index.html`. The file is organized into clearly-commented regions:

| Section | What to edit |
| --- | --- |
| `<title>` and `<head>` | Page title, meta tags, font choices |
| `:root` CSS variables | Color palette (`--violet`, `--electric`, `--silver`, etc.) |
| `<nav class="top">` | Logo, nav links, CTA button |
| `<section id="hero">` | Name, headline, subhead, stat numbers |
| `<section id="experience">` | Terminal cards with role bullets |
| `<section id="work">` | Project cards (`.project-card`) |
| `<section id="skills">` | Skill chips and certification cards |
| `<section id="contact">` | Email, résumé link, socials |
| `THREE.JS` block | Particle count, palette, cursor force, scroll mapping |

### Change the particle count

```js
const PARTICLE_COUNT = 5000;  // lower to 1500 for older GPUs
```

### Change the palette

```js
const palette = [
  new THREE.Color('#4DA8FF'),  // electric blue
  new THREE.Color('#7A5CFF'),  // violet
  new THREE.Color('#C9C9D6'),  // silver
];
```

### Tweak scroll-driven camera

```js
camera.position.z = 400 - scrollProgress * 90;  // 0..90 zoom range
particles.rotation.y = twist * 0.6 + t * 0.04;
```

---

## 🏗 Tech Stack

| Layer | Library | Loaded via |
| --- | --- | --- |
| Layout & utilities | [Tailwind CSS](https://tailwindcss.com) | CDN |
| 3D scene | [Three.js r128](https://threejs.org) | CDN |
| Animations | [GSAP 3.12](https://greensock.com/gsap/) + ScrollTrigger | CDN |
| Display font | [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) | Google Fonts |
| Body font | [Inter](https://fonts.google.com/specimen/Inter) | Google Fonts |
| Mono font | [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) | Google Fonts |

All dependencies are pulled from public CDNs at runtime — there is nothing to install.

---

## 📦 Deploy

Any static host will work. A few one-click options:

- **GitHub Pages** — push to `main`, enable Pages in repo settings, point at `/` (root). Done.
- **Netlify** — drag the folder onto netlify.com/drop.
- **Vercel** — `vercel deploy` in the repo root.
- **Cloudflare Pages** — connect the repo, no build command needed.

No `dist/` folder, no build artifacts, no env vars.

### GitHub Pages in 30 seconds

```bash
# From the repo root
git checkout -b gh-pages
git push origin gh-pages
```

Then in GitHub → **Settings → Pages** → Source: `gh-pages` branch, `/ (root)`. Your site will be live at `https://shaamnatheshwar.github.io/portfolio-website/`.

---

## ⚡ Performance Notes

- **DPR capped at 2** — prevents retina screens from rendering 4× the pixels.
- **Resize is throttled** to one update per animation frame.
- **`requestAnimationFrame` pauses on `visibilitychange`** — the scene stops drawing when you switch tabs.
- **BufferGeometry with Float32Arrays** — no per-frame allocations in the hot loop.
- **Precomputed neighbor index** for the line network — avoids the O(n²) "find nearest" cost.
- All shaders are simple and fit comfortably in a single draw call per layer (particles + lines).

On a 2020-era laptop the scene holds a steady 60fps in Chrome and Firefox.

---

## 📁 Project Structure

```
portfolio-website/
├── index.html      # The entire site — HTML, CSS, JS, shaders, all-in-one
└── README.md       # You are here
```

That's the whole repo. 49 KB, one file.

---

## 📄 License

MIT — use it, fork it, ship it. Attribution appreciated but not required.

---

## 👤 About

Built by **Shaamnatheshwar Sasikumar** — DevOps & Cloud Engineer at Flex.
Specializing in Linux, AWS, Kubernetes, Terraform, and modernising legacy monitoring to the Prometheus / LGTM stack.

- LinkedIn: [linkedin.com/in/shaamnatheshwar](https://linkedin.com/in/shaamnatheshwar)
- Email: shaam.devops@gmail.com

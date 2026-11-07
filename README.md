# mukherjee96.github.io

Source code for [mukherjee96.github.io](https://mukherjee96.github.io).

Built with **Hugo** using a custom in-house fork of the StartBootstrap Resume theme.

---

## 🛠️ How to Update Content (No HTML Editing!)

All resume and portfolio content is managed via structured YAML files in the `data/` directory:

| Content Section | File to Edit |
| :--- | :--- |
| **Profile, Bio, & Social Links** | `data/profile.yaml` |
| **Skills & Categories** | `data/skills.yaml` |
| **Work Experience & Publications** | `data/experience.yaml` |
| **Portfolio & Projects** | `data/portfolio.yaml` |
| **Education & Achievements** | `data/education.yaml` |

When you edit any of these files and push to `master`, GitHub Actions automatically builds and deploys the updated website to GitHub Pages in seconds.

---

## 💻 Local Development

### Prerequisites
Install Hugo (Hugo Extended recommended):

```bash
# macOS (Homebrew)
brew install hugo
```

### Run Local Development Server
```bash
hugo server
```

Open [http://localhost:1313/](http://localhost:1313/) to view the site with instant live-reload.

### Build Static Site
```bash
hugo --minify
```
Output files will be generated in `public/`.

---

## 📁 Repository Structure

```text
├── .github/workflows/deploy.yml   # GitHub Actions deployment to GitHub Pages
├── content/_index.md              # Hugo homepage entry
├── data/                          # 👈 Edit content here
│   ├── profile.yaml
│   ├── skills.yaml
│   ├── experience.yaml
│   ├── portfolio.yaml
│   └── education.yaml
├── layouts/                       # Hugo HTML templates & partials
│   ├── _default/baseof.html
│   ├── index.html
│   └── partials/
├── static/                        # CSS, JS, fonts, images, and favicon
│   ├── favicon.png
│   └── assets/
├── hugo.yaml                      # Hugo configuration
└── DECISIONS.md                   # Architecture & technical decisions log
```

# Architecture and Technical Decisions

This document records the architectural and technology decisions for **mukherjee96.github.io**.

---

## 1. Static Site Generator: Hugo (over Astro)

* **Date:** November 2026
* **Status:** Accepted
* **Context:** The website is currently maintained by manually editing a monolithic 576-line HTML file (`index.html`). This is cumbersome and error-prone when adding or modifying resume items, skills, or portfolio entries. We evaluated modern static site generators (Astro vs. Hugo) to transition to a structured, data-driven workflow.
* **Decision:** Adopt **Hugo** and reject Astro.
* **Rationale:**
  * **Zero Dependency Overhead:** Hugo is distributed as a single standalone binary. It requires **no Node.js, no `npm`, and no `node_modules`**, completely eliminating npm package churn, `npm audit` warnings, peer dependency conflicts, and Dependabot notification fatigue.
  * **Longevity & Reproducibility:** By pinning the Hugo binary version in CI/CD (GitHub Actions), the site will build consistently years into the future without routine dependency upgrades.
  * **Instant Builds:** Hugo compiles the static site in milliseconds with zero cold-start delay.
  * **GitHub Pages Integration:** Native GitHub Actions support via official deployment workflows.

---

## 2. Theme Strategy: In-House Custom Fork of StartBootstrap Resume

* **Date:** November 2026
* **Status:** Accepted
* **Context:** The site originated from `startbootstrap-resume` but has evolved over years with custom visual tweaks: custom purple branding via CSS variables (`#500075`), profile avatar repositioned into the hero section, a 4-column categorized skills grid, a dedicated portfolio section with action buttons, custom top loader bar, and self-hosted fonts. Off-the-shelf Hugo themes (like `hugo-theme-clean-resume`) would overwrite these customizations and require extensive overrides.
* **Decision:** Treat the existing codebase as our **own in-house fork** of the StartBootstrap Resume theme.
* **Rationale:**
  * We maintain 100% control over design and styling.
  * Preserves existing custom CSS (`assets/css/resume.css` and `assets/css/constants.css`) and assets without breaking visual identity.
  * Leaves the door open to future styling and layout extensions without fighting third-party theme constraints.

---

## 3. Content Authoring: Data-Driven YAML Surface

* **Date:** November 2026
* **Status:** Accepted
* **Context:** Content updates should not require editing HTML markup, layout code, or template tags.
* **Decision:** Separate all site content into structured **YAML data files** in `data/`, with Markdown support enabled for rich text descriptions using Hugo's `markdownify`.
* **Data File Structure:**
  * `data/profile.yaml`: Personal bio, title, location, email, social links, meta descriptions.
  * `data/skills.yaml`: Skill categories (Languages, Web Technologies, Tools/Databases, Workflow) and items.
  * `data/experience.yaml`: Work history, roles, companies, employment dates, descriptions, and publications.
  * `data/portfolio.yaml`: Projects, tech stacks, feature bullet points, project URLs, and GitHub links.
  * `data/education.yaml`: Educational background, degrees, institutions, GPA, and honors/hackathons.
* **Rationale:**
  * Clean, human-readable YAML syntax.
  * Adding a job or project only requires copying a simple YAML block.
  * Markdown enabled inside YAML string fields (links, bold text, lists) for formatting flexibility without raw HTML.

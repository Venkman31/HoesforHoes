---
type: project
status: Archived
date: 2026
tags:
  - project
  - web-development
  - frontend
  - landing-page
  - ui-design
---

# Project: Hose for Hoes 🔥

## 📌 Overview
A mobile-first marketing landing page for a novelty firefighter-themed dating concept (originally "HoesforHoes", later rebranded to "Hose4Hoes"). The goal was to quickly stand up a single, self-contained promotional page — hero, "how it works", value proposition, features, and a call-to-action — with a bold, high-contrast visual identity. The project was ultimately archived: the deployed `index.html` and `README.md` were emptied out, but the complete source remains in git history.

## 🛠️ Tech Stack & Architecture
* **Languages & Frameworks:** HTML5, CSS3 (vanilla, no framework), Google Fonts (Oswald + Inter)
* **Database/Storage:** None — fully static, no backend or persistence
* **Architecture Style:** Static single-page site; all styles inlined in a single `index.html` with a mobile-first responsive layout

## 🎯 Skills Applied
*Active skills used or learned during this project:*
* `[[Skill - HTML]]` - Structured a semantic single-page layout (hero, sections, cards, CTA, footer)
* `[[Skill - CSS]]` - Hand-wrote all styling: gradients, rounded pill buttons, card components, custom typography
* `[[Skill - Responsive Web Design]]` - Mobile-first layout upgraded to desktop via a `min-width: 768px` media query
* `[[Skill - UI Design]]` - Defined a red/dark/light brand palette and consistent visual hierarchy with display + body fonts
* `[[Skill - Git]]` - Iterated through renames, uploads, and content removal across multiple commits

## 🧩 Connectors & Shared Concepts
*Concepts, tools, or patterns that link this project to other areas of my knowledge base:*
* `[[Connector - CSS Custom Properties]]` - Theming via `:root` variables (`--red`, `--dark`, `--light`, `--grey`)
* `[[Connector - Mobile-First Design]]` - Base styles target mobile, progressively enhanced for larger screens
* `[[Connector - Media Queries]]` - Breakpoint-driven layout adjustments
* `[[Connector - Google Fonts]]` - External webfont loading (Oswald / Inter) shared across web projects
* `[[Connector - Landing Page Pattern]]` - Hero → How It Works → Why → Features → CTA → Footer conversion funnel
* `[[Connector - CSS Flexbox]]` - Centered hero content via flex column layout
* `[[Connector - Static Site]]` - Self-contained, deploy-anywhere single HTML file

## 📈 Key Deliverables & Features
* **Full-screen Hero:** Overlaid gradient on a background image with headline, tagline, and dual CTA buttons (primary + outlined secondary).
* **"How It Works" Section:** Three numbered step cards (Sign Up → Match → Ignite).
* **Value Proposition ("Why") Section:** Dark-themed bulleted list highlighting selling points.
* **Features Section:** Card grid covering verification, safety/moderation, and local matching.
* **Call-to-Action + Footer:** Closing conversion prompt and a lightly humorous copyright footer.
* **Responsive Buttons:** Full-width on mobile, constrained and centered on desktop.

## 🧠 Lessons Learned & Technical Challenges
* **Challenge:** Keeping a single-file page visually cohesive without a CSS framework or design system.
* **Solution:** Centralized the theme in `:root` CSS custom properties and reused a small set of component classes (`.btn`, `.card`, `.section-title`) for consistency.
* **Takeaway:** `[[Concept - Design Tokens]]` — even a tiny static page benefits from centralizing colors and typography so the whole look can be adjusted from one place.

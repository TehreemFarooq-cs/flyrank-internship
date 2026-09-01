# Week 4: Stack Selection Rationale

## 1. Constraints & Requirements
* **Cost:** Free tools and hosting only.
* **Skill Level:** Comfortable with basic React, recently working with Next.js and TypeScript, and first-time exposure to the Vercel AI SDK.
* **Portfolio Scope:** A multi-page developer portfolio showcasing project case studies, code repos, and interactive demos.
* **Work Display Requirement:** Needs to cleanly present code snippets, responsive UI previews, and technical case studies without heavy overhead. Dynamic elements are minimal/not strictly required for launch.

---

## 2. Three Stack Options Considered

1. **No-Code Builder (Carrd / Framer / Canva)**
   * **How to build:** Drag-and-drop visual editors via a browser dashboard.
   * **Where to host:** Free tiers on Carrd or Framer subdomains.
   * **Backend required:** No.
   * **Trade-off:** Extremely fast to publish and great for visual layouts, but it provides zero code control, limits deep customization, and does not demonstrate technical software engineering skills.

2. **Plain HTML, CSS, and JavaScript (with AI assistance)**
   * **How to build:** Writing semantic HTML and modular CSS/JS files with AI guidance.
   * **Where to host:** Netlify Drop, GitHub Pages, or Vercel.
   * **Backend required:** No.
   * **Trade-off:** 100% transparent, lightning-fast, and deeply educational, but managing multiple pages and complex layouts manually can become tedious as the site grows.

3. **Next.js + TypeScript + Tailwind CSS (Vercel Framework Stack)**
   * **How to build:** Component-driven architecture using React components, TypeScript for type safety, and Tailwind CSS for styling.
   * **Where to host:** Vercel (Free Tier).
   * **Backend required:** Not strictly for a static portfolio, though API routes are available if needed later.
   * **Trade-off:** Highly professional and matches modern industry standards, but introduces build configurations and routing complexity that a simple static portfolio might not strictly need right away.

---

## 3. Decision & Rationale

**Chosen Stack:** Next.js + TypeScript + Tailwind CSS, hosted on **Vercel**.

* **Why this choice:** Even though a simple HTML/CSS setup is easier, I chose Next.js and Tailwind because it aligns closely with the modern web tools I am actively learning. Using Vercel allows me to seamlessly push updates via GitHub and maintain a professional developer workflow.
* **Can I maintain this:** Yes. Because I am already familiar with React basics and have worked with Next.js and Tailwind, I can comfortably read, modify, and troubleshoot the code structure with AI assistance without getting bogged down by complicated build errors.
* **Does it show my work well:** Perfectly. It allows me to embed responsive layouts, clean typography for case studies, and code blocks that accurately reflect front-end engineering competencies.

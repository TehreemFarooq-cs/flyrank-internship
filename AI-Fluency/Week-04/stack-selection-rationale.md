# Week 4: Stack Selection Rationale

## 1. Constraints & Requirements

* **Cost:** Free tools and hosting only.
* **Skill Level:** Comfortable with basic React, recently working with Next.js and TypeScript, and first-time exposure to the Vercel AI SDK.
* **Portfolio Scope:** A multi-page developer portfolio showcasing project case studies, code repos, and interactive demos.
* **Work Display Requirement:** Needs to cleanly present code snippets, responsive UI previews, and technical case studies without heavy overhead. Dynamic elements are minimal/not strictly required for launch.
* **Backend needed at launch:** No. Everything ships as a static site. If I add something dynamic later (a contact form, an interactive demo endpoint), I can bolt it on without switching stacks.

---

## 2. Three Stack Options Considered

1. **No-Code Builder (Carrd / Framer / Canva)**
   * **How to build:** Drag-and-drop visual editors via a browser dashboard.
   * **Where to host:** Free tiers on Carrd or Framer subdomains (Carrd's free tier is the more usable of the two — Framer's free tier is fairly restrictive, no custom domain).
   * **Backend required:** No.
   * **Trade-off:** Extremely fast to publish and great for visual layouts, but it provides zero code control, limits deep customization, and does not demonstrate technical software engineering skills.

2. **Plain HTML, CSS, and JavaScript (with AI assistance)**
   * **How to build:** Writing semantic HTML and modular CSS/JS files with AI guidance.
   * **Where to host:** Netlify Drop, GitHub Pages, or Vercel.
   * **Backend required:** No.
   * **Trade-off:** 100% transparent, lightning-fast, and deeply educational, but managing multiple pages and complex layouts manually gets tedious as the site grows — every case study page means hand-copying nav/header/footer markup.

3. **Next.js + TypeScript + Tailwind CSS (Vercel Framework Stack)**
   * **How to build:** Component-driven architecture using React components, TypeScript for type safety, and Tailwind CSS for styling.
   * **Where to host:** Vercel (Free Tier).
   * **Backend required:** No, not for a static portfolio. API routes exist and are available later if I want something dynamic, but I'm not turning them on now.
   * **Trade-off:** Highly professional and matches modern industry standards, but introduces build configuration and routing complexity that a simple static portfolio doesn't strictly need right away.

---

## 3. Pressure-Testing the Front-Runner (Next.js + Tailwind on Vercel)

* **What breaks if I pick the simplest option (plain HTML/CSS) instead?**
  Nothing breaks exactly, but it stops scaling well. Once I have several case study pages that share layout (nav, footer, project card structure), copy-pasting markup by hand across files gets error-prone and slow to update.

* **What do I actually maintain if I pick the most powerful option?**
  Real ongoing cost, not zero: build configuration, occasional dependency updates, routing setup, and the possibility of build errors when something in the toolchain shifts. I'm accepting that trade for the reusability and structure I get in return.

* **Can I finish in two weeks?**
  Yes. This isn't a from-scratch learning curve for me — I already have working React/Next.js/TypeScript experience, so I'm applying skills I have rather than learning the stack and building at the same time.

* **Does it show my work the way it needs to be shown?**
  Yes, and better than the alternatives. Code snippets, responsive UI previews, and case studies all render cleanly as React components. The no-code option fails this requirement outright since it can't demonstrate engineering skill, and plain HTML/CSS can do it but with more manual repetition per page.

---

## 4. Decision & Rationale

**Chosen Stack:** Next.js + TypeScript + Tailwind CSS, hosted on **Vercel**.

**Backend at launch:** Not needed. This stays a static site pushed through Vercel. API routes stay available if I want to add something dynamic down the line, but I'm not building that now.

**Why this choice:** Plain HTML/CSS would honestly be the easier and faster road, and I considered it seriously. But I picked Next.js and Tailwind because it's the stack I'm already actively learning and using, and a portfolio built with it doubles as proof I can work with the tools I claim to know. Pushing updates through GitHub to Vercel also keeps me in a normal developer workflow instead of a one-off publishing process I'll have to relearn later.

**Can I maintain this:** Yes. I already know React basics and have hands-on time with Next.js and Tailwind, so I can read, modify, and debug the project structure myself, with AI as backup when I hit something unfamiliar rather than being fully dependent on it.

**Does it show my work well:** Yes. It lets me embed responsive layouts, real code blocks, and structured case study pages in a way that actually reflects front-end engineering work — not just a static description of it.

**The two I didn't pick, and why:**
- *No-code (Carrd/Framer):* fastest to publish, but gives up all code control and doesn't demonstrate the technical skills this portfolio exists to prove.
- *Plain HTML/CSS/JS:* the honest "simplest" choice and genuinely tempting for how fast and low-maintenance it is, but it would mean hand-managing repeated layout across multiple case study pages, and it doesn't showcase the modern tooling I'm actually building experience in.

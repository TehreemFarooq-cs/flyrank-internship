# The Prompt Ladder: Front-End AI Engineering

## Baseline (Version 0)
* **The Prompt:** Build a web app.
* **The Output:** A generic response asking me what kind of app I want to build and listing basic technologies like HTML, CSS, and JavaScript.
* **The Four Notes:**
  * **What changed in the prompt:** Nothing, this is the starting baseline.
  * **What improved in the output:** Nothing; it is completely vague and unhelpful.
  * **What still failed:** It lacks any subject matter, tech stack, target user, or functional requirements.
  * **What you would try next:** Add a clear goal specifying what the app actually does.

---

## Version 1: Clearer Goal
* **The Prompt:** Build a React and TypeScript web app that functions as a virtual bookshelf to track reading progress.
* **The Output:** A basic boilerplate code structure with a simple App component and a list of book objects.
* **The Four Notes:**
  * **What changed in the prompt:** Added a specific goal, tech stack, and application type.
  * **What improved in the output:** It stopped asking generic questions and generated actual, functional React/TypeScript component code.
  * **What still failed:** The UI styling is completely missing, and it didn't include any external data fetching or API integration.
  * **What you would try next:** Add real context by integrating an external API (like Open Library).

---

## Version 2: Real Context
* **The Prompt:** Build a React and TypeScript web app that functions as a virtual bookshelf to track reading progress. Integrate the Open Library API to search for books, but include request abort timeouts and payload limits to handle slow network responses.
* **The Output:** A more detailed component that includes `fetch` calls to the Open Library search endpoint, basic error handling, and search input states.
* **The Four Notes:**
  * **What changed in the prompt:** Added real context regarding external API integration and edge-case handling (timeouts/payloads).
  * **What improved in the output:** It generated practical network handling code instead of just mock arrays.
  * **What still failed:** The UI layout is messy, lacks styling structure, and the search results overflow without proper fallback UI for missing cover images.
  * **What you would try next:** Add a specified output format and UI constraints.

---

## Version 3: Constraints & Specified Output Format
* **The Prompt:** Build a React and TypeScript web app that functions as a virtual bookshelf to track reading progress. Integrate the Open Library API to search for books, with request abort timeouts and payload limits. Format the output as clean, modular component files separated into `App.tsx`, `BookSearch.tsx`, and `ShelfList.tsx`, and constrain styling to Tailwind CSS utility classes without external UI libraries.
* **The Output:** Modular code split across three separate code blocks with Tailwind classes applied directly to the JSX.
* **The Four Notes:**
  * **What changed in the prompt:** Added output format (file separation) and constraints (Tailwind CSS only, no heavy UI libraries).
  * **What improved in the output:** The code is structured into logical, maintainable files rather than one giant monolithic component.
  * **What still failed:** This actually made it worse in one aspect: the generated code omitted TypeScript interface definitions for the Open Library JSON response, causing type errors when trying to map the search results.
  * **What you would try next:** Add strict quality criteria and type definition requirements.

---

## Version 4: Quality Criteria & Type Definitions
* **The Prompt:** Build a React and TypeScript web app that functions as a virtual bookshelf to track reading progress. Integrate the Open Library API to search for books, with request abort timeouts and payload limits. Format the output as clean, modular component files (`App.tsx`, `BookSearch.tsx`, `ShelfList.tsx`), constrained to Tailwind CSS. Quality criteria: Every API response must be fully typed with explicit TypeScript interfaces, and image fallbacks must be handled gracefully if a book cover is missing.
* **The Output:** Clean component files featuring explicit `interface Book` definitions and ternary checks for missing cover image URLs.
* **The Four Notes:**
  * **What changed in the prompt:** Added quality criteria focusing on strict TypeScript typing and defensive UI rendering (image fallbacks).
  * **What improved in the output:** The compilation errors from Version 3 disappeared, and the code handles missing data gracefully without breaking the layout.
  * **What still failed:** It lacks usage instructions or setup steps on how to run it locally with Vite.
  * **What you would try next:** Add verification requirements and execution steps.

---

## Version 5: Verification Requirements (Final Prompt)
* **The Prompt:** Build a React and TypeScript web app that functions as a virtual bookshelf to track reading progress. Integrate the Open Library API to search for books, with request abort timeouts and payload limits. Format the output as clean, modular component files (`App.tsx`, `BookSearch.tsx`, `ShelfList.tsx`), constrained to Tailwind CSS. Quality criteria: Every API response must be fully typed with explicit TypeScript interfaces, and image fallbacks must be handled gracefully. Verification requirement: Include a short terminal command guide and package dependencies list at the end so it can be run immediately with Vite.
* **The Output:** Fully typed React components, Tailwind styling, robust API error handling, image fallbacks, and a clear setup guide with Vite and npm commands.
* **The Four Notes:**
  * **What changed in the prompt:** Added verification requirements (setup commands and dependency lists).
  * **What improved in the output:** The response went from a code snippet to a complete, runnable, production-ready engineering artifact.
  * **What still failed:** Nothing significant for a single-prompt generation scope; the output is complete and immediately usable.
  * **What you would try next:** Save this structure as a reusable template.

---

## Final Reusable Prompt

```markdown
Build a React and TypeScript web app for [SPECIFY APP PURPOSE, e.g., tracking reading progress / managing medication inventory]. 
Integrate [SPECIFY API OR DATA SOURCE], including error handling and payload limits. 
Format the output as clean, modular component files with clear file headers. 
Constrain styling to [SPECIFY CSS APPROACH, e.g., Tailwind CSS] without external UI component libraries. 
Quality criteria: Every data model and API response must have explicit TypeScript interfaces, and missing assets must include fallback UI states. 
Verification requirement: Include the required package dependencies and a short terminal command guide to run the code locally.

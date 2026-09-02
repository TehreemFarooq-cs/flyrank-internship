# Agent Concepts, Workflows and Model Context Protocol (MCP)

## 1. What is an Agent?
The main difference between a regular workflow and an AI agent comes down to one question: who decides what happens next? 

In a standard workflow, the path is hardcoded. A human sets up every single step, order and rule ahead of time, and the system just runs through them one by one. An agent works differently. It runs in a loop where the AI actually looks at what is happening, figures out the results and decides its next move on its own. While a workflow follows a strict script, an agent adapts based on what it sees along the way.

## 2. Classifying My FL-04 Pipeline
My FL-04 pipeline is definitely a workflow. To break down what it does: I add a source to NotebookLM, run a single fixed prompt to get notes in a specific four-section format (TL;DR, Key Concepts, Code/API Specifics, Gotchas/Open Questions), and then I manually review the output and copy it into Google Docs. 

Every step and its exact order were decided by me beforehand, not the model. NotebookLM never decided on its own to look for extra sources, skip a section, or change how it worked; it just ran the exact same instructions for every single input I gave it. 

This isn't a bad thing. In software development, one should always start with the simplest solution that works. For a straightforward task like summarizing study notes, a reliable, step-by-step workflow is much better than dealing with the unpredictability of an agent.

## 3. What is MCP?
The Model Context Protocol (MCP) acts like a standardized "USB-C port for AI apps." It gives AI a universal way to connect securely to outside tools, local files and live services without needing a bunch of custom, one-off integrations. MCP has three main parts:

* **Tools:** Functions the model controls. The AI decides when and how to use them based on conversational context.
* **Resources:** Data the app controls. The app decides what files or info to feed into the context.
* **Prompts:** Shortcuts and templates that the user controls to guide things.

When I tested this using Claude connected to my Google Drive, actions like running `search_files` and reading specific documents were actual tool calls. The model looked at my prompt and decided when to pull live data (such as finding old files like *Enzymes.pdf* or reading the raw text of *His First Flight.pdf*) instead of just guessing or relying only on its built-in training data.

## 4. Upgrading the Pipeline to an Agent
To turn this fixed pipeline into a real agent, the system would need the ability to control its own steps instead of following a straight line. A concrete upgrade for this pipeline would be adding an autonomous search and check loop:

* **Dynamic Source Gathering:** Instead of me having to manually find and upload files, the pipeline would have MCP search tools. If the model realizes it's missing some context while writing notes, it could search my drive or a database and grab the extra file on its own.
* **Evaluation & Iteration Loop:** Instead of just writing the notes once and stopping, the model could run a self-check step to compare its output against a checklist. If it spots missing sections or weak points, it could loop back, fetch more info and fix the draft by itself before showing it to me.

This changes things because the AI decides when the job is actually done based on quality, rather than just running a fixed number of steps.

## 5. Conclusion
A straightforward workflow is still the best choice for predictable tasks where one wants speed, low cost and total reliability. Agents add extra complexity and overhead, so they are really only worth it for open-ended problems where the AI has to deal with the unknown and figure things out on the fly.

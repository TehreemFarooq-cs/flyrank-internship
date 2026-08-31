# Prompt Iteration Log: Real Task Prompting Fundamentals

## Task Selected
* **Task Description:** Converting plain JavaScript code into strictly typed TypeScript files (Task #7 from FL-01 audit).

---

## Version 0: Naive Baseline
* **Prompt:** Convert this JavaScript to TypeScript.
* **Output:** A code block containing the converted file, but missing explicit interfaces for complex nested objects, relying on `any` types for function parameters, and using loose type assertions.
* **Iteration Note:** 
  * *Technique Applied:* None (Naive baseline).
  * *Observed Output Difference:* The AI provided a generic type conversion that immediately threw TypeScript compiler errors due to implicit `any` definitions and missing structural types for nested data objects.

---

## Version 1: Role Assignment
* **Prompt:** You are a senior front-end software architect specializing in strict enterprise TypeScript codebases. Convert this JavaScript to TypeScript.
* **Output:** The code block improved slightly by adding descriptive type names, but it still defaulted to `any` types for untyped function callbacks and external event objects.
* **Iteration Note:** 
  * *Technique Applied:* Role Assignment.
  * *Observed Output Difference:* Establishing a persona made the code cleaner and more readable, but it didn't eliminate loose typing on complex parameters because boundaries weren't explicitly defined.

---

## Version 2: Context and Motivation
* **Prompt:** You are a senior front-end software architect specializing in strict enterprise TypeScript codebases. Convert this JavaScript to TypeScript for a production React Native application where runtime type safety prevents mobile crashes and state corruption. Convert this JavaScript file.
* **Output:** The output introduced basic interface definitions for state objects, but still included broad union types and skipped edge-case handling for optional parameters.
* **Iteration Note:** 
  * *Technique Applied:* Context and Motivation.
  * *Observed Output Difference:* Providing application context shifted the AI toward producing interface definitions instead of inline type aliases, but it still lacked strict compiler rule compliance (`noImplicitAny`).

---

## Version 3: Few-Shot Examples
* **Prompt:** You are a senior front-end software architect specializing in strict enterprise TypeScript codebases. Convert JavaScript to TypeScript for a production React Native application. Follow this conversion pattern:
  * *Input JS:* `function renderUser(user) { return user.name; }`
  * *Output TS:* `interface User { id: string; name: string; } function renderUser(user: User): string { return user.name; }`
  Convert this target JavaScript file using this exact rigor.
* **Output:** The output strictly adhered to the explicit interface pattern shown in the example, stopping the usage of loose parameter types.
* **Iteration Note:** 
  * *Technique Applied:* Few-Shot Examples.
  * *Observed Output Difference:* Providing a concrete input/output example successfully eliminated implicit `any` types and forced the model to generate explicit top-level interfaces.

---

## Version 4: Output Structure
* **Prompt:** You are a senior front-end software architect specializing in strict enterprise TypeScript codebases. Convert JavaScript to TypeScript for a production React Native application. Follow this pattern: [Insert Few-Shot Example]. Structure your response into two distinct markdown sections: 
  1. **Interfaces & Types:** All explicit TypeScript interfaces and type aliases.
  2. **Refactored Code:** The fully typed implementation using the defined interfaces.
  Convert this target JavaScript file.
* **Output:** The output successfully separated interface declarations from implementation logic, making the code clean and easy to modularize into type definition files.
* **Iteration Note:** 
  * *Technique Applied:* Output Structure.
  * *Observed Output Difference:* Forcing structural separation stopped the AI from cluttering component logic with inline type definitions, though edge cases in complex asynchronous functions were occasionally missed.

---

## Version 5: Step Decomposition (Final Prompt)
* **Prompt:** You are a senior front-end software architect specializing in strict enterprise TypeScript codebases. Convert JavaScript to TypeScript for a production React Native application by following these sequential steps:
  1. Analyze the raw JavaScript file to identify all data structures, parameters, and return types.
  2. Write explicit TypeScript interfaces for every data model without using `any` or `Record<string, unknown>`.
  3. Refactor the functions step-by-step, applying strict typing to parameters and return values.
  4. Verify that the final code complies with strict TypeScript compiler options.
  Structure your final response into two distinct sections: **1. Interfaces & Types** and **2. Refactored Code**. Convert this target JavaScript file.
* **Output:** A pristine, production-ready TypeScript module with completely decoupled, rigorous interface declarations and zero implicit type gaps.
* **Iteration Note:** 
  * *Technique Applied:* Step Decomposition.
  * *Observed Output Difference:* Breaking down the conversion into sequential logical gates eliminated all lingering type safety bugs, ensuring complete compilation readiness on the first pass.

---

## Cross-Model Comparison (Claude vs. ChatGPT)
* **Claude (Claude 3.5 Sonnet):** Produced cleaner modular structures, naturally avoided implicit `any` types even without strict few-shot enforcement in earlier versions, and maintained idiomatic React Native patterns.
* **ChatGPT (GPT-4o):** Required the explicit step decomposition and few-shot examples to match Claude's rigor; otherwise, it tended to fall back on `Record<string, any>` types to bypass complex object structures quickly.

---

## Final Reusable Prompt Template

```markdown
You are a senior front-end software architect specializing in strict enterprise TypeScript codebases. Convert the provided JavaScript file to strict TypeScript for a production application by following these sequential steps:
1. Analyze the raw JavaScript code to identify all data models, parameters, and return types.
2. Write explicit TypeScript interfaces for every data structure without using `any`.
3. Refactor the implementation step-by-step, applying strict typing to all functions, hooks, and props.

Follow this interface convention:
- Input JS: [INSERT EXAMPLE JS]
- Output TS: [INSERT EXAMPLE TS]

Structure your final response into two distinct markdown sections:
1. **Interfaces & Types**
2. **Refactored Code**

Target JavaScript code to convert:
[INSERT JAVASCRIPT CODE HERE]

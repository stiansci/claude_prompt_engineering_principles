# A Comprehensive Guide to Claude Prompt Engineering Principles

## Table of Contents

- [Chapter 1: Basic Prompt Structure](#chapter-1-basic-prompt-structure)
- [Chapter 2: Being Clear and Direct](#chapter-2-being-clear-and-direct)
- [Chapter 3: Assigning Roles (Role Prompting)](#chapter-3-assigning-roles-role-prompting)
- [Chapter 4: Separating Data and Instructions](#chapter-4-separating-data-and-instructions)
- [Chapter 5: Formatting Output and Speaking for Claude](#chapter-5-formatting-output-and-speaking-for-claude)
- [Chapter 6: Precognition (Thinking Step-by-Step)](#chapter-6-precognition-thinking-step-by-step)
- [Chapter 7: Using Examples (Few-Shot Prompting)](#chapter-7-using-examples-few-shot-prompting)
- [Chapter 8: Avoiding Hallucinations](#chapter-8-avoiding-hallucinations)
- [Chapter 9: Complex Prompts from Scratch](#chapter-9-complex-prompts-from-scratch)
- [Chapter 10: Advanced Techniques](#chapter-10-advanced-techniques)

---

## Chapter 1: Basic Prompt Structure

*   **Use Alternating Roles:** Prompts must use an alternating sequence of `user` and `assistant` conversational turns. The first message must always have the `user` role.
*   **Use System Prompts for Context:** A system prompt is the ideal place to provide high-level context, instructions, rules, or guidelines that should apply to the entire conversation. A well-written system prompt can significantly improve Claude's performance and ability to follow instructions.

---

## Chapter 2: Being Clear and Direct

*   **Give Clear and Direct Instructions:** Claude has no context beyond what you provide. Instruct it as you would a new person on a task—be explicit, direct, and avoid ambiguity. If a human would be confused by your instructions, Claude will be too.
*   **Request Specific Behavior:** If you want Claude to behave in a certain way, ask for it directly. For example, to avoid conversational filler, instruct it to "Skip the preamble; go straight into the poem."
*   **Force a Decision:** If Claude provides a non-committal or balanced answer, you can get a definitive one by explicitly asking it to choose, e.g., "If you absolutely had to pick one, who would it be?"

---

## Chapter 3: Assigning Roles (Role Prompting)

*   **Assign a Role or Persona:** Instructing Claude to adopt a specific role (e.g., "You are a logic bot," "You are a friendly cat") can significantly improve its performance and tailor its response style, tone, and content.
*   **Provide Detailed Context for the Role:** The more detail you provide about the role, the better Claude will inhabit it. Consider the role's expertise, perspective, and even its intended audience.
*   **Use Role Prompting for Complex Tasks:** Assigning an expert role can make Claude better at performing math, logic, and other complex reasoning tasks.

---

## Chapter 4: Separating Data and Instructions

*   **Use Prompt Templates:** For repetitive tasks, separate the fixed instructions (the template) from the variable data. This allows you to reuse the core prompt with different inputs.
*   **Clearly Delineate Data from Instructions:** It is critical to make sure Claude knows which part of the prompt is the instruction and which part is the data it needs to process.
*   **Use XML Tags to Enclose Data:** The most reliable way to separate data from instructions is to wrap the data in XML tags (e.g., `<document>`, `</document>`). Claude is specifically trained to recognize this structure, which prevents it from misinterpreting your data as part of the instructions.

---

## Chapter 5: Formatting Output and Speaking for Claude

*   **Request a Specific Output Format:** You can control how Claude formats its response by explicitly asking for it. For example, tell Claude to "Put the poem in `<haiku>` tags" or "Format the output as a JSON object."
*   **Use XML Tags for Programmatic Parsing:** Asking Claude to wrap its final output in XML tags makes the response easy to parse and extract programmatically, separating the desired content from any conversational filler.
*   **Prefill the Assistant's Response:** A powerful technique to force a specific format is to "speak for Claude" by providing the beginning of its response in the `assistant` turn. For example, starting the assistant turn with `<haiku>` or `{` strongly compels Claude to generate a haiku or a JSON object, respectively.

---

## Chapter 6: Precognition (Thinking Step-by-Step)

*   **Instruct Claude to Think Step-by-Step:** For complex tasks that require reasoning, instruct Claude to "think step-by-step" or lay out its reasoning process before giving the final answer.
*   **Thinking Must Be "Out Loud":** The act of writing down the reasoning steps is what improves Claude's accuracy. You cannot ask it to "think silently"; the thinking process must be part of the generated output.
*   **Be Mindful of Order Bias:** Claude can sometimes be sensitive to the order in which you present options and may be more likely to choose the second of two options.

---

## Chapter 7: Using Examples (Few-Shot Prompting)

*   **Provide Concrete Examples:** One of the most effective ways to guide Claude is to provide one or more examples of the desired behavior. This is known as "few-shot prompting."
*   **Use Examples for Both Content and Format:** Examples can demonstrate the correct answer, the desired tone, and the exact output format you require. Often, showing Claude an example is easier and more effective than writing out complex instructions.

---

## Chapter 8: Avoiding Hallucinations

*   **Give Claude an "Out":** To reduce the chances of Claude making up information (hallucinating), explicitly give it permission to state when it doesn't know an answer. For example, "If you don't know the answer, say so."
*   **Require Evidence-Based Answers:** When asking questions about a provided document, instruct Claude to first find and extract relevant quotes from the text. Then, instruct it to base its final answer only on those quotes. This grounds the response in the provided source material.
*   **Use Low Temperature:** For factual tasks, set the `temperature` parameter to a low value (like 0.0) to make responses more deterministic and less creative, which can help reduce hallucinations.

---

## Chapter 9: Complex Prompts from Scratch

*   **Structure Complex Prompts with Key Elements:** For complex tasks, build your prompt using a structured approach. A good starting point is to include these elements in order: Role/Task Context, Tone, Rules, Examples, Input Data, and finally, the Immediate Task Request.
*   **Place the Final Question at the End:** The most important instruction—the specific question or task for Claude to perform—should be placed at or near the end of the prompt to ensure it is given the most weight.

---

## Chapter 10: Advanced Techniques

*   **Chaining Prompts:** Break down a complex task into a sequence of simpler prompts. The output of one prompt becomes the input for the next, creating a powerful processing pipeline. This is useful for refining, correcting, or building upon previous generations.
*   **Tool Use (Function Calling):** Allow Claude to interact with external tools (like APIs or databases). This involves defining the tools in the prompt, having Claude output a structured request to use a tool, executing that tool in your code, and feeding the result back to Claude to synthesize a final answer.
*   **Search & Retrieval (RAG):** Augment Claude's knowledge by retrieving relevant information from an external source (like a document database) and providing that information as context within the prompt. Instruct Claude to use only the provided context to answer the user's question, which improves accuracy and relevance.
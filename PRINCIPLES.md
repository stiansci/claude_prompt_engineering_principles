# A Comprehensive Guide to Claude Prompt Engineering Principles (Enhanced with Examples)

This guide provides a set of principles for getting the best possible results from Claude. Each chapter has been enhanced with concrete examples to illustrate the concepts and help you become a more effective prompt engineer.

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

### Use Alternating Roles
Prompts must use an alternating sequence of `user` and `assistant` conversational turns. The first message must always have the `user` role. This format helps Claude understand the flow of the conversation.

### Use System Prompts for Context
A system prompt is the ideal place to provide high-level context, instructions, rules, or guidelines that should apply to the entire conversation. A well-written system prompt can significantly improve Claude's performance and ability to follow instructions. Use the system prompt mainly for high-level scene-setting and put most of your specific instructions in the user prompts.

**Example:**

```
<system>
You are a writing assistant that follows my personal writing rules:
1. Use plain language.
2. Keep sentences short.
3. Avoid clichés and hype.
4. Be clear and straightforward.
5. Write like you speak.
</system>

<user>
Write a newsletter about how to write faster with AI.
</user>
```

---

## Chapter 2: Being Clear and Direct

### Give Clear and Direct Instructions
Claude has no context beyond what you provide. Instruct it as you would a new person on a task—be explicit, direct, and avoid ambiguity. If a human would be confused by your instructions, Claude will be too.

**Vague Prompt:**
> "Summarize the text."

**Clear and Direct Prompt:**
> "Summarize the following text in three bullet points, focusing on the main arguments and conclusions."

### Request Specific Behavior
If you want Claude to behave in a certain way, ask for it directly. For example, instead of saying "be concise," it's better to give a specific sentence range like "Limit your response to 2–3 sentences".

**Example:**
> "Skip the preamble; go straight into the poem."

### Force a Decision
If Claude provides a non-committal or balanced answer, you can get a definitive one by explicitly asking it to choose.

**Example:**
> "If you absolutely had to pick one, who would be the more influential artist: Leonardo da Vinci or Michelangelo?"

---

## Chapter 3: Assigning Roles (Role Prompting)

### Assign a Role or Persona
Instructing Claude to adopt a specific role can significantly improve its performance and tailor its response style, tone, and content.

**Example:**
> "You are a senior data analyst. Summarize the provided dataset into 3 key insights, each backed by a numeric trend. Keep sentences under 20 words."

### Provide Detailed Context for the Role
The more detail you provide about the role, the better Claude will inhabit it. Consider the role's expertise, perspective, and even its intended audience.

**Example:**
> "You are a historian specializing in the Roman Empire, writing for a high school audience. Explain the causes of the fall of the Western Roman Empire in a way that is engaging and easy to understand."

### Use Role Prompting for Complex Tasks
Assigning an expert role can make Claude better at performing math, logic, and other complex reasoning tasks.

**Example:**
> "You are a logic bot. Analyze the following argument and identify any logical fallacies. Explain your reasoning for each fallacy found."

---

## Chapter 4: Separating Data and Instructions

### Use Prompt Templates
For repetitive tasks, separate the fixed instructions (the template) from the variable data. This allows you to reuse the core prompt with different inputs.

### Clearly Delineate Data from Instructions
It is critical to make sure Claude knows which part of the prompt is the instruction and which part is the data it needs to process.

### Use XML Tags to Enclose Data
The most reliable way to separate data from instructions is to wrap the data in XML tags (e.g., `<document>`, `</document>`). Claude has been trained to recognize and respond to XML-style tags, which helps separate instructions, examples, and inputs more effectively.

**Example:**
```
<user>
Summarize the main ideas from the provided text.

<text>
The text to be summarized goes here. It can be a long article, a report, or any other piece of text.
</text>
</user>
```

You can use any names you like for these tags; what's important is the `<>` and `</>` format.

---

## Chapter 5: Formatting Output and Speaking for Claude

### Request a Specific Output Format
You can control how Claude formats its response by explicitly asking for it.

**Example:**
> "Put the poem in `<haiku>` tags."
> "Format the output as a JSON object."

### Use XML Tags for Programmatic Parsing
Asking Claude to wrap its final output in XML tags makes the response easy to parse and extract programmatically, separating the desired content from any conversational filler.

**Example:**
```
<user>
Extract the names of all the people mentioned in this article and list them in XML tags.

<article>
John Doe and Jane Smith attended the conference.
</article>
</user>

<assistant>
<people>
<person>John Doe</person>
<person>Jane Smith</person>
</people>
</assistant>
```

### Prefill the Assistant's Response
A powerful technique to force a specific format is to "speak for Claude" by providing the beginning of its response in the `assistant` turn. This is also known as "prefilling".

**Example:**
To compel Claude to generate a JSON object, you can structure your prompt like this:
```
<user>
Please convert the unstructured data into JSON using our schema.
Data: name: John, age: 30
</user>

<assistant>
{
</assistant>
```

---

## Chapter 6: Precognition (Thinking Step-by-Step)

### Instruct Claude to Think Step-by-Step
For complex tasks that require reasoning, instruct Claude to "think step-by-step" or lay out its reasoning process before giving the final answer. This is also known as chain-of-thought (CoT) prompting.

**Example:**
> "Solve the following math problem. Think step-by-step and show your work before giving the final answer."

### Thinking Must Be "Out Loud"
The act of writing down the reasoning steps is what improves Claude's accuracy. You cannot ask it to "think silently"; the thinking process must be part of the generated output. To better organize the output, you can ask Claude to put its reasoning inside `<thinking>` tags.

**Example:**
```
<user>
Please solve this logic puzzle. First, think about it step-by-step within <thinking></thinking> tags. Then, provide the final answer.

[Puzzle details]
</user>
```

### Be Mindful of Order Bias
Claude can sometimes be sensitive to the order in which you present options and may be more likely to choose the second of two options. Instructing it to think step-by-step can help mitigate this bias.

---

## Chapter 7: Using Examples (Few-Shot Prompting)

### Provide Concrete Examples
One of the most effective ways to guide Claude is to provide one or more examples of the desired behavior. This is known as "few-shot" or "multishot prompting".

**Example of a zero-shot prompt (no examples):**
> "Classify the sentiment of the following text as positive, negative, or neutral. Text: I think the vacation was okay."

**Example of a few-shot prompt:**```
<user>
You are a sentiment classifier. Classify the following texts as positive, negative, or neutral.

<examples>
  <example>
    <text>The movie was fantastic!</text>
    <sentiment>positive</sentiment>
  </example>
  <example>
    <text>I was disappointed with the service.</text>
    <sentiment>negative</sentiment>
  </example>
</examples>

Classify this text:
<text>The weather is pleasant today.</text>
</user>
```

### Use Examples for Both Content and Format
Examples can demonstrate the correct answer, the desired tone, and the exact output format you require. Often, showing Claude an example is easier and more effective than writing out complex instructions.

---

## Chapter 8: Avoiding Hallucinations

### Give Claude an "Out"
To reduce the chances of Claude making up information (hallucinating), explicitly give it permission to state when it doesn't know an answer.

**Example:**
> "Based on the provided text, answer the following question. If the answer is not in the text, say 'I don't know.'"

### Require Evidence-Based Answers
When asking questions about a provided document, instruct Claude to first find and extract relevant quotes from the text. Then, instruct it to base its final answer only on those quotes. This grounds the response in the provided source material.

**Example:**
```
<user>
Please answer the question based *only* on the provided document. First, find the relevant quotes from the document and enclose them in <quotes></quotes> tags. Then, provide your final answer based on those quotes.

<document>
[Insert document text here]
</document>

<question>
What was the main finding of the study?
</question>
</user>
```

### Use Low Temperature
For factual tasks, set the `temperature` parameter to a low value (like 0.0) to make responses more deterministic and less creative, which can help reduce hallucinations.

---

## Chapter 9: Complex Prompts from Scratch

### Structure Complex Prompts with Key Elements
For complex tasks, build your prompt using a structured approach. A good starting point is to include these elements in order:
1.  **Role/Task Context:** Define who the AI should be.
2.  **Tone:** Specify the desired tone.
3.  **Rules:** Set boundaries and constraints.
4.  **Examples:** Provide 1-2 examples of a good output.
5.  **Input Data:** Provide the background data or documents.
6.  **Immediate Task Request:** State the specific task for Claude to perform right now.

### Place the Final Question at the End
The most important instruction—the specific question or task for Claude to perform—should be placed at or near the end of the prompt to ensure it is given the most weight.

---

## Chapter 10: Advanced Techniques

### Chaining Prompts
Break down a complex task into a sequence of simpler prompts. The output of one prompt becomes the input for the next, creating a powerful processing pipeline. This is useful for refining, correcting, or building upon previous generations.

**Example:**
1.  **Prompt 1 (Drafting):** "Draft an email to the team about the new project timeline."
2.  **Prompt 2 (Refining):** "Take the following email draft and make the tone more formal and concise. [Insert draft from Prompt 1]"
3.  **Prompt 3 (Translating):** "Translate the refined email into Spanish. [Insert refined draft from Prompt 2]"

### Tool Use (Function Calling)
Allow Claude to interact with external tools (like APIs or databases). This involves defining the tools in the prompt, having Claude output a structured request to use a tool, executing that tool in your code, and feeding the result back to Claude to synthesize a final answer.

### Search & Retrieval (RAG)
Augment Claude's knowledge by retrieving relevant information from an external source (like a document database) and providing that information as context within the prompt. Instruct Claude to use only the provided context to answer the user's question, which improves accuracy and relevance.

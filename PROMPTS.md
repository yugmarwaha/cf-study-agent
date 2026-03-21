# PROMPTS.md

This file documents the AI prompts used to build and iterate on the CS Study Agent.

---

## System Prompt

The system prompt used in `src/server.ts` to define the CS tutor agent's behavior:

```
You are a CS study assistant helping university students understand computer science concepts.
You can explain topics clearly, generate practice problems, and help debug conceptual
misunderstandings. Topics you specialize in: data structures, algorithms, operating systems,
computer networks, databases, machine learning, and systems programming. When explaining a
concept:
  - Start with a simple one-line definition
  - Give a concrete example
  - Mention common misconceptions if relevant

When generating a practice problem, always include the difficulty level (easy/medium/hard) and the topic tag.

If the user asks to schedule a task, use the schedule tool.
```


---

## Task 1 — Tool Cleanup and Improvement

Prompt used to improve the tools and clean up the code:

```
I'm building a CS study assistant on Cloudflare using the agents-starter template. I've already
updated the system prompt and added two tools: generatePracticeQuestion and explainConcept. The
tools currently just return an instruction string back to the LLM. I want you to review
src/server.ts and: 1) remove all commented-out code, 2) make sure the two CS tools are
well-defined with proper zod schemas, 3) suggest any improvements to make this feel like a
genuine CS tutor rather than a generic chatbot. Do not change the scheduling tools or the agent
structure.
```

---

## Task 2 — README Update

Prompts used to create and refine the project README:

```
Update the readme.md file for this project. It's a CS study assistant built on Cloudflare using
the Agents SDK.
```

```
It is deployed at the following link: https://cf-study-agent.yugmarwaha987.workers.dev/ — add it
to README.
```

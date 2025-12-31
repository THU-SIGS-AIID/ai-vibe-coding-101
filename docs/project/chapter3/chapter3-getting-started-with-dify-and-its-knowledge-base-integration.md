# Project 3: Getting Started with Dify and Knowledge Base Integration

## Review of Previous Lessons

In the previous lessons, we learned the basics of AI programming, prompt engineering, and AI image generation in groups. These contents helped us initially understand the boundaries and capabilities of different Large Language Models (LLMs) or generative models.

1.  **AI Programming**: We used AI-native tools (like Cursor, Trae, etc.) to complete simple functional modules or games.
2.  **Prompt Engineering**: We learned how to guide AI to output expected results through zero-shot, few-shot, and Chain-of-Thought (CoT) techniques.
3.  **AI Image Generation**: We used models like Recraft, Midjourney, or DALL-E to generate creative visual content.

---

## Learning Objectives for This Lesson

Today, we will take a step further from "simple dialogue" to "building applications." We will learn:

1.  **The Difference Between Chatbot and AI Agent**: Understand what an "Agent" is and why we need it.
2.  **Workflow Thinking**: Learn how to decompose complex tasks into multiple steps (Workflow).
3.  **Introduction to Dify**: Master the basic operations of the open-source LLM application development platform Dify.
4.  **Knowledge Base (RAG) Integration**: Learn how to let AI "read" your documents and answer questions based on specific knowledge.

---

## 1. From Chatbot to AI Agent

### What is a Chatbot?
A traditional Chatbot (like the basic version of ChatGPT) usually performs **Passive Response**:
*   User: "Help me write a travel plan for Tokyo."
*   AI: (Generates a plan based on its own training data).

### What is an AI Agent?
An AI Agent is a "Smart Agent" with **Autonomy** and **Tool-Using Capabilities**:
*   **Perception**: It can perceive user intent and environment.
*   **Planning**: It can decompose goals into multiple sub-tasks.
*   **Action (Tools)**: It can call external APIs (search, calculator, database) to perform tasks.
*   **Memory**: It can remember past interactions and adjust current behavior.

**Example**:
*   User: "Book a hotel in Tokyo for next Tuesday, with a budget under 1000 RMB."
*   AI Agent:
    1.  Searches for the specific date of "next Tuesday".
    2.  Calls a hotel booking API to filter by budget.
    3.  Compares reviews and selects the best option.
    4.  Asks the user for confirmation and completes the booking.

---

## 2. Workflow Thinking

In complex scenarios, a single prompt (One-shot) often fails to produce perfect results. We need to use **Workflow** thinking.

A Workflow is like a factory assembly line:
1.  **Input**: Receive user requirements.
2.  **Node 1 (Pre-processing)**: Clean the text or extract keywords.
3.  **Node 2 (LLM Processing)**: Generate content based on keywords.
4.  **Node 3 (Logic Branch)**: If the generated content is too long, summarize it; otherwise, output directly.
5.  **Output**: Deliver the final result to the user.

**Why use Workflows?**
*   **Controllability**: Each step can be debugged individually.
*   **Stability**: Complex logic is handled by specialized nodes, reducing AI "hallucinations."
*   **Reusability**: Common logic modules can be reused across different projects.

---

## 3. Introduction to Dify

[Dify](https://dify.ai/) is an extremely powerful open-source LLM application development platform. It provides a visual interface that allows us to build AI applications without writing extensive code.

### Core Concepts in Dify:
1.  **Chat App**: A basic conversational interface.
2.  **Workflow**: A visual canvas for building complex logic.
3.  **Agent Assistant**: An assistant capable of calling tools.
4.  **Knowledge**: The RAG (Retrieval-Augmented Generation) module.

### Hands-on Exercise: Building Your First Dify Workflow
1.  Log in to the Dify platform (use the official cloud version or a community-deployed version).
2.  Create a new "Workflow" application.
3.  Add an "LLM Node," select your model (e.g., DeepSeek, GPT-4), and write System Prompts.
4.  Connect nodes and click "Preview" to test.

---

## 4. Knowledge Base (RAG) Integration

### What is RAG?
**RAG (Retrieval-Augmented Generation)** is a technique that combines "Retrieval" with "Generation."

*   **Problem**: LLMs have a "cutoff date" for their training data and don't know your private documents.
*   **Solution**:
    1.  **Indexing**: Upload documents (PDF, Markdown, etc.) to the Dify Knowledge Base.
    2.  **Retrieval**: When a user asks a question, the system first finds relevant snippets in the documents.
    3.  **Augmentation**: The system sends the question + the retrieved snippets to the LLM.
    4.  **Generation**: The LLM answers based on the provided "context."

### Why RAG?
*   **Accuracy**: Answers are based on facts rather than imagination.
*   **Privacy**: You can use your own data without retraining the model.
*   **Cost-effectiveness**: Much cheaper and faster than fine-tuning a model.

---

## 5. Homework: Build Your "Personal Knowledge Assistant"

**Task Description**:
Use Dify to build an AI assistant that can answer questions based on a specific set of documents (e.g., a course syllabus, a product manual, or your own notes).

**Requirements**:
1.  Upload at least one document to the Dify **Knowledge** section.
2.  Create a **Chat App** or **Workflow** that integrates this knowledge base.
3.  Configure the "Prompt" to ensure the AI prioritizes information from the knowledge base.
4.  Test and share your application link or screenshots.

---

## Summary
By mastering Dify and RAG, you have moved from being a "user of AI" to a "builder of AI applications." In the next lesson, we will explore how to integrate these powerful back-end capabilities into your own front-end projects.

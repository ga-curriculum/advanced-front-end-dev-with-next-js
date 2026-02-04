# Instructor Guide: Advanced Front-End Development with Next.js

## Module Overview

In this module, learners use Next.js to create dynamic, high-performance front-end interfaces that interact with AI services through APIs. The session focuses on moving beyond basic Node.js scripts to building full-stack web applications where the "Backend" and "Frontend" are tightly integrated via the Next.js App Router.

## Learning Objectives

By the end of this session, students will be able to:

* 
**Develop AI-responsive front-end components** using Next.js for dynamic rendering and data fetching.


* **Differentiate** between Server Components (secure logic) and Client Components (interactive UI) to properly manage API keys and state.
* **Implement** specific UI patterns for AI, such as loading skeletons and streaming text, to manage the inherent latency of Large Language Models (LLMs).
* **Construct** a functional Next.js page that accepts user input, communicates with an AI model, and renders the result.

## Session Pacing Guide (120 Minutes total)

| Duration   | Segment                             | Instructor Action                                                                                                                     |
| ---------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **20 min** | **Why Next.js for AI?**             | Contrast standard React (SPA) with Next.js (SSR). Explain the benefits of hiding API keys on the server side of the framework.        |
| **25 min** | **Server vs. Client Components**    | Use the "Kitchen vs. Dining Room" analogy. Live code: Show what happens when you try to use `useState` in a Server Component (Error). |
| **25 min** | **Server Actions & Data Fetching**  | Demonstrate creating a `actions.js` file. Explain `use server`. Show how to call this function directly from a form.                  |
| **20 min** | **UX for AI: Handling Latency**     | Discuss "Perceived Performance." Show how to add a simple loading state (`useFormStatus` or `useState`). Briefly mention "Streaming." |
| **30 min** | **Lab: Building a Next.js AI Page** | Facilitate the lab. Help students scaffold a new app and connect it to OpenAI.                                                        |

---

## Delivery Notes & Teaching Tips

### 1. The "Kitchen vs. Dining Room" Analogy (Server vs. Client)

* **Concept:** Next.js App Router mixes server and client code, which is confusing.
* **The Analogy:**
* **Server Component (The Kitchen):** Where the raw ingredients (Data/API Keys) and dangerous tools (Database connections) are. The customer (Browser) never enters the kitchen.
* **Client Component (The Dining Room):** Where the customer sits. It has interactivity (salt shakers, menus, buttons), but no raw ingredients or secrets.


* **Key Rule:** You can pass food (Data) from the Kitchen to the Dining Room, but you can't bring the Dining Room table into the Kitchen.

### 2. Server Actions: The "Waiter"

* **Simplification:** In the previous module, we built a separate Express server. In Next.js, **Server Actions** replace that manual API setup.
* **Visual Aid:** Draw a diagram showing the "Server Action" as a tunnel that securely transports the user's request from the Client Component to the Node.js environment running on the server.

### 3. Managing AI Latency (The "Soufflé" Problem)

* **Context:** Database queries take milliseconds. AI takes seconds.
* **Teaching Tip:** Ask students, "How long will you wait for a website to load before leaving?" (Usually < 3 seconds).
* **Solution:** Explain that we must cheat time.
* *Skeleton Loaders:* "We are working on it."
* *Streaming:* "Here is the first word... then the second..." (Like a typewriter). This keeps the user engaged.



---

## Lab Guide: Building a Next.js AI Page

**Lab Objective:** Build a Next.js page that fetches and displays AI-generated text or images.

### Setup

* **Tools:** Node.js, Text Editor (VS Code).
* **Prerequisite:** Students must have their OpenAI API Key from the previous module.

### Common Student Issues & Solutions

* **Issue:** "I get an error: *Event handlers cannot be passed to Client Component props*."
* *Solution:* They likely forgot to put `'use client'` at the top of a component that uses `onClick` or `useState`. Remind them: "If it clicks, it clients."


* **Issue:** "My API Key isn't found."
* *Solution:* In Next.js, standard environment variables are only available on the server. If they try to access `process.env.KEY` in a Client Component, it will be undefined. This is a **security feature**. They must move the API call to a Server Action.


* **Issue:** "The page refreshes when I submit the form."
* *Solution:* If using a standard `<form>` without a Server Action, the browser defaults to a refresh. Ensure they are using the Next.js `<Form>` component or properly handling `onSubmit` with `e.preventDefault()` if doing it manually.



### Debrief Questions

At the end of the lab, ask:

1. "Why did we have to put the OpenAI code in `actions.js` (Server) instead of right inside the component?" (Security/Secret Keys).
2. "What did the application look like while the AI was thinking? Was it clear to the user that something was happening?"

---

## Resources for the Instructor

* **Reference:** [Next.js App Router Documentation](https://nextjs.org/docs/app)
* **Reference:** [React "use server" Directive](https://react.dev/reference/react/use-server)
* **AI Prompt Bank:**
* *"I have a 'Hydration Error' in Next.js. What does that usually mean?"* (Mismatch between server HTML and client HTML).
* *"Explain the difference between `page.js` and `layout.js`."*
---
layout: default
title: "Activity 3"
parent: Hands-On Activities
nav_order: 3
---

# Activity 3: Designing a Development Team Using Subagents

---

## Overview

This activity is adapted from the "Multi-agent design patterns" lesson in Microsoft's [AI Agents for Beginners](https://microsoft.github.io/ai-agents-for-beginners/08-multi-agent/) course.

Our client is the Allegheny Cat Café, a small café where visitors can have a coffee with resident cats and maybe adopt one. They want a simple website showing their menu, their cats, and a way to book a visit.

First, you will design a team of agents that could build this website, using the patterns and building blocks from the mini-lecture. Then you will run a small three-agent team in GitHub Codespace, where each agent does one job and passes its result to the next. Finally, you will check whether the café's rules survive each handoff or get lost or changed along the way. Handoffs are where multi-agent systems often break.

You do not need any programming experience. Nobody writes code today, including the agents.

## Logistics

Sit in groups of 4 to 5. Do the design with a partner, and help each other through setup.

Everyone runs the tools in their own browser and completes their own tasks. The reflection is individual, handwritten, and will be graded. You may not use any AI tool to write the reflection.

## Setup (5 minutes)

1. **Sign in to GitHub.**
   - If you have an account, sign in at <https://github.com>
   - If not, create one at <https://github.com/signup>
2. **Open the project in a codespace.** A codespace is VS Code running in your browser. It is free with any GitHub account.
   - Go to <https://github.com/modern-genai-se/allegheny-cat-cafe>
   - Click the green **`<> Code`** button, open the **Codespaces** tab, and click **Create codespace on main**
   - Wait for VS Code to open in your browser. The first time can take a couple of minutes
3. **Trust the folder.** When the codespace finishes loading, a popup asks "Do you trust the authors of the files in this folder?" Click the blue **Trust Folder & Continue** button.
4. **Turn on GitHub Copilot.**
   - Hover over the Copilot icon in the Status Bar at the bottom left of the window. Select **Set up Copilot** (in some versions it says **Enable AI Features**)
   - Sign in with GitHub and follow the prompts. If you do not have a Copilot plan, you will be signed up for Copilot Free, which is enough for today
5. **Open the chat.**
   - If you do not already see the **Chat** panel on the right side of the window, press `Ctrl+Cmd+I` (macOS) or `Ctrl+Alt+I` (Windows) to open it
   - At the bottom of the chat box, click **Copilot** and change it to **Local**
   - Make sure the selector next to the **+** in the chat box is set to **Agent**
6. **Check it.** In the file list on the left, you should see `BRIEF.md` and a `.github/agents` folder. Open `BRIEF.md`. This is the café's request, and you will use it throughout the activity.

If you are still stuck after 5 minutes, work off a groupmate's laptop for the tool steps and keep moving.

## Activity (15 minutes)

Do not edit any files by hand except your Tester file in Step 2.

### Step 1: design the team (5 minutes, with a partner)

**Assignment:** Design a multi-agent system for developing the Allegheny Cat Café website. Identify the agents involved, their roles and responsibilities, and how they interact with each other. 

Fill in **Table 1** on your reflection sheet as you go. Your reflection will ask about your design.

Tip: You may need more agents than you think. Think about the different stages of building software.

For each agent in your design, write down:

- **Agent:** a short name for it
- **Role:** what it is responsible for
- **Receives from:** which agent (or person) it gets its work from, and what that work is
- **Hands off to:** which agent it passes its result to, and what that result is

### Step 2: write the Tester (4 minutes)

Your design probably has more agents than we can run in the time we have, so for the rest of the activity you will run a small piece that most designs share: the planning stages. Three agents pass work down a line:

1. A **Product Manager** reads `BRIEF.md` and writes `requirements.md`, a numbered list of everything the website must do.
2. A **Designer** reads `requirements.md` and writes `user-stories.md`, short descriptions of how visitors will use the site.
3. A **Tester** writes `test-checklist.md`, a list of checks someone could run on the finished website to confirm it does what the café asked.

The Product Manager and Designer are already written. You will write the Tester, using the same questions you answered for each agent in your design: what it does, what it receives, and what it hands off.

**Goal:** Create a Tester agent file that gives the Tester everything it needs to do its job.

A Tester agent does not see your chat. It only knows what is in its file and the short message the main agent sends it.

1. In the file list on the left, open the `.github/agents` folder. Open `product-manager.agent.md` and `designer.agent.md` and read them. Your Tester file will follow the same layout.
2. Right-click in the file list, choose **New File**, and type this full path: `.github/agents/tester.agent.md` 
3. Paste this skeleton into the new file.

```
   ---
   name: Tester
   description:
   user-invocable: false
   tools: ['read', 'edit']
   ---
   You are the tester on a small software team.

   ## Objective

   ## What to base the checks on

   ## What to write

   ## What to return

   ## Boundaries
```

4. Fill it in, in your own words. Do not change the `name` or `tools` lines.
   - **description:** one sentence telling the main agent when to use the Tester.
   - **Objective:** what the Tester must produce. It should write `test-checklist.md`.
   - **What to base the checks on:** which files the Tester should read: `BRIEF.md`, `requirements.md`, `user-stories.md`, or some combination. This is the Tester's "receives from."
   - **What to write:** what each check should look like, so a person could actually carry it out on the finished website.
   - **What to return:** what the Tester reports back to the main agent when it is done. This is its "hands off to."
   - **Boundaries:** at least one thing the Tester must not do. It can edit files, so say which files it must not change.
5. Press `Cmd+S` / `Ctrl+S` to save.
6. **Check it:** every section of your file has at least one line under it, and the `name` line still says `Tester`.

### Step 3: run the team (4 minutes)
1. Click **+** at the top of the Chat view to start a new chat. Check that the bottom of the chat box still says **Local** and **Agent**.
2. Send this prompt in the chat:

```
   Turn the café's request in BRIEF.md into planning documents using your team. First, have the Product Manager subagent write requirements.md. Next, have the Designer subagent write user-stories.md from requirements.md. Finally, have the Tester subagent write test-checklist.md. Do not do any of these steps yourself. When all three are done, summarize what each subagent reported.
```

3. If VS Code asks for permission to create or edit a file, allow it.
4. Each agent appears in the chat as a collapsed step. Click one to see the exact message the main agent sent it and what it sent back.
5. **Check it:** three new files appear in the file list: `requirements.md`, `user-stories.md`, and `test-checklist.md`. Open the Tester's step in the chat and note whether it followed what you wrote in your file.

### Step 4: trace three rules (2 minutes)

**Goal:** find out whether the café's rules survived each handoff.

Each agent only saw what the agent before it wrote. If a rule was dropped or reworded early, every agent after that point worked from the wrong version.

1. Find **Table 2** on your reflection sheet.
2. For each rule, open each file and use `Cmd+F` / `Ctrl+F` to look for it.
3. Mark each cell **kept**, **changed**, or **missing**.

| Rule from BRIEF.md | requirements.md | user-stories.md | test-checklist.md |
| --- | --- | --- | --- |
| Closed Monday and Tuesday | | | |
| 1 to 6 people per booking | | | |
| Anyone under 12 must come with an adult | | | |

## Reflection (5 minutes)

Answer both questions by hand on the sheet provided. Use your design, your trace table, and your notes. Do not use AI to assist in writing this reflection.

1. Describe one handoff from your design in Step 1: which two agents, and exactly what information passes between them. Then describe one point in your design where a human should approve the work before the team continues, and explain why that point needs a human rather than another agent.

2. Look at your trace table from Step 4. Did any of the café's rules change or go missing on its way from `BRIEF.md` to `test-checklist.md` as the work passed from one agent to the next? Describe what happened to one rule and explain why you think it happened.

## Grading

10 points. Graded on the reflection only.

| Criterion | Points |
| --- | --- |
| Q1: Designing the team | 4 |
| Q2: Tracing a rule | 5 |
| Format: name, date, both answered | 1 |

### Q1: Designing the team (4 points)

Full credit names two specific agents from your design and what information passes between them. It then names one point where a human should approve the work, and explains why that point needs a human rather than another agent, i.e., what a human can judge that an agent cannot, or what goes wrong if no one checks.

**Good:**

> In our design, the Requirements agent hands the Designer a numbered list of what the site must do, including every booking rule from the brief. The Designer never reads the brief itself, so if a rule is missing from the list, nothing after that point will include it. A human should approve right after the requirements are written: the café owner checks the list before anything else happens. Another agent could compare the list to the brief, but only the owner knows what they actually meant, for example whether "Wednesday through Sunday" also covers holidays. Catching a wrong requirement there is cheaper than catching it after the site is built.

**Not sufficient (0 to 1 point):**

> The agents pass information to each other and a human checks the final result to make sure it's good.

### Q2: Tracing a rule (5 points)

Full credit uses your trace table to describe what happened to one specific rule on its way from `BRIEF.md` to `test-checklist.md`, and gives a reason based on what each agent was given to work from. If every rule was kept, full credit says so, describes one rule's path, and explains what you think kept it intact.

**Good:**

> The rule "closed Monday and Tuesday" changed in requirements.md, where the Product Manager rewrote it as "open five days a week." That version no longer says which days are closed. The Designer only reads requirements.md, so its user story copied the vaguer version. In test-checklist.md the original rule came back, because my Tester read BRIEF.md as well as requirements.md. I think the rule changed because the Product Manager was summarizing the brief in its own words, and nobody after it checked that summary against the source except the Tester.

**Not sufficient (0 to 1 point):**

> Some of the rules changed a little because the agents wrote things differently.

## Submission

Hand your reflection sheet to the instructor before you leave. Late reflections are not accepted, since the activity is in class.

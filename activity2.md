---
layout: default
title: "Activity 2"
parent: Hands-On Activities
nav_order: 2
---

# Activity 2: Using Skill Files 

---

## Overview

Every software project has rules that live in its documentation and in its maintainers' heads. A coding agent may find some of those rules on its own and miss or skip others, and the result can differ from one run, or one laptop, to the next. A skill is one way to make this more reliable. A skill is a plain text file, `SKILL.md`, that tells the agent when to use it and what steps to follow.

In this activity you will ask a coding agent to make a small contribution to a real open source project. You will see what it gets right and wrong on its own, write a skill that teaches it the project's rules, and run it again.

In this activity you will ask a coding agent to make a small edit to a copy of a real open source project on your laptop, the kind of edit the project has written rules for. Nothing is submitted to the project. You will see which rules the agent follows on its own, write a skill that spells the rules out, and run the same request again to see what changes.

The project is [public-apis](https://github.com/public-apis/public-apis), a popular list of free web services that developers can build on. The whole list is one big table, and contributing means adding one row. You do not need to read or run any code.


## Logistics

Sit in groups of 4 to 5. Help each other through setup and unblock each other during the tasks.

Everyone runs the tools on their own laptop and completes their own tasks. The reflection is individual, handwritten, and will be graded. You may not use any AI tool to write the reflection.

## Setup (5 minutes)

You need Cursor and a copy of the game. No terminal, Python, or Node.js required.

0. **Install Cursor.**
   - NOTE: Only do Step 0 if you do not already have Cursor installed (which was required for Activity 1)
   - Go to [cursor.com](https://cursor.com), download Cursor, and install it
   - Open it and set up a free account

1. **Download the repository.**
   - Go to [https://github.com/public-apis/public-apis](https://github.com/public-apis/public-apis)
   - Click the green **`<> Code`** button at the top of the page and select **Download ZIP**
   - Unzip the file and save the folder somewhere you can find again, such as your Desktop

2. **Download the README separately.** The ZIP does not include it.
   - On the same GitHub page, click `README.md` in the file list to open it
   - Click the download icon at the top right of the file view, next to **Raw**
   - Drag the downloaded `README.md` into the folder you unzipped in step 1, next to `CONTRIBUTING.md`

3. **Open the project in Cursor.**
   - In Cursor, choose **File > Open IDE** or **File > Open Editor Window** if you do not see 'Open IDE' as an option
   - From the start page, select **Open Project**
   - Select the folder you unzipped in step 1
   - Cursor opens the project in a new window. You should see `README.md` (the list) and `CONTRIBUTING.md` (the project's rules) in the file list on the left

If you are still stuck after 3 minutes, work off a groupmate's laptop and keep moving.

## Activity (12 minutes)

Do not edit any files by hand except your skill file. Everything else goes through the agent.

### Step 1: ask the agent to contribute (3 minutes)

1. Press `Cmd+L` (macOS) or `Ctrl+L` (Windows) to open the chat sidebar. Set the mode selector at the bottom to **Agent**.
2. Send this prompt exactly as written. It asks the agent to add a website that tracks the International Space Station.

   ```
   Add this API to the list of APIs in found in README.md: WhereTheISS.at API, docs at https://wheretheiss.at/w/developer. It's a free REST API that gives you the current position, velocity, altitude, and other real-time tracking info for the International Space Station and other satellites. No API key needed and it works over https.
   ```

3. The agent adds one row to the table in `README.md` and shows you the change. Look at the row it wrote, and read its explanation. Did it open `CONTRIBUTING.md` on its own?
4. **Check it** against four of the project's rules:
   - The name does not end in "API" and does not include a web ending like `.com` or `.at`
   - The description is 100 characters or fewer
   - The description does not end with a period
   - The row is in alphabetical order within its section
5. Note which rules the agent followed and which it broke. Compare with a groupmate. Did your agents make the same choices? Then click **Undo All** (labeled **Reject All** in some versions) at the top of the chat panel to remove the row.

### Step 2: write a skill (6 minutes)
 
1. Open `CONTRIBUTING.md` and find the four rules from Step 1. Notice how the guide states them: one short line each, written for a person who already knows what to do. In your skill file, you will rewrite each rule as a clear step for the agent, then tell the agent to double-check its finished row against those rules before it stops.
2. Right-click in the file list, choose **New File**, and type this full path: `.cursor/skills/add-public-api/SKILL.md`
3. Paste this skeleton into the new file:
   ```
   ---
   name: add-public-api
   description: 
   ---
   # Add an entry to the public-apis list
 
   ## Steps
   1.
   2.
   3.
 
   ## Check before you finish
   ```
 
4. Fill it in, in your own words. For details on the format, see the [Agent Skills specification](https://agentskills.io/specification):
   - **description:** one sentence saying when the agent should use this skill
   - **Steps:** what the agent should do, in order, to add a row correctly
   - **Check before you finish:** what the agent must verify about its own row before it stops
5. Press `Cmd+S` / `Ctrl+S` to save.

### Step 3: run it again (3 minutes)
 
1. Open a **new chat** so the agent starts fresh. Make sure the mode is still **Agent**.
2. Send the same prompt from Step 1.
3. If the agent's reply does not mention your skill, open another new chat, type `/add-public-api`, paste the prompt after it, and send.
4. **Check it** against the same four rules. Note what changed from Step 1 and what did not.

## Reflection (5 minutes)
 
Answer both questions by hand on the sheet provided. Do not use AI to assist in writing this reflection.
 
1. What did the agent get right and wrong the first time, and did it find the project's rules on its own? What did your skill change? Use what you saw to explain what a skill gives you that leaving the agent to find the rules on its own does not.

2. The contribution guide was written for people. What was hard about turning it into instructions for an agent? Give one specific example from your own skill, such as a rule you had to spell out as a step or something you chose to leave out, and say what that taught you about writing for an agent.

## Grading
 
10 points. Graded on the reflection only.
 
| Criterion | Points |
|---|---|
| Q1: What the agent did on its own | 4 |
| Q2: Writing for an agent | 5 |
| Format: name, date, both answered | 1 |
 
### Q1: What the agent did on its own (4 points)
 
Full credit names specific things the agent got right and wrong in your first run, says whether it found the rules on its own, says what changed in the second run, and draws a conclusion about skills from it. If your skill changed nothing, full credit explains why you think that happened.
 
**Good:**
> The first time, the agent opened CONTRIBUTING.md without being asked and got most things right: the right section, alphabetical order, a short description with no period. It still named the entry "WhereTheISS.at", even though the guide says to leave the web ending out of the name. My groupmate's agent never opened the guide and put the row at the bottom of the section. After we wrote our skills, mine fixed the name and hers fixed the order. The agent can find the rules, but whether it did, and how carefully it followed them, changed from laptop to laptop. A skill makes the rules and a final check part of the task every time, for everyone on the team.
 
**Not sufficient (0 to 1 point):**
> The agent made some mistakes at first and then the skill fixed them.
 
### Q2: Writing for an agent (5 points)
 
Full credit gives one concrete example from your own skill and explains what it taught you.
 
**Good:**
> The guide just says to keep entries in alphabetical order. A person knows what to do with that. My first version of the skill said the same thing and the agent still put the row at the bottom of the section. I had to write it as a step: find the right section, read the names around where the new one belongs, and insert the row between them. I learned that an agent needs the procedure, and a person only needs the goal. I left out the parts about forking and pull requests because the agent was only editing a file on my laptop.
 
**Not sufficient:**
> I made the rules clearer so the AI could understand them.
 
## Submission
 
Hand your reflection sheet to the instructor before you leave. Late reflections are not accepted, since the activity is in class.
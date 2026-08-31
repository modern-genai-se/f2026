---
layout: default
title: "Activity 1"
parent: Hands-On Activities
nav_order: 1
---

# Activity 1: Using GenAI to Change Code You Didn't Write

---

## Overview

Most industrial software development work is changing or maintaining code that someone else wrote. Coding agents are increasingly how that work gets done, which puts a lot of weight on the prompt. 

In this activity you will make four changes to a working game using a coding agent in Cursor. You are given an informal requirement for each task, not a complete specification. Writing the prompt is the work, and how you write it will determine the output from the coding agent. Keep a log of every prompt you send. You will compare your log against a groupmate's at the end.

You do not need to read or understand the source code. Everything you need to notice is visible from playing the game.

## Logistics

Sit in groups of 4 to 5. Help each other through setup and unblock each other during the tasks.

Everyone runs the tools on their own laptop and completes their own tasks. The reflection is individual, handwritten, and will be graded. You may not use any AI tool to write the reflection.

## Setup (5 minutes)

You need Cursor and a copy of the game. No terminal, Python, or Node.js required.

1. **Download the repository.**
   - Go to [https://github.com/gabrielecirulli/2048](https://github.com/gabrielecirulli/2048)
   - Click the green **`<> Code`** button at the top of the page and select **Download ZIP**
   - Unzip the file and save the folder somewhere you can find again, such as your Desktop

2. **Install Cursor.**
   - Go to [cursor.com](https://cursor.com), download Cursor, and install it
   - Open it and set up a free account

3. **Open the project in Cursor.**
   - In Cursor, choose **File > Open IDE**
   - From the start page, select **Open Project**
   - Select the folder you unzipped in step 1
   - Cursor opens the project in a new window. You should see a file list on the left containing `index.html`, a `js` folder, and a `style` folder

4. **Run the game in your browser.**
   - In the file list, right-click `index.html` and choose **Reveal in Finder** (macOS) or **Reveal in File Explorer** (Windows)
   - In the window that opens, double-click `index.html`. The game opens in your browser
   - Press an arrow key to confirm the game works
   - Leave this browser tab open for the rest of the activity. You will come back to it after every task

If you are still stuck after 5 minutes, work off a groupmate's laptop and keep moving.

## Activity (15 minutes)

Work through the four tasks in order. Each task gives you a goal, your job is to get the agent to produce a version of the game that meets it. Do not edit any code by hand. Everything goes through the agent.

**Write down every prompt you send, numbered.** If a task takes you four prompts, you should have four numbered lines. You will need these for the reflection.

Make note of what changes you observe after each task.

### Task 1: change the win condition (2 minutes)

**Goal:** the game should end in a win when the player reaches 32, instead of 2048.

1. In Cursor, press `Cmd+L` (macOS) or `Ctrl+L` (Windows) to open the chat sidebar on the right.
2. At the bottom of the chat box there is a mode selector. Set it to **Agent**.
3. Write your prompt in the chat box and press Enter, then record the prompt in your prompt log.
4. The agent edits files and shows you the changes. Click **Keep All** (labeled **Accept All** in some versions) at the top of the chat panel.
5. Press `Cmd+S` / `Ctrl+S` to save. If any file tab shows a dot instead of an x, it still has unsaved changes.
6. Switch to your browser tab and press `Cmd+R` / `Ctrl+R` to reload.
7. Click **New Game** on the page. The game saves your progress in the browser, so without this you may still be looking at the old board.
8. **Check it:** merge tiles until you reach 32. Does the win message appear? If not, send another prompt and add it to your log.

### Task 2: add a move counter (3 minutes)

**Goal:** the page should show a running count of how many moves the player has made.

1. Write your prompt, send it, and copy it onto your prompt log.
2. Click **Keep All**.
3. Press `Cmd+S` / `Ctrl+S` to save.
4. Reload the browser tab and click **New Game**.
5. **Check it:** make several moves and watch the counter. Then press an arrow key in a direction where nothing can move, for example press left when all tiles are already flush left. Does the counter still go up? Is that what you wanted? If not, send another prompt and add it to your log.

### Task 3: resize the board (4 minutes)

**Goal:** the game should be played on a 5x5 board instead of a 4x4 board.

1. Write your prompt, send it, and copy it onto your prompt log.
2. Click **Keep All**.
3. Press `Cmd+S` / `Ctrl+S` to save.
4. Reload the browser tab and click **New Game**.
5. **Check it:** look at the board and play a few moves. Are there five columns and five rows? Do the tiles line up with the grid squares behind them? Does the score change on moves where nothing appears to happen? Write down exactly what you see on the screen. If it is wrong, send another prompt and add it to your log.

### Task 4: two-player mode (6 minutes)

**Goal:** two games on the same page. The player 1 uses WASD, the player 2 uses the arrow keys. Each game keeps its own score.

1. Write your prompt, send it, and copy it onto your prompt log.
2. Click **Keep All**.
3. Press `Cmd+S` / `Ctrl+S` to save.
4. Reload the browser tab and click **New Game**.
5. **Check it:** are there two boards? Does WASD move only the player 1 board and the arrow keys only the player 2 board? Does scoring on one board leave the other alone? Play both at once with a groupmate if that is easier.
6. Keep prompting until you accomplish the task or until time runs out. Log every prompt.
7. **Before you move on:** trade prompt logs with someone in your group and play both versions. Find one thing they told the agent that you never did, and one thing you told it that they never did. Note what each of those changed about the game.

## Reflection (10 minutes)

Answer all three questions by hand on the sheet provided. Use your prompt log and the notes you took during the activity. Do not use AI to assist in writing this reflection.

1. Write your first prompt for Task 4 exactly as you sent it, then write the prompt that finally got you what you wanted. If your first prompt worked, say so. If your first prompt did not work, what did you have to add, and what made you realize it was missing?

2. Compare your Task 4 prompts with a groupmate's. Name one thing they specified that you did not, and one thing you specified that they did not. For each, say what difference you believe it made in the two games.

3. Your prompts for the four tasks specified what each should accomplish, but they most likley did not specify everything about how the finished game looks and behaves. Name three design decisions in your final version that you never specified, then pick the one you would most want to change, explain why, and write the prompt you would send to change it.

## Grading

10 points. Graded on the reflection only.

| Criterion | Points |
|---|---|
| Q1: Prompt log and revision | 3 |
| Q2: Divergence | 3 |
| Q3: Unmade decisions | 3 |
| Format: name, date, all three answered | 1 |

### Q1: Prompt log and revision (3 points)

Full credit reproduces both prompts as written, then explains what changed and what triggered the change. If one prompt was enough, full credit says so and explains what you think made that prompt sufficient.

**Good:**
> First prompt: "make it two player." I got one board where WASD and the arrows both moved the same tiles, so two people were fighting over one game. Working prompt: "Show two separate 2048 boards side by side on the page. The left board only responds to WASD. The right board only responds to the arrow keys. Each board has its own score displayed above it." I only realized I had to say "separate boards" after watching my own arrow key move the tile my partner had just moved with D. The word I was missing was independent, and I did not know I needed it until I saw them share state.

**Not sufficient (0 to 1 point):**
> My first prompt was too vague so I made it more specific and then it worked.

> I asked for two player mode and it did it.

### Q2: Divergence (3 points)

Full credit names two concrete, observable differences. Written so someone who never saw either version could picture both.

**Good:**
> Mine put the two boards next to each other at the same size, and each board had its own score box sitting directly above it. Theirs stacked one board above the other and kept a single score bar at the top of the page with both scores in it, separated by a slash. Second difference: on mine, when one player lost, that board froze and showed game over while the other player kept going. On theirs, the moment either player lost, both boards stopped.

**Not sufficient:**
> Theirs looked different from mine and worked a bit differently.

> Mine was better designed.

### Q3: Unmade decisions (3 points)

Full credit names three specific behaviors nobody in the room chose, and identifies what settled them. "The AI decided" is only sufficient if it says what the AI was working from, for example the existing code, the default styling, or an assumption it filled in.

**Good:**
> First, whether one player losing ends the other player's game. I never said, and it decided both stop. Second, whether the two boards share a best score or keep separate ones. Mine kept one shared best score, which I noticed only because my partner's kept two. Third, the two boards ended up side by side rather than stacked one above the other. My prompt only asked for two players, so I never said anything about where the boards should sit on the page.

**Not sufficient:**
> The AI made a lot of decisions for me about how the game looks and works.

## Submission

Hand your reflection sheet to the instructor before you leave. Late reflections are not accepted, since the activity is in class.
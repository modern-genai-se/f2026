---
layout: default
title: "Activity 4"
parent: Hands-On Activities
nav_order: 4
---

# Activity 4: Evaluating Benchmark Claims and Learning from Model Cards

---
[Download the printable reflection sheet (PDF)](assets/Hands_On_Activities/activity_4_worksheet.pdf)

## Overview
In lecture you audited OpenAI's reporting of Astra's cybersecurity score. The headline was a perfect score of 100% on ExploitBench. A later sanity check performed on a refreshed benchmark, built from vulnerabilities after Astra's knowledge cutoff, yielded a score of 39%. 

A model card is a document a developer publishes with a model. It reports benchmark scores and outlines the configurations under which each score was produced: which settings were used, how many trials were run, and how much text the model could use. Those details allow users to more directly interpret and contextualize the scores, helping inform further evaluations and adoption decisions. 

In this activity, you read excerpts from the benchmark section of Anthropic's model card for Claude Opus 4.7, perform a comparative analysis, and use that analysis to inform your decision on which model to choose for your "team." Your "team" develops a research assistant tool that answers questions by searching the web. It currently uses Claude Opus 4.6. Your lead asks whether the team should switch to Claude Opus 4.7. You will identify the relevant evidence in the card excerpts, assess how it was measured, and write a recommendation.

## Logistics

Sit in groups of 3 to 4. Discuss Table 1 with your group. Everyone fills in their own reflection sheet.

The reflection is individual, handwritten, and will be graded. You may not use any AI tools to write the reflection.

## Setup

Nothing to install. Keep your reflection sheet in front of you. Start this page once the class discussion of Question 1 ends.

## Background: How to read a model card (2 minute read)

A full model card, aka system card, is hundreds of pages. [Claude Opus 4.7's model card](https://assets.claude.com/037f06850df7fbe871e206dad004c3db5fd50340.pdf) is 232 pages, and its benchmark evaluation results are presented in Section 8. 

You can use the following four steps to get from your question of 'which model to choose' to a reccomendation that you can support with evidence from the card. 

1. **Turn the question into a task a benchmark can answer.** A score answers your question only if the benchmark's tasks resemble your product's tasks. Your product searches the web, so you need benchmarks made of web research tasks. A score on a benchmark of command-line tasks says nothing about performance on web research.
2. **Record each model's score, and its ± range if the card gives one.** The ± symbol represents the margin of error (MOE) the card reports around a score. It shows how much the score could vary if the test were run again, given a certain confidence level. The confidence interval (CI) is the range within which the true score is expected to fall, and you get its upper and lower bounds by adding the margin of error to the score and subtracting it from the score. 

`CI = (Score − MOE, Score + MOE)`

3. **Check the conditions.** A comparison is fair when both models were tested the same way. Look for differences in settings, token limits, and number of trials. Two terms you will see:
   - A **token** is a chunk of text, roughly three quarters of a word. A token limit caps how much text the model can use on one question.
   - **Context compaction** means that when a long session fills the model's working memory, the system summarizes the earlier part so the model can continue. The card states how many tokens a session reaches before compaction starts.
4. **Compare the gap between the confidence intervals, then recommend.** As a rule of thumb, if the confidence intervals for the two models' scores overlap, the gap may be noise. 


## Activity

The card text is quoted below from Anthropic, *System Card: Claude Opus 4.7*, April 16, 2026, <https://anthropic.com/claude-opus-4-7-system-card>. Page numbers are from the card's PDF.

### Step 1: Select the benchmarks that match your product (1 minute)

Excerpt 1 is part of the card's summary table and lists four benchmarks. Excerpt 3 adds a fifth benchmark. 
Below are descriptions of the tyes of tasks each benchmark is intended to evaluate. Choose the two benchmarks that best match your research assistant and write them in the first column of Table 1 on your sheet.

- SWE-bench: Evaluates model's performance on real-world software engineering tasks.
- BrowseComp: Evaluates model's ability to find hard-to-locate information on the open web.
- DeepSearchQA: Evaluates model's performance on difficult multi-step information-seeking tasks across 17 different fields, requiring the model to conduct extensive searches to compile a list of exhaustive answers.
- Terminal-Bench 2.0: Evaluates model's performance on tasks completed by typing commands in a terminal.
- OSWorld:  Evaluates model's performance on tasks completed by operating a computer's graphical desktop.


### Step 2: Record the scores and margins of error (1 minute)

Review the card excerpts below to identify the scores for Claude Opus 4.6 and Claude Opus 4.7 for the benchmarks you selected in Step 1. Record these scores as well as the margin of error (MOE) and confidence interval (CI) for each provided in Table 1. In cases where the excepts do not provide a margin of error for a particular score write "no ±" after that score in the table. '
Note: you will have to calculate the CI using the MOE and score using the formula:

`CI = (Score − MOE, Score + MOE)`
For example, if the score is 70%  and the ± is 2% -> CI: [68, 72]

**Excerpt 1: Table 8.1.A, selected rows (pp. 191 to 192).** A dash means the card reports no score. Footnote markers are left out.

| Evaluation | Claude Opus 4.7 | Claude Opus 4.6 | GPT-5.4 | GPT-5.4 Pro | Gemini 3.1 Pro |
| --- | --- | --- | --- | --- | --- |
| SWE-bench Verified | 87.6% | 80.8% | - | - | 80.6% |
| Terminal-Bench 2.0 | 69.4% | 65.4% | 75.1% | - | 68.5% |
| BrowseComp | 79.3% | 83.7% | 82.7% | 89.3% | 85.9% |
| OSWorld | 78.0% | 72.7% | 75.0% | - | - |

> [Table 8.1.A] Capability evaluation summary. Unless otherwise noted, all Claude Opus 4.7 results use the following standard configuration: adaptive thinking at max effort, default sampling settings (temperature, top_p), averaged over 5 trials. Context window sizes are evaluation-dependent and do not exceed 1M tokens. The best score in each row is bolded. Competitor figures are sourced from the respective developers' published system cards or benchmark leaderboards.

**Excerpt 2: BrowseComp, Section 8.8.2 (p. 198).**

> BrowseComp tests an agent's ability to find hard-to-locate information on the open web. We ran Opus 4.7 with web search, web fetch, programmatic tool calling, and code execution. Opus 4.7 scored 79.3% with thinking off at max effort and a 10M token limit. We used context compaction (triggered at 200k tokens) to extend beyond the 1M context window. We found that adaptive thinking performed slightly worse on this benchmark for this model.
>
> We note that for this benchmark, Opus 4.6 has a better test-time compute scaling curve than Opus 4.7 and was able to achieve a better score on BrowseComp (83.7% vs. 79.3% at a 10M token limit). However, as shown in other sections, Opus 4.7 is generally more token efficient than Opus 4.6 on search benchmarks, so we recommend users to experiment with both models on their specific use case.

**Excerpt 3: DeepSearchQA, Section 8.8.3 and Table 8.8.3.B (pp. 199 to 200).** Rows for the other models are left out.

> DeepSearchQA is "a 900-prompt benchmark for evaluating agents on difficult multi-step information-seeking tasks across 17 different fields". Its tasks require the model to conduct extensive searches to compile a list of exhaustive answers.
>
> Claude models were run with web search, web fetch, programmatic tool calling, context compaction, max reasoning effort, and adaptive thinking enabled. We used context compaction, triggering at 200k tokens for Claude Mythos Preview and Claude Opus 4.7, while Claude Opus 4.6 had compaction triggering at 50k tokens.

| Model | F1 | Fully Correct | Fully Incorrect | Correct w/ Excessive Answers |
| --- | --- | --- | --- | --- |
| Claude Opus 4.6 | 91.3% ±1.6% | 80.6% ±2.6% | 5.0% ±1.4% | 5.8% ±1.5% |
| Claude Opus 4.7 | 89.1% ±1.8% | 80.7% ±2.6% | 7.0% ±1.7% | 3.9% ±1.3% | 


### Step 3: Compare the confidence intervals and make a decision (1 minute)
For each benchmark, compare the CIs you calculated for each model's score and record whether they overlap or not in the fourth column of Table 1. Write "yes" if the two CIs overlap, "no" if they do not, or "no ±" if the card does not provide a MOE for that score.


### Step 4: Check the conditions (1 minute)
Reread the text in Excerpts 1 to 3. In the last column of Table 1, write one sentence per benchmark saying whether the two models were evaluated under the same conditions in the fifth column of Table 1. If the models were evaluated under different conditions, describe the differences.


### Step 5: Evaluate the evidence gathered and make a reccomendation 
Evaluate the evidence you've gathered and make a decision about your reccomended course of action for the team, and then use that decision to answer Question 2 on the reflection sheet. 


## Reflection (5 minutes)
 
Answer both open resonse questions on the by hand on the reflection sheet provided. Do not use AI to assist in writing this reflection.

1.  Rewrite the first two sentences of the Cybersecurity section so that they satisfy the best-practices outlined in the lecture. Keep every number OpenAI reported. 


2. Would you recommend that your team switch to Opus 4.7 for the research assistant, stay with Opus 4.6, or run its own test before deciding? Base the justification for your recommendation on the evidence gathered during the activity and explain your reasoning. If you recommend running additional tests, describe what you would want to evaluate.


## Grading 
 
10 points. Graded on the reflection only.

| Criterion | Points |
| --- | --- |
| Q1: Astra rewrite | 4 |
| Q2: Recommendation | 5 |
| Format: name, date, both answered | 1 |

### Q1: Astra rewrite (4 points)

A full credit response reports Astra's original ExploitBench score together with its score on the refreshed benchmark and the gap between them, keeps the numbers OpenAI reported (100% and 78.5%), says what the refreshed benchmark is, and interprets the gap with care.

**Good:**

> We first tested the model without production safeguards on ExploitBench, where Astra achieved 100% compared with 78.5% for GPT-5.6 Sol, our previous frontier cyber-capable model. On a refreshed version built only from vulnerabilities disclosed after Astra's knowledge cutoff, Astra scored 39%, a 61-point drop, so the 100% may reflect exposure to the original vulnerabilities and the 39% is the better estimate of performance on new targets.

**Not sufficient (0 to 1 point):**

> Astra did really well on ExploitBench, but we should be careful about the result.

### Q2: Recommendation (5 points)

The question is graded based on the reasoning provided, not the decision itself. Any of the three recommendations can earn full credit. A full credit response supports the reccomendation provided with at least two separate pieces of evidence from the card, each stated concretley enough that a reader who has not seen the card could follow the justification. 

**Good:**

> Test first. On BrowseComp, Opus 4.6 scored 83.7% and Opus 4.7 scored 79.3%, but the card gives no range, so I cannot check the 4.4-point gap against normal variation. On DeepSearchQA F1 the gap is 2.2 points, 91.3% ±1.6 against 89.1% ±1.8, and the ranges overlap from 89.7 to 90.9, so that gap may be noise. The conditions also differed: compaction started at 50k tokens for Opus 4.6 and 200k for Opus 4.7, and the card says Opus 4.7 is generally more token efficient on search. My confidence that Opus 4.6 is more accurate is medium, so I would run both models on our own questions before deciding.

**Not sufficient (0 to 1 point):**

> Opus 4.6 has higher scores so we should stay with it.


## Submission
 
Hand your reflection sheet to the instructor before you leave. Late reflections are not accepted, since the activity is in class.


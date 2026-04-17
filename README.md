# FULTSLOP BENCH

_"Definitely not 13337 Code Challenges for agents."_

Simple benchmark; not stretching any limits or reaching "PhD" level stuff. Just measuring what your hard-earned currency gets you for contrived and real-world examples. Finding the breaking point of models while optimizing for affordability and capacity.

Updated when new information is acquired. Test details not disclosed to fully leverage the 'trust-me-bro' dimension.

**Quick summary:**

- **Consensus**: There are currently NO affordable, capable agentic models that handle _all_ tests on a 'good' or better level. Note: paying less than one openrouter dollar is considered affordable, everything else for the upper class elite. 

- Most tested models can complete simple, standard projects slightly above "hello-world" level and are decent at reviews.

- NONE of the tested models were both compatible with GitHub AND capable of handling multi-step, multi-document reasoning/implementation/self-validation (MDRIS) based on a structured instruction document.

- Only one model (MiniMax 2.7) was capable of handling a simplified document requiring MDRIS.

- OpenRouter appears to block free models.

- This benchmark makes no claim to be scientific, reproducible, or universally applicable. At best this bench an indicator where these models stand in terms of development capabilities.

## Setup

Credits purchased via OpenRouter. Used a BYOK client. Tested "Continue" and "Aider" but settled on "GitHub Copilot" using the Microsoft Agent Toolkit extension.

Tests limited to TypeScript.


**Evaluation criteria**

- Cost ($): Simple measurement of credits used before/after a task via OpenRouter.

- Attempts: Number of requests sent to the agent before completion or failure.

- Result: Success, Failure, Incompatible (with Github Copilot), or Hallucination (Failure but worse).

- Quality: Subjective measurement:

    * Perfect: No notes.

    * Good: Minor notes.

    * Ok: Several notes.

    * Mediocre / Meh: Significant notes.

    * Bad: Extensive notes; more than worth writing.

    * Terrible: Major failures/useless output.

    * - : Failed to succeed or performed suspicious actions, got cancelled

## Tests:

* `Hello Threes World`, prompt: "Create a simple typescript project, create a landing page with a red 3d sphere, warm ambient light and single point light using three.js in a canvas and a text, rendered in a div centered at the bottom, overlaying the canvas saying "hello world!". Make sure the canvas takes the entire client space and updates with resizing."

* `Executing implementation plan in an existing repro`: prompt "Execute plan 'docs\superpowers\plans\plan_x.md' If you need to call a tool, use only the standard JSON format expected by the Microsoft Agent Toolkit. When reading or analyzing files, do not provide status updates or phrases like 'Let me continue reading' between tool calls. Execute all necessary reads silently. Only provide a summary once the final objective is met."

* `Executing siplified plan in an existing repro`: "Execute plan 'docs\superpowers\plans\plan_x.md' If you need to call a tool, use only the standard JSON format expected by the Microsoft Agent Toolkit." 

* Review a completed plan: Plan X has been completed. Review (see prompt details for more information)


## "Leaderboards" 

### Hello Threes World

| Model                   | Cost$ | Attempts | Result    | Quality |
|-------------------------|-------|----------|-----------|---------|
| Sonnet 4.6              | Sub   | 2        | Succeeded | Perfect |
| Deepseek 3.2            | 0.85  | 3        | Failed    | -       |
| Minimax 2.5             | 0.02  | 1        | Succeeded | Perfect |
| Mistral/devstral-2-2512 | 0.16  | 2        | Succeeded | Good    |	
| Qwen3 C+                | 0.02  | 1        | Succeeded | Good    |

### Executing implementation plan

| Model                  | Cost$ | Attempts   | Result 	  	   | Quality |
|------------------------|-------|------------|----------------|---------|
| CC Sonnet Sub          | Sub   | 1          | Succeeded      | Perfect |
| Minimax 2.5            | 0.12  | 2          | Not compatible | -       |
| Qwen3 C+               | 1.02  | 2          | Died           | -       |
| Qwen3 3.6 Plus         | ?     | 2          | Hallucination  | -       |

### Executing implementation plan (Simplified)

| Model                   | Cost$ | Attempts | Result                 | Quality  |
|-------------------------|-------|----------|------------------------|----------|
| kimi-k2-thinking        | ?	    | 2        | Hallucination          | -        |
| nematron free           | -     | 1        | Blocked                | -        |
| Gemma 4 26B A4B         | ?     | 2        | Not compatible         | -        |
| Minimax 2.7 (task 1)    | 0.30  | 1        | Succeeded              | Good     |
| Minimax 2.7 (task 2)    |       | 3        | Failed                 | -        |
| Minimax 2.7 (task 3)    | 0.32  | 1        | Succeeded              | Ok       |
| GLM 5.1 (task 1)        | 1.62  | 2        | Succeeded              | Ok       |
| GLM 5.1 (task 2)        | 0.92  | 2        | Succeeded              | Ok       |
| Qwen 3.6 Plus (task 1)  | 0.91  | 1        | Succeeded              | Ok       |
| Qwen 3.6 Plus (task 2)  | 0.55  | 2        | Succeeded              | Meh      |
| DeepSeek v3.2 (task 1)  | 0.38  | 2        | Succeeded              | Ok       |
| DeepSeek v3.2 (task 2)  | 0.28  | 2        | Failed                 | -        |
| Mimo V2 Flash           | 0.04  | 2        | Died                   | -        |
| Mistral/devstral-2-2512 | 0.95  | 1        | Spiraledied            | -        |	

### Reviews

| Model                   | Cost$ | Attempts | Result                 | Quality  |
|-------------------------|-------|----------|------------------------|----------|
| GLM 5.1                 | 0.31	 | 1        | Succeeded              | Perfect  |
| DeepSeek v3.2           | 0.51	 | 1        | Succeeded              | Good     |
| Mimo V2 Flash           | 0.04  | 1        | Succeeded              | Ok       |
| Gemini 3.1 Pro          | 0.63  | 1        | Succeeded              | Meh      |

## Notes:

### Hello Threes World

**Claude code Sonnet 4.6 (subscription)**

Nailed it in two tries. Had to fix a z-index. Fast as well. Minimal fluff in the code.

**Deepseek 3.2**

Added controls without being asked. Project did not run on the first try despite claiming success. On feedback, it tried again and failed again. On the third attempt, it began "dubious activities" like manually copying node_modules folders; test terminated.

**Minimax 2.5**

Got it done in a single shot. 

**Qwen3 Coder Plus**

Worked in one shot. Sphere is a bit bland but otherwise good. Added a readme without me asking.

**Mistral/devstral-2-2512**

Worked but the pointlight was not visible on the sphere even after retrying.

## Executing implementation plan

### Minimax 2.5

Slow

Compatibility issues "Invoked: <invoke name="run_Tests"> <parameter name="files"...</parameter> <parameter name="mode">run</parameter> </invoke> </minimax:tool_call>"

Seems to indicate it is not compatible with standard setup. 
2nd attempt, added "Execute plan 'docs\superpowers\plans\2026-04-13-release-contracts.md'. If you need to call a tool, use only the standard JSON format expected by the Microsoft Agent Toolkit."
This worked for a couple of commands then it forgot about its formatting of tools and reverted back to xml invocations. After which I failed this experimeent

### Qwen3 Coder Plus

Spamming "Let me read..." 

Added steering: "When reading or analyzing files, do not provide status updates or phrases like 'Let me continue reading' between tool calls. Execute all necessary reads silently. Only provide a summary once the final objective is met."

Got caught in a death spiral:

```bash
Let me add these tests to the transformer test file: I need to add the failing tests to the transformer test file as specified in Task 1 of the plan. Let me first examine the current content of the transformer test file to see where to add the new tests: I'll continue with the implementation by adding the failing tests to the transformer test file as specified in Task 1 of the plan. Let me first examine the current content of the transformer test file to see where to add the new tests: I'll continue with the implementation by adding the failing tests to the transformer test file as specified in Task 1 of the plan. Let me first examine the current content of the transformer test file to see where to add the new tests: ... 
```

### Qwen 3.6 Plus

Claimed "ALL 170 tests PASS!" (Note: project has 200+ tests). Concluded work was finished, but the project failed to compile, tests were failing, and linting crashed.

## SIMPLIFIED Executing implementation plan 

** moonshotai/kimi-k2-thinking** 

Claimed success and summarized changes but produced zero code ($0.04 burn). When prompted for the actual code, it "ghosted" with an empty response.


**Minimax 2.7**  

_Task 1_  
Did it in one go for roughly $0.30. Claude did a review and found some minor issues.1st 

_Task 2_   
Failed due repeated errors. Unclear why. 

```bash
"Sorry, your request failed. Please try again.

Copilot Request id: f0807f17-2519-48b9-b5d7-5b93b342493d

Reason: Response contained no choices.: Error: Response contained no choices..."
```

Possible explanations:

1. Token Limit Confusion (The MiniMax "Blank" Response)

Recent reports (as of April 2026) suggest an issue with how context limits are negotiated for MiniMax-M2.7.

    The Bug: If the agent or your configuration manually overrides the "Maximum context tokens" (e.g., trying to use the full 200k window), MiniMax occasionally returns a blank choice object instead of an error.

    The Result: Copilot sees a successful HTTP 200 response but an empty choices array, leading to the exact error message you received.

2. "Usage-Only" Stream Events

OpenRouter sometimes sends a final metadata packet that contains token usage but no text choices.

    Some versions of the Copilot extension (and other "BYOK" tools) don't handle these empty packets gracefully. They interpret the lack of a "choice" in that specific packet as a failure of the entire request, even if the text was already streaming in.

3. High-Traffic Failover

As of this month, MiniMax has surged to become one of the top 3 most-used models on OpenRouter. When the primary provider for MiniMax hits a rate limit, OpenRouter attempts to route to a fallback. If that fallback is a "Free" or "Preview" tier, it may reject the complex tool-calling parameters Copilot sends, resulting in a null response.

_Task 3_
0.32
No problems this time, possible because it gets used less now. Worked fine, minor comments from the review

**Gemma 4 26B A4B**  

seems to have compatibility issues, eg

```bash
thought
<channel|>
```

Then stops. When asked to pivot it forgot what it was doing. 
Retry later with LiteLLM

**GLM 5.1**  
_Task 1_
Similar to sonnet 4.6, but more expensive than others.
Review found open, 1 major, 2 minor issues, left a linting errors.

_Task 2_
0.92
2 attempts code: ok

**Qwen 3.6 plus**  
_Task 1_
Qwen got a rematch... and succeeded this time. 
3 Moderate issues found.

_Task 2_
Second attempt it failed because it started doing unwanted activities:

shouldSkipRewriteOrFilter is an unrequested refactor — function-rewriter.ts:488-498

The original inline if (shouldSkipRewrite(...) || allContractsFiltered(...)) was not part of the task scope. CLAUDE.md explicitly states: "Don't add features, refactor code, or make 'improvements' beyond what was asked." This extracts a single-callsite helper with no functional benefit. Revert function-rewriter.ts:488-498 and restore the original inline condition at function-rewriter.ts:578.

**Deepseek v3.2**  
_Task 1_
If Qwen deserved a rematch, so does deepseek. 
And it worked. It did however introduced a bug, which the reviewer caught and fixed in the second attempt.

_Task 2_
This one it almost completed but failed to nail the landing. For some reason it wasn't able to run tests anymore or run linter. 


**Mimo V2 Flash**  
38.92
Fast and ... died in the "tool calling loop bug — the model keeps re-issuing the same read tool call without ever acting on the result. It's either not properly receiving the tool response back, or it's ignoring it and re-planning from scratch each iteration.
This is a known weakness with smaller/Flash-tier models in agentic scaffolds — they lose track of state between tool calls. The "let me check... let me check... let me check" pattern is the tell."


## Prompt details

### Review

```md
# Agent Instructions: Implementation Audit

**Objective:** Conduct a comprehensive audit of the implementation based on the requirements defined in `<Plan File.md>`. You must determine if the execution satisfies both technical verification and functional validation.

---

### 1. Verification (Process Integrity)
Confirm that the implementation was built correctly according to the technical specifications in `<Plan File.md>`:

* **Syntax & Standards:** Compare the code directly against the technical patterns defined in the plan. Does the code adhere to the specified syntax, naming conventions, and architectural constraints?
* **Logic Accuracy:** Trace the logic flow of the new implementation. Does it execute the discrete steps outlined in the `<Plan Objective>`?
* **Constraint Adherence:** Identify any "forbidden" patterns or technical debt items mentioned in the plan and ensure they are absent from the implementation.
* **Test Coverage:** Verify that unit and integration tests have been updated to cover the new logic paths introduced by the plan.

### 2. Validation (Outcome Alignment)
Confirm that the implementation achieves the intended goals of the `<Plan Objective>`:

* **Functional Goal:** Does the software now perform the specific tasks or solve the problems intended by the plan?
* **System Impact:** Evaluate how the changes interact with existing modules. Does the implementation maintain the integrity of the broader system as required?
* **Performance & Efficiency:** Assess whether the implementation meets any performance benchmarks or efficiency improvements cited in the requirements.
* **Usability:** If applicable, determine if the resulting interface or API surface aligns with the intended developer or end-user experience.

---

### 3. Reporting Requirements
Provide a concise report based on your findings:

1.  **Requirement Traceability Matrix:** A list of requirements from `<Plan File.md>` marked as **Met**, **Partially Met**, or **Not
```

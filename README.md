# FULTSLOP BENCH

_"Definitely not 13337 Code Challenges for agents."_

Simple benchmark; not stretching any limits or reaching "PhD" level stuff. Just measuring what your hard-earned currency gets you for contrived and real-world examples. Finding the breaking point of models while optimizing for affordability and capacity.

Updated when new information is acquired.

**Quick summary:**

- **Consensus**: There are currently NO affordable, capable agentic models that handle all tests.

- Most tested models can complete simple, standard projects slightly above "hello-world" level.

- Surprisingly, Deepseek 3.2—touted as a cost-effective alternative to Sonnet 4.6—was unable to provide a working solution.

- NONE of the tested models were both compatible with GitHub AND capable of handling multi-step, multi-document reasoning/implementation/self-validation (MDRIS) based on a structured instruction document.

- Only one model (MiniMax 2.7) was capable of handling a simplified document requiring MDRIS.

- OpenRouter appears to block free models.

- This benchmark makes no claim to be scientific, reproducible, or universally applicable.

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

    * Mediocre: Significant notes.

    * Bad: Extensive notes; more than worth writing.

    * Terrible: Major failures/useless output.

    * - : Failed to succeed or performed suspicious actions, got cancelled

## Tests:

* `Hello Threes World`, prompt: "Create a simple typescript project, create a landing page with a red 3d sphere, warm ambient light and single point light using three.js in a canvas and a text, rendered in a div centered at the bottom, overlaying the canvas saying "hello world!". Make sure the canvas takes the entire client space and updates with resizing."

* `Executing implementation plan in an existing repro`: prompt "Execute plan 'docs\superpowers\plans\2026-04-13-release-contracts.md' If you need to call a tool, use only the standard JSON format expected by the Microsoft Agent Toolkit. When reading or analyzing files, do not provide status updates or phrases like 'Let me continue reading' between tool calls. Execute all necessary reads silently. Only provide a summary once the final objective is met."

* `Executing siplified plan in an existing repro`: "Execute plan 'docs\superpowers\plans\2026-04-15-keepcontracts-step1-function-rewriter.md' If you need to call a tool, use only the standard JSON format expected by the Microsoft Agent Toolkit." 


## "Leaderboards" 

### Hello Threes World

| Model                   | Cost$ | Attempts | Result    | Quality |
|-------------------------|-------|----------|-----------|---------|
| Sonnet 4.6              | Sub   | 2        | Succeeded | Perfect |
| Deepseek 3.2 		        | 0.85  | 3  	  	 | Failed    | - 	     |
| Minimax 2.5  			      | 0.02  | 1 		   | Succeeded | Perfect |
| Mistral/devstral-2-2512 | 0.16  | 2		     | Succeeded | Good    |	
| Qwen3 C+	   			      | 0.02  | 1		     | Succeeded | Good    |

### Executing implementation plan

| Model 	   			       | Cost$ | Attempts   | Result 	  	   | Quality |
|------------------------|-------|------------|----------------|---------|
|CC Sonnet Sub 			     | Sub 	 | 1 		      | Succeeded      | Perfect |
|Minimax 2.5   			     | 0.12  | 2 		      | Not compatible | -       |
|Qwen3 C+				         | 1.02  | 2		      | Died		       | - 		   |
|Qwen3 3.6+				       | ?     | 2		      | Hallucination  | - 		   |

### Executing implementation plan (Simplified)

| Model 	   			        | Cost$ | Attempts | Result 	      | Quality |
|-------------------------|-------|----------|----------------|---------|
| kimi-k2-thinking	      | ?	    | 2 		   | Hallucination  | -       |
| nematron free 		      | -     | 1		     | Blocked		    | - 		  |
| Gemma 4 26B A4B 		    | ?     | 2		     | Not compatible | - 		  |
| Gemma 4 26B A4B 		    | ?     | 2		     | Not compatible | - 		  |
| Minimax 2.7 		  	    | 0.30  | 1		     | Succeeded      | Good	  |

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

Compatibility issues "Invoked: <invoke name="run_Tests"> <parameter name="files">["c:\\Users\\lassc\\Code\\typescript\\fsprepost\\test\\transformer.test.ts"]</parameter> <parameter name="mode">run</parameter> </invoke> </minimax:tool_call>"

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


** Minimax 2.7 **

Did it in one go for roughly $0.30. Claude did a review and found some minor issues.


** Gemma 4 26B A4B **

seems to have compatibility issues, eg

```bash
thought
<channel|>
```

Then stops. When asked to pivot it forgot what it was doing.


## Models remaining

| Model ID (OpenRouter)                  | Est. Cost (In/Out) | Strengths / Notes                     |
|----------------------------------------|--------------------|---------------------------------------|
| qwen/qwen-3-coder-32b-instruct         | $0.07 / $0.15      | Successor to the old free Qwen Coder. |
| deepseek/deepseek-v3.2:nitro           | $0.25 / $0.38      | Unified coder/reasoning (Fast tier).  |
| zhipuai/glm-4-9b-chat                  | $0.08 / $0.08      | High precision on boilerplate code.   |
| meta-llama/llama-4-scout-8b            | $0.10 / $0.20      | Massive context, good for long files. |
| mistralai/mistral-small-3-24b          | $0.10 / $0.10      | Excellent spatial logic for Three.js. |
| deepseek/deepseek-r1-distill-llama-70b | $0.20 / $0.50      | Best "Thinker" for fixing failed code.|

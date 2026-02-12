---
layout: default
title:  "AI Tooling One Year Later"
date: 2026-02-10 
categories: AI
---

# AI Tooling One Year Later

One year ago, I created an AI application to generate insightful text from multiple inputs.
At that time, success was largely driven by model sophistication.
The dominant question was: which model is smartest?
Local models were entirely insufficient for nuanced synthesis or credible research.
They struggled with hallucinations, missed context, and unreliable reasoning.
Frontier models accessed via APIs produced good results, especially when prompts were carefully structured.
Still, outputs required substantial human correction and steering.
Web UIs like ChatGPT, Claude, and Perplexity produced vastly superior results.
Their advantage was not just model size, but orchestration, search depth, retry logic, and synthesis layers invisible to the user.

![AI Android chasing Runbook]({{ "/assets/images/AI-Tooling-One-Year-Later/runbook-race.png" | relative_url }})

Much has changed in the past year, so I thought it was a good time to reconsider the approach.
A job application is a good reference case for evaluating AI workflow approaches, and the same patterns show up in investment research where key signals can be subtle and hard to anticipate.
In this article, I focus on the job application example.

Your inputs are typically the target company and the job description.
These act as explicit constraints.
You also have a suitable resume and one or more sample cover letters that demonstrate a personal communication style.
These anchor both content and tone.

Covers are not merely formalities.
They are tools for explaining alignment.
More importantly, writing a cover letter forces synthesis.
It challenges the author to think beyond the job description and infer unstated organizational needs using external signals.
Often in leadership roles, hiring managers do not explicitly outline their true needs.
They prefer ambiguity, either to avoid signaling internal issues or to keep options open.
You will never see a job description that says, "Our developers distrust security leadership, and we need someone who can repair that relationship."
Yet that is often exactly the problem to be solved.

## Scenarios to Explore

I explored four scenarios, each representing a different tradeoff between capability, control, effort, and insight.

1. **ChatGPT or Claude Web UI**

This is the baseline scenario against which the other approaches are measured.
The web UI performs deep research, ingests all inputs, and proposes cover letter topics in the form of a draft letter.
In practice, you must review the research and redirect the model toward more accurate or relevant topics.
Once redirected, the UI excels at polishing language, tightening structure, and avoiding basic disqualifying errors like grammar, spelling, or formatting issues.
However, controlling output quality requires constant vigilance.
Even the newest models drift from constraints unless repeatedly reminded.
The intelligence is there, but compliance is fragile.

Having set Scenario 1 as the web UI, I brainstormed the remaining scenarios with Claude Web (Opus 4.5), Claude CLI (Opus 4.5), and ChatGPT 5.2 Web.
Here are the three other scenarios I settled on.

2. **Claude Projects**

Claude projects, similar to OpenAI projects and custom GPTs, allow pre-canned instructions, reference documents, and scoped iteration.
This reduces prompt repetition and improves consistency across runs.
Iteration remains conversational, which preserves usability.
However, responses can still drift over time unless constraints are restated.
Projects feel closer to structured prompting than to fully agentic systems.
They improve input logistics but do not fundamentally change research depth or output quality.
Overall, projects tend to deliver results similar to the standard web UI when given the same inputs.

3. **Claude CLI Skills**

Claude CLI Skills were not available a year ago.
They introduce a different abstraction by decomposing a task into multiple prompts orchestrated locally.
Each skill handles a narrow responsibility, such as research, drafting, synthesis, or editing.
Outputs are written to files, enabling inspection, revision, and versioning.
Iteration happens through co-editing local artifacts rather than conversational back and forth.
This increases perceived control and auditability, but research quality is usually weaker than the web UI.
The Claude CLI will tell you that web UI research is better, and in practice it is.

4. **Multi-Agent Pipeline**

The final scenario is a fully custom pipeline with nodes for research, synthesis, topic generation, and cover drafting.
This approach offers maximal transparency and tunability.
Each step can be tested, swapped, or optimized independently.
In practice, each step **must** be optimized, and this is where much of the human effort remains.
A major downside is effort.
This path requires roughly an order of magnitude more human work.
More importantly, even with significant engineering, matching the breadth and depth of web UI research remains out of reach.
Research efficacy is the second major downside. 

The rest of this article examines these options and extracts general lessons.

### Scenario 1: Chatbot Web UI

The web UI is the primary **component** in this solution.
The user should enable web search and research features.

Creation **effort** is minor, with most work spent iterating a reusable prompt that can be carried into other scenarios.
Expect to adjust the prompt and cover samples over time.
Once the prompt and guidance inputs are stable, the entire process can be completed in 30 minutes.

Since this is a one-shot way to get started, the **input** prompt must be complete and accompanied by the company name, optional URL, job description, resume, and at least one cover sample.

The web UI **usage** case is the fastest to start.
The hard part, creating the prompt, can be done iteratively with the LLM in chat mode.
For example, once you get a good result, a useful last step is to ask the LLM to create a reusable prompt to reproduce that result next time.

To this point, the process's main **challenge** is ensuring you verify the accuracy of the claims implied by the chosen cover topics.
The LLM tends to present claims with equal confidence.
Beyond cover quality, there are important tasks left undone.
For example, you will want to keep a log of job submissions and their status.
Log entries will still need manual normalization because one-shot runs miss small details.
You will also want to preserve submitted artifacts for future reference.
Do this offline, since LLMs are not reliable archival storage.

Using the web UI is the default approach for most users.
The **lesson** for the remaining scenarios is that having a high-quality prompt is the essential step, and the LLM can help you build it.
I reuse the same inputs for the remaining scenarios.

### Scenario 2: Claude Projects

The major **component** in this scenario is a persistent project workspace that encapsulates prompts, reference documents, and example artifacts.
Unlike the web UI's fully ad hoc nature, the project introduces a lightweight form of state by anchoring instructions and inputs across sessions.

Creation **effort** is still modest, but slightly greater than Scenario 1.
Initial setup requires curating and uploading stable prompt instructions, representative resumes, and multiple cover samples.
The upfront work pays off only if the project is reused across multiple iterations.

**Inputs** are largely identical to the web UI scenario: company name, optional URL, job description, resume, and prior cover samples.
The difference is that many of these inputs are pre-loaded once and assumed to persist, reducing repeated copy-paste friction.

The **usage** experience feels like a directed version of the web UI.
You arrive and the tool indicates your responsibilities.
Iteration remains conversational, and it is easy to refine outputs incrementally.

**Challenges** center on prompt drift as processing proceeds farther from the initial run.
Responses slowly diverge from original constraints unless you restate them.
The project abstraction reduces repetition but does not eliminate the need for vigilance.
Research depth is comparable to the web UI, but it is not improved by the project construct itself.

The primary **lesson** informing the next scenario is that persistence alone is not control.
While projects improve logistics and consistency, they do not provide explicit orchestration, verification, or decomposition of tasks.
To gain stronger guarantees over outputs, the process must be broken into smaller, inspectable steps rather than relying on a single, ever-growing instruction set.

### Scenario 3: Claude CLI Skills

The major **components** in this scenario are the CLI runtime, a custom skills library (multiple small prompts with narrow responsibilities), and local artifacts (markdown files, PDFs, and folders) that act as the system of record.
Instead of one large prompt that tries to do everything, the work is decomposed into steps such as research, extraction, synthesis, drafting, and edit suggestions.

**Effort** to create is moderate.
Creating one skill is straightforward, but creating a reliable set of skills requires designing interfaces between them, defining file formats, and deciding what each step must output for the next step to succeed.
The effort is front-loaded into structure: naming, directory layout, and repeatable invocation patterns.
Much of the scaffolding can be generated quickly with Claude, but it still requires human review and refinement.

**Inputs** are reused as-is, but you must be more intentional about file formats and ordering.
That is acceptable because the goal is for the tooling to enforce process and produce more consistent, controlled output.

**Usage** relies on the human as the orchestrator.
You run a step, inspect the results, iterate if needed, and then run the next step.
This is not a black-box tool.
The result is a stronger sense of control and easier debugging, especially when outputs are versioned in Git.

The most prominent **challenge** is the relatively poor quality of web research available via the CLI.
Web research through CLI tooling is weaker than web UI research, and shallow inputs produce shallow outputs even if the prompting is excellent.
In practice, you either bring in research from a web UI or build an external search capability, for example via MCP.

Other challenges emerge as soon as the workflow is decomposed into discrete skills.
Decomposition exposes the need for human evaluation of each step's output.
This is the first time the process forces explicit success criteria and test iterations to determine the right prompts and approach.
That burden becomes even more pronounced in the multi-agent pipeline scenario.

A practical constraint is rate limiting.
In my experience, the Claude CLI tends to hit Pro subscription limits faster than the web UI, although I do not have consistent statistics to prove it.

A couple of important **lessons** lead into the next scenario.
First, visibility into each step's output quality, plus the ability to iterate inputs inexpensively, becomes a real advantage.
Second, decomposition offers the promise of tighter control over outputs, but it does not automatically solve research completeness, termination logic, or cross-step verification.
Third, search quality is materially lower via the CLI, so improving search capability or providing outside research input is required.
To approach web UI quality, the pipeline must become more agentic through iterative research loops, explicit scoring, and structured intermediate outputs that can be validated before proceeding.

### Scenario 4: Multi-Agent Pipeline

**Components** include a fully custom Python command line application.
This approach lets you choose building blocks, for example pdfplumber for PDF extraction and SQLite for caching HTTP and LLM responses.
You can also select different models for different steps.
That flexibility creates many choices.
Those choices drive experimentation, the need for intermediate result visibility, and criteria for judging utility.
If you are vibe coding, the LLM will not anticipate these needs unless you specify them.

In this light, I experimented with the following options.

* Search engines: SearXNG vs Anthropic Web Search.
* Local models via Ollama: phi4:14b and qwen3:30b-a3b were usable.
  * Seven others produced incomplete results on an RTX 4090 16GB: deepseek-r1:14b, gemma3:12b, glm-4.7-flash, gpt-oss:20b, llama3, qwen2.5:32b, and phi4-reasoning.
* Cloud models: claude-opus-4.5 and claude-sonnet-4.5.

The **effort** to create this pipeline is high.
As with a real product team, you must sketch the architecture and design.
While the LLM is a good partner, it will not take initiative on NFRs like testability.
As progress continues, it will also introduce duplicated functionality across modules.
On the other hand, you learn quickly and benefit from the LLM's knowledge of APIs and syntax.
However, that knowledge is not perfect, so testing and review remain essential. 
Reading API documents is important to ensure proper and complete use of available tooling. 

**Inputs** remain the same as in other scenarios, but formats must be tightly controlled.
For example, you become responsible for converting PDF inputs into clean text.
In the web UI and CLI Skills scenarios, input format is less restricted.

**Usage** is driven through a complex command line.
Parameters include company, job description, resume, cover samples, external research reports, output destination, search engines, model providers and models, and which processing steps to execute.
Most parameters can be defaulted for normal use, but for testing you will want to specify them explicitly.
In practice, you will also want test driver scripts to run multiple scenarios, capture basic metrics, and produce a comparison report.
Very little of this is anticipated by a vibe coding partner.
It is on you to define the test plan, implement the harness, and decide what success looks like.

**Challenges** are many.
First, effort: most of it goes into testing process nodes and making LLM and component choices.
In my experience, at least two thirds of the work is iterative development.
Second, local models must be thoroughly tested across a variety of inputs.
A model may load and execute, but memory constraints, especially with MoE variants, can cause failures on some inputs even though others succeed.
Given different objectives, both local and cloud models vary in effectiveness.
If you are already going to the trouble of making multiple LLM calls, it is worth optimizing model and step selection.
However, optimization itself becomes a major challenge because, compared to the web UI, optimization can become a project of its own. 

Consider one example.
A deep research run in the web UI might issue 300 searches.
The same search via a cloud search API might perform only 10.
Local search via SearXNG can also be less effective, depending on configuration and sources.
In my experience, web UI deep research identifies at least double the number of important results with much higher signal validity rate.

If I executed a fifth scenario, what **lessons** would carry forward?
First, search quality is a crucial input regardless of which LLM models you select.
The fastest way to improve search quality is to use the web UI.
The next option is a cloud or if absolutely necessary, a local search API.
However, both require engineering to iterate on results and reissue new queries.
That iteration loop is a large part of why web UI deep research tools obtain superior results.
Unfortunately, replicating 300 searches via an API can cost 3-5x more.
It is unclear how far programmed search can improve without breaking the budget.

Second, segmenting the process provides added control over results and exact formats.
In this multi-agent pipeline, the final step's only job is reporting, which is converting data gathered earlier into desired formats.
That part can work quite well, and for mass production purposes, dedicated reporting is a must.
However, be ready to scaffold for testing and evaluation.
Vibe coding tools will not drive that work, so you must.

That said, a multi-agent pipeline is not the last option.
Ideally, frameworks exist that automate via the web UI.
An AI browser such as Anthropic Comet might be a candidate.
Similarly, Chrome extensions such as SuperPower ChatGPT have potential.
Desktop automation tools such as Claude Desktop or AskUI also come to mind.
A major downside is that web UI terms of service often prohibit accessing services through non-human means.
Accordingly, efforts to automate the web UI can be exposed legally and practically.

<!--
**Rubric for Scenarios** Not to be part of final article
  Check that outline follows
    The major components
    Effort to create
    Inputs provided 
    Usage experience 
    Challenges encountered 
    Lessons informing next scenario 
-->
## Takeaways Above the Tech

Frontier models have come a long way in the last 12 months, largely through improvements in available tools, including search.
Last year's effort was limited by the small amount of context an LLM could consume and by inconsistent adherence to prompts.

At this point, the greatest value lies in segmenting the problem and giving LLMs the highest quality inputs possible.
Semi-custom approaches such as CLI Skills, or fully custom pipelines such as the multi-agent scenario, can produce highly controllable outputs.
However, they require significant engineering time and cost, even when an AI coding agent handles much of the mechanical work.

For now, a human orchestrator provides the best effectiveness tradeoff for all but the most highly scaled operations.
Coach humans on web UI prompting for each step.
Automate some steps while leaving others in the web UI.
This approach also reduces terms of service exposure from automating web UI interactions.
In this example, research and cover iteration should remain interactive steps.

![Runbook and AI running together](/assets/images/AI-Tooling-One-Year-Later/runbook-together.png)
# Prompt library

Copy-paste prompts for Claude Code, grouped by phase. Replace the `{placeholders}` with your own details.
Source: the Claude Code docs prompt library (code.claude.com/docs/en/prompt-library), plus FitnessCEO-specific prompts at the bottom.

**★ Start here (try these first):** 1 · Get oriented → 2 · Find where something happens → 3 · Find and fix a failing test → 4 · Write tests, run them, fix failures → 5 · Review your changes before you commit

---

## Discover

### Onboard
- **Get oriented in a new repository** ★1
  `give me an overview of this codebase: architecture, key directories, and how the pieces connect`
  *Why:* describe what you want to know, not which files to read. *Make it stick:* run `/init` to set up CLAUDE.md.

### Understand
- **Explain unfamiliar code**
  `explain what {path} does and how data flows through it. write it up as {format}`
  e.g. path = `src/scheduler/queue.ts`, format = `an HTML page with a diagram, then open it in my browser`
  *Why:* name the file and the answer format.
- **Find where something happens** ★2
  `where do we {behavior}?` — e.g. `validate uploaded file types`
  *Why:* search by behaviour, not filename.
- **Check what breaks before you delete**
  `what would break if I deleted {target}?` — e.g. `the retryWithBackoff helper`
- **Trace how code evolved**
  `look through the commit history of {path} and summarize how it evolved and why`
- **Scope a change before you start** (Product, Design)
  `which files would I need to touch to {change}?` — e.g. `add a dark mode toggle to settings`
- **Ask the codebase a product question** (Product)
  `I am a {role}. walk me through what happens when a user {action}, from the UI down to the result`

## Design

### Plan
- **Plan a multi-file change before touching code**
  `plan how to refactor the {target} to {goal}. list the files you would change, but don't edit anything yet`
  *Why:* separates exploration from edits. Shift+Tab toggles plan mode.
- **Draft a spec by interview**
  `I want to build {feature}. interview me about implementation, UX, edge cases, and tradeoffs until we have covered everything, then write the spec to SPEC.md`
  *Make it stick:* save as a `/spec` skill.
- **Turn a meeting into tickets** (needs issue tracker connector)
  `read {input} and write up the action items, then create a ticket in {tracker} for each one, with acceptance criteria`
- **Map edge cases before building**
  `list the error states, empty states, and edge cases for {feature} that the design needs to cover`

### Prototype
- **Turn a mockup into a working prototype** (paste the mockup first)
  `here is a mockup. build a working prototype I can click through, matching the layout and states shown`
- **Implement from a screenshot and self-check** (paste the design; needs browser/preview)
  `implement this design, then take a screenshot of the result, compare it to the original, and fix any differences`
  *Why:* gives Claude a verification loop.

## Build

### Implement
- **Follow an existing pattern**
  `look at how {example} is implemented to understand the pattern, then build {new} the same way`
- **Generate docs for undocumented code**
  `find {scope} without {format} comments and add them, matching the style already used in the file`
- **Add a small, well-defined feature**
  `add a {endpoint} endpoint that returns {payload}`
- **Build a small internal tool from scratch**
  `create a {tool} using HTML, CSS, and vanilla JavaScript, then open it in my browser`
- **Work an issue end to end**
  `read issue #{issue}, implement the fix, and run the tests`
- **Find and update copy across the codebase**
  `find every place we say "{copy}" or a close variant, show me each one in context, then update them all to "{new}". leave tests and the changelog alone`
- **Draft a document from past examples**
  `read the {examples} in {folder} to learn the structure and voice, then draft a new one for {topic}`

### Test
- **Write tests, run them, fix failures** ★4
  `write tests for {path}, run them, and fix any failures`
- **Drive implementation from tests**
  `write tests for {feature} first, then implement it until they pass`
- **Fill gaps from a coverage report**
  `read {report} and add tests for the lowest-covered files until each is above {target}%`

### Refactor
- **Migrate a pattern across the codebase**
  `migrate everything from {from} to {to}: identify every place that needs to change, then make the changes`
- **Port code to another language**
  `port {source} to {target}, keeping the same {keep}`
- **Optimize against a measurable target**
  `optimize {target} to bring {metric} from {current} down to under {goal}`
- **Fix a precise visual bug**
  `the {element} extends {amount} beyond the {container} on {viewport}. fix it.`

### Review
- **Review your changes before you commit** ★5
  `review my uncommitted changes and flag anything that looks risky before I commit`  (or `/code-review`)
- **Review a pull request**
  `review PR #{pr} and summarize what changed, then list any concerns`
- **Review infrastructure changes before applying** (paste plan output)
  `here is my Terraform plan output. what is this going to do, and is anything here going to cause problems?`
- **Run a security review with a subagent**
  `use a subagent to review {path} for security issues and report what it finds`
- **Catch issues before formal review**
  `review {file} for {concerns} and list anything I should fix before it goes to {reviewer}`

### Steer
- **Course-correct a wrong approach**
  `that is not right: {feedback}. try a different approach`
- **Narrow the scope of a change**
  `that is too much. keep only the changes to {scope} and undo your other edits`
- **Turn a correction into a rule**
  `you keep {mistake}. add a rule to CLAUDE.md so this stops happening`

## Ship

### Git
- **Resolve merge conflicts**
  `resolve the merge conflicts in this branch and explain what you kept from each side`
- **Commit with a generated message**
  `commit these changes with a message that summarizes what I did`
- **Open a pull request from a ticket**
  `find the ticket about {topic} in {tracker} and open a PR that implements it`

### Release
- **Draft release notes from git history**
  `compare {from} to {to} and draft release notes grouped by feature, fix, and breaking change`
- **Write a CI workflow**
  `write a GitHub Actions workflow that {steps} on every push to {branch}`

## Operate

### Debug
- **Find and fix a failing test** ★3
  `the {test} test is failing, find out why and fix it`
- **Investigate a reported error**
  `users are seeing {symptom} on {where}. investigate and tell me what is going on`
- **Fix a build error at the root** (paste the error)
  `here is a build error. fix the root cause and verify the build succeeds`

### Incident
- **Investigate a production incident**
  `{symptom}. check the logs, recent deploys, and config changes, then tell me the most likely cause`
- **Diagnose from a console screenshot**
  `here is a screenshot of {console}. walk me through why {resource} is failing and give me the exact commands to fix it`
- **Query logs in plain English** (needs log store connector)
  `show me all {events} for {scope} over {timeframe}. write the query, run it, and tell me what stands out`

### Data
- **Analyze a data file**
  `read {file}, summarize the key patterns, and write the results to {output}`
- **Generate variations from performance data**
  `read {file}, find the underperforming {items}, and generate {n} new variations that stay under {limit} characters`

### Automate
- **Turn a recurring task into a skill**
  `create a /{name} skill for this project that {steps}`
- **Add a hook for repeat behavior**
  `write a hook that {action} after every {event}`
- **Connect a tool with MCP**
  `connect {server} via MCP so you can read its {data} directly`
- **Capture what to remember for next time**
  `summarize what we did this session and suggest what to add to CLAUDE.md`

---

## What makes these prompts work
1. **Describe the outcome, not the steps.** — `add rate limiting to the public API and make sure existing tests still pass`
2. **Give it a way to check its own work.** — `write the migration, run it against the dev database, and confirm the schema matches` (or `/verify`)
3. **Point at a reference.** — `add a settings page that follows the same layout as the profile page`
4. **State the measurable target.** — `get the bundle size under 200KB and show me what you removed`
5. **Give it the artifact.** — `why is the build failing? @build.log`
6. **Say how you want the answer.** — `explain how the payment retry logic works as an HTML page with a diagram, then open it in my browser`

Once a prompt works, make it repeatable: save it as a skill (`/command`), record conventions in CLAUDE.md, and use plan mode for big or risky changes.

---

## FitnessCEO extras — funnels, pages and business (same patterns applied)
- **Brutal offer teardown**
  `act as a sceptical direct-response strategist. tear apart {offer/page}: who it's for, the promise, proof, price, objections, CTA. rank the 5 biggest conversion killers and rewrite the top one. don't soften it`
- **Landing page benchmark + self-check**
  `build {page} for {audience}, then screenshot it at mobile and desktop, compare against the best-in-class pattern (single CTA, above-the-fold promise, social proof, fast load) and fix every gap`
- **Funnel edge-case map**
  `list every drop-off point, error state, empty state and abandoned-step scenario in {funnel}, and what recovery (email/SMS/retargeting) each one needs`
- **Measurable funnel target**
  `improve {step} to move {metric} from {current} to {goal}. show me the hypotheses ranked by expected impact and effort before changing anything`
- **Claims check before launch**
  `review {copy/page} for unsupported health or results claims, missing disclaimers, and anything that would get ads rejected, and list fixes before it goes live`
- **On vs in the business check**
  `here's my week/plan: {list}. tell me honestly which items are me working in the business, what to delegate/automate/kill, and the one thing that would move revenue most`

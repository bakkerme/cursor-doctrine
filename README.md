# cursor-doctrine
Personal notes on Cursor use for commercial grade software engineering.

# Overall Notes
- Innacuracy in prompts can lead to weird outcomes. Sometimes the LLM will tell you that you're wrong if you're confident and false, but you'll probably not believe it. Sometimes it'll just do what you tell it to, not what you think you're telling it to do.

# Outstanding Questions
- Where is the line between tasks that are quicker for humans vs teaching the AI
- How do we optimise the AI to begin to take over smaller and smaller task?

# Models
## Claude 3.5 Sonnet
### Initial Assumptions + Community thoughts
- Basic, mostly dependable

### IRL Experience
- Best default
- Uses tools and applies diffs the most consistent out of all models

## o4-mini
### Initial Assumptions + Community thoughts
- Good for planning

### IRL Experience
- Thinking Model
- Slow, no \<think> tokens available
- Poor at grepping and navigating the codebase, requires precise context management
- Is this an opportunity to use @codebase?

# Effective Prompts

## Planning a basic new feature
Included context: `rssmock.md`, `processor.go`, `mocks.go`
```
This plan needs to now include the ability to load in RSS mocks based on the persona being loaded.

The path the data is dumped is as follows: 
{PROJECT_ROOT}/feed_mocks/rss/{PERSONA_NAME}/{PERSONA_NAME}.rss
{PROJECT_ROOT}/feed_mocks/rss/{PERSONA_NAME}/{POST_ID}.rss

There is already RSS mocking code in processor.go. Ensure that is represented in this plan, and the required changes.

Update the rssmock.md document with a new section detailing the plan to make the required changes.
```

RSS Mocking in processor.go is innacurate information, it's actually in mock.go, which lead to a bad result initially, where the file reading was added to the RSS reading code. After including mocks.go, the results were improved.

Without asking it to create a new section, it updated the existing docs in an unnatural way that may have resulted in bad task following during implementation.

## Creating Feature Docs
RSS is the Go module in question.

```
@rss Let's start producing some documentation for the rss module.

Include:
* Features
* Directory structure
* Notable functions and types

This document should be ./docs/rss.md
```

# Rules
- An outline of project structure in an .mdc file should suffice for practical use
  - Should each module be linked to their own docs? Will the LLM actually read them umprompted?

# Workflows

## Planning/Documenting
- Ask the LLM to start a markdown planning document
- Open the doc and provide feedback on sections with a clear structure the LLM can follow
  - Like (USER: Some feedback here)
- Ask it to use full links to files when referencing behaviour. This reduces grepping and lookups, increasing speed.
- Feel free to make changes too, but I've found the LLM can reproduce deleted sections (needs more research)
- Ask the LLM to refactor based on the provided feedback annotations.

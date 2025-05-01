
With @codebase vs without, no other context other than rules, minimal prompting.
```
@codebase
The llm batch system is currently hardcoded. Make it configurable.
claude-3.5-sonnet
```

Results:
- Perfect results
- Second run did not create the Validation rule. (Added this into the envar rules.)
- Third run, eventually successful. It got confused looking for LLM processor, despite already identifying where the change needed to be made. It's unclear why it did that, but it increased task time substantially.

Without Results:
- Eventually found the specification rule and produced identical results.
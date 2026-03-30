# Context7 MCP playbook

## Why use Context7 in this repo

Use Context7 when the task depends on current framework or library behavior, example patterns, or version-specific guidance. Do not use it as a substitute for understanding the local codebase.

A good workflow is:

1. Read the repo files first.
2. Identify the exact library question.
3. Use Context7 for that narrow question.
4. Compare the docs result with the local code before editing.
5. Explain the change in plain language.

## Setup

```bash
export CONTEXT7_API_KEY=your_key_here
claude
```

Then in Claude Code:

```text
/mcp
```

## Good prompts

- `Use Context7 to confirm the current FastAPI recommendation for startup/lifespan handling.`
- `Use Context7 to verify current httpx timeout and error handling examples before changing feed fetching.`
- `Use Context7 to compare current FastAPI TestClient guidance with our existing tests.`

## What not to do

- Do not ask Context7 broad questions when the repo itself already answers them.
- Do not let documentation lookup replace tests.
- Do not copy large examples without adapting them to the actual repo.

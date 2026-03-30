# Context7 Status Bridge

Context7 Status Bridge is a compact internal integration service that normalizes external product-status incidents into a local format the support team can query.

This repo isolates the labs that depend on:

- project-scoped MCP via `.mcp.json`
- Context7 for current library and framework documentation
- integration-oriented code changes
- workflow automation later with commands, hooks, or subagents

## Scenario

The support engineering team monitors third-party product status feeds. Different vendors publish different payload shapes, and the internal team wants a single small service that:

- imports incidents from a provider feed
- stores them locally for a dev workflow
- exposes a small API for recent incidents and summaries
- supports provider-specific parsing without becoming a huge framework exercise

## Repository map

```text
.
├── .claude/
│   ├── settings.json
│   └── settings.local.example.json
├── .github/workflows/ci.yml
├── .mcp.json
├── .vscode/
│   ├── extensions.json
│   └── tasks.json
├── CLAUDE.md
├── data/fixtures/statuspage_sample.json
├── docs/
│   ├── architecture.md
│   ├── mcp-playbook.md
│   ├── module-fit.md
│   └── starter-files.md
├── pyproject.toml
├── scripts/
│   ├── bootstrap.sh
│   └── run_dev.sh
├── src/status_bridge/
│   ├── api/
│   │   ├── health.py
│   │   └── incidents.py
│   ├── app.py
│   ├── cli.py
│   ├── config.py
│   ├── db.py
│   ├── feeds.py
│   ├── models.py
│   ├── repository.py
│   └── service.py
└── tests/
    ├── test_api_incidents.py
    ├── test_feeds.py
    ├── test_health.py
    └── test_service.py
```

## Quickstart

```bash
uv sync --extra dev
uv run python -m status_bridge.cli import-fixture
uv run uvicorn status_bridge.app:app --reload
```

Useful endpoints:

- `http://127.0.0.1:8000/docs`
- `http://127.0.0.1:8000/healthz`
- `http://127.0.0.1:8000/incidents`
- `http://127.0.0.1:8000/incidents/summary`

## Context7 setup

Export your Context7 API key before launching Claude Code:

```bash
export CONTEXT7_API_KEY=your_key_here
claude
```

In Claude Code, run `/mcp` to confirm that the project-scoped `context7` server is visible.

## Good first MCP prompts

```text
Use Context7 to confirm the current FastAPI testing pattern for our stack before editing the API tests.
```

```text
Use Context7 to verify current httpx client usage for timeout and error handling, then compare it with our feed-fetching code.
```

```text
Use Context7 to look up current FastAPI lifespan guidance and tell me whether our app startup pattern should change.
```

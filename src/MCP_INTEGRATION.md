## Exercise: Integrate MCP with Copilot

This document walks through a minimal, hands-on exercise to extend GitHub Copilot with a Model Context Protocol (MCP) data source. The goal is to show a safe, repeatable way to surface repository-specific context to Copilot-like systems.

Steps
1. Create a small MCP provider service that exposes a JSON endpoint with contextual information (e.g., function signatures, recent PR summaries, test failures). For example, a tiny Flask or FastAPI service that returns a JSON object at `/mcp/context`.
2. Define the context schema your MCP provider will serve. Keep it small and focused (titles, descriptions, timestamps, and optional URLs).
3. Host the MCP provider locally (or as a dev container) and ensure it's reachable from your development environment.
4. Configure the Copilot or MCP-capable client to query the MCP endpoint and include those snippets as additional context for completions. Follow the client's documentation for how to plug an external context provider into the prompt or request pipeline.
5. Iterate: add more context items (test output, failing stack traces, critical TODOs) and tune which items are surfaced.

Example minimal JSON schema

```json
{
  "repo": "owner/repo",
  "items": [
    {"id":"tests-failure-1","title":"Unit tests failing in CI","summary":"3 tests failing in tests/test_api.py","url":"https://ci.example.com/build/123"}
  ]
}
```

Security and privacy
- Only surface non-sensitive, public, or repository-scoped information.
- Avoid sending secrets, tokens, or personal data to any external LLM provider.

Next steps I can take for you
- Scaffold a minimal MCP FastAPI provider (`src/mcp_provider.py`) and add an example client call in `src/static/app.js` to demonstrate fetching MCP context. Ask me to implement this and I will create the branch, code, tests, and PR.

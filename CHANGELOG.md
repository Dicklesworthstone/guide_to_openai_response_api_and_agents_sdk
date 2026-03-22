# Changelog

All notable changes to **Guide to OpenAI Response API and Agents SDK** are documented here.

This repository is a single-document reference guide (not a versioned library), so the changelog tracks content milestones rather than semver releases. There are no tags or GitHub Releases as of 2026-03-21.

Repository: <https://github.com/Dicklesworthstone/guide_to_openai_response_api_and_agents_sdk>

---

## 2026-02-21 — License and Social Preview

Two housekeeping commits that added repository metadata without changing the guide content.

### Added

- **MIT with OpenAI/Anthropic Rider license** — custom license restricting use by OpenAI, Anthropic, and their affiliates without express written permission from Jeffrey Emanuel.
  [8f487c8](https://github.com/Dicklesworthstone/guide_to_openai_response_api_and_agents_sdk/commit/8f487c87c5ed8168318537b1ba1307134103748a)
- **GitHub social preview image** (`gh_og_share_image.png`, 1280x640) for consistent link previews when sharing the repository URL.
  [faa4405](https://github.com/Dicklesworthstone/guide_to_openai_response_api_and_agents_sdk/commit/faa4405fe110aff44c5a3a5e382e7661b33a5b4a)

---

## 2025-04-25 — Initial Publication

The full guide was published in a single commit (`de5e52e`), immediately following repo creation (`82032e2`). Together they constitute the initial release of the guide.

- [de5e52e — Update README.md](https://github.com/Dicklesworthstone/guide_to_openai_response_api_and_agents_sdk/commit/de5e52e4b65168e00d3e23caa90aa2ed62ce29b1) (3,910 lines added)
- [82032e2 — Initial commit](https://github.com/Dicklesworthstone/guide_to_openai_response_api_and_agents_sdk/commit/82032e21ce6fdeaab17900f39319184953b130e0) (empty README placeholder)

### Guide Content Overview

The README (~3,900 lines) is an exhaustive, self-contained reference covering OpenAI's March 2025 agentic-AI platform announcement. The content is organized into the following major areas:

#### Responses API (`/v1/responses`)

- Design philosophy: unification of Chat Completions simplicity with Assistants API tool-use power.
- Core request/response structure, item-based design, polymorphism improvements.
- State management via `previous_response_id` and `truncation` parameter.
- Streaming with Server-Sent Events (SSE).
- SDK helpers (`response.output_text`), data storage, and evaluation integration.
- Full parameter reference (model, input, instructions, tools, temperature, top_p, max_output_tokens, structured output via `text.format`, `store`, `metadata`, `truncation`).
- Implications for Chat Completions API and Assistants API migration path.

#### Built-in Tools

- **Web Search** (`web_search_preview`) — real-time internet access, inline citations, `user_location` context, search context size control, cost model (per-search pricing).
- **File Search** (`file_search`) — managed RAG over Vector Stores, chunking strategies, ranking options (`ranker`, `score_threshold`), result annotations with file citations, multi-store queries, attribute-based filtering.
- **Computer Use** (`computer_use_preview`) — UI automation via screenshots and structured actions (click, type, scroll, keypress, drag, etc.), safety model, `acknowledged_safety_checks`, environment requirements (sandboxed VM), current limitations (preview status).

#### OpenAI Agents SDK

- Core primitives: `Agent`, `Runner`, `Tool`, `Handoff`, `Guardrail`.
- Agent configuration: `name`, `instructions` (static or dynamic callable), `model`, `tools`, `handoffs`, `output_type` (structured output via Pydantic), `model_settings`.
- `@function_tool` decorator with automatic JSON Schema generation from type hints and docstrings.
- Hosted tool wrappers: `WebSearchTool`, `FileSearchTool`, `ComputerTool`.
- `Runner.run()` and `Runner.run_streamed()` execution methods with agentic loop mechanics.
- `RunResult` / `RunResultStreaming` with `final_output`, `to_input_list()`, `last_agent`, guardrail results.
- Streaming events: `RawResponsesStreamEvent`, `RunItemStreamEvent`, agent lifecycle events.
- Typed context (`Agent[TContext]`, `RunContextWrapper`) for dependency injection.
- Guardrails: `@input_guardrail` / `@output_guardrail` decorators, concurrent execution with LLM calls, `GuardrailFunctionOutput` with `tripwire_triggered`.
- Handoff mechanics: `handoff()` function, `Handoff` object, input/output filters, `on_handoff` callbacks.
- Model Context Protocol (MCP) integration via `MCPServerStdio`, `MCPServerStreamableHTTP`.
- Lifecycle hooks: `RunHooks` and `AgentHooks` with `on_start`, `on_end`, `on_handoff`, `on_tool_start`, `on_tool_end`.
- Tracing: automatic trace/span creation, `@trace`, `custom_span`, `set_tracing_disabled`, `set_trace_processors`, OpenAI dashboard integration.
- LiteLLM integration for non-OpenAI model providers.
- `draw_graph()` visualization utility.

#### Supporting Infrastructure

- **Vector Stores API** (`/v1/vector_stores`) — creation, chunking strategy (auto/static), expiration policies, file attachment and polling, direct search queries, batch operations.
- **Files API** (`/v1/files`) and **Uploads API** (`/v1/uploads`) — file upload for fine-tuning, assistants, and batch; multipart upload for large files; purpose-based organization.

#### Platform Management and Operations

- Organization/Project administration via Admin API — user management, invites, service accounts, API key lifecycle, audit logs.
- Fine-tuning API — supervised and preference (DPO) methods, hyperparameters, checkpoints, model permissions.
- Usage and cost monitoring APIs — Completions, Costs, and Audit Logs endpoints.
- Security and data handling — API key scoping, data retention policies, `store` parameter, zero-data-training default.

#### Peripheral and Realtime APIs

- Realtime API (`/v1/realtime`) for voice agents — WebSocket/WebRTC transport, audio transcription, VAD, session configuration.
- Audio API (TTS, STT), Images API (DALL-E generation/editing), Embeddings API, Moderations API.

#### Advanced Architectural Patterns

- **Deterministic agent flows** — sequential pipelines with dedicated per-step agents.
- **Handoffs and routing** — triage/dispatcher agents, language-based routing, escalation patterns.
- **Agents as tools** — controlled sub-processing via `agent.as_tool()`, orchestrator pattern.
- **LLM-as-a-Judge / self-correction loops** — iterative refinement with evaluator agents.
- Combining patterns for complex real-world workflows.

#### Developer Reference

- **Detailed Addendum: API Specifications and SDK Nuances** — granular parameter tables, object schemas, rate limit headers.
- **Trickiest Parts and Tips** — state management pitfalls, tool orchestration, Computer Use safety, debugging strategies, cost optimization, data preparation, API versioning considerations.
- **Detailed Examples Addendum** — runnable code samples (Python, JavaScript, cURL) for: basic text generation, image input, web search, file search, computer use, function tools, conversation state, streaming, structured output, reasoning, agent definition, handoffs, guardrails, dynamic instructions, lifecycle hooks, SDK streaming, LiteLLM usage, graph visualization, fine-tuning data formats, batch API formats, audio/image/embedding/moderation API calls, and admin API operations.

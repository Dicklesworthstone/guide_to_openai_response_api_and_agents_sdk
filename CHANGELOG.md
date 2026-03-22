# Changelog

All notable changes to **Guide to OpenAI Response API and Agents SDK** are documented here.

This repository is a single-document reference guide (not a versioned library), so the changelog tracks content milestones rather than semver releases. There are no tags or GitHub Releases as of 2026-03-21.

Repository: <https://github.com/Dicklesworthstone/guide_to_openai_response_api_and_agents_sdk>

---

## 2026-02-21 — Repository Metadata

Two housekeeping commits that added repository metadata without changing the guide content.

### License

- **MIT with OpenAI/Anthropic Rider** — custom license restricting use by OpenAI, Anthropic, and their affiliates without express written permission from Jeffrey Emanuel. Defines "Restricted Parties" broadly (officers, directors, employees, contractors, agents, consultants, service providers), covers derivative works, and includes automatic termination and equitable-relief clauses.
  [`8f487c8`](https://github.com/Dicklesworthstone/guide_to_openai_response_api_and_agents_sdk/commit/8f487c87c5ed8168318537b1ba1307134103748a)

### Social Preview

- **GitHub social preview image** (`gh_og_share_image.png`, 1280x640) for consistent link previews when sharing the repository URL.
  [`faa4405`](https://github.com/Dicklesworthstone/guide_to_openai_response_api_and_agents_sdk/commit/faa4405fe110aff44c5a3a5e382e7661b33a5b4a)

---

## 2025-04-25 — Initial Publication

The full guide was published in a single commit immediately following repo creation. Together the two commits constitute the initial release.

- [`de5e52e` — Update README.md](https://github.com/Dicklesworthstone/guide_to_openai_response_api_and_agents_sdk/commit/de5e52e4b65168e00d3e23caa90aa2ed62ce29b1) (3,910 lines added)
- [`82032e2` — Initial commit](https://github.com/Dicklesworthstone/guide_to_openai_response_api_and_agents_sdk/commit/82032e21ce6fdeaab17900f39319184953b130e0) (empty README placeholder)

### Guide Content Overview

The README (~3,900 lines of Markdown) is an exhaustive, self-contained reference covering OpenAI's March 11, 2025 agentic-AI platform announcement. Content is organized by capability area below.

---

#### Responses API (`/v1/responses`)

The foundational API positioned as the successor to both Chat Completions and Assistants.

- **Design philosophy** — unification of Chat Completions simplicity with Assistants API tool-use power; superset of Chat Completions with equivalent performance.
- **Core request/response structure** — item-based design, simplified polymorphism, unified `input`/`output` model.
- **State management** — `previous_response_id` for implicit multi-turn context; `truncation` parameter with `"auto"` strategy.
- **Streaming** — Server-Sent Events (SSE) with granular event types for low-latency UX.
- **SDK helpers** — `response.output_text` convenience accessor and similar ergonomic improvements.
- **Data storage and evaluation** — `store` parameter (default `true`) enabling 30-day retention for tracing and evals.
- **Full parameter reference** — `model`, `input`, `instructions`, `tools`, `temperature`, `top_p`, `max_output_tokens`, `text.format` (structured output), `store`, `metadata`, `truncation`, `stream`.
- **Migration guidance** — continued Chat Completions support; Assistants API feature-parity roadmap with mid-2026 deprecation target.

#### Built-in Tools

First-party capabilities callable directly within `client.responses.create`.

- **Web Search** (`web_search_preview`) — real-time internet access, inline citations with URL annotations, `user_location` context for geo-aware results, search context size control, per-search pricing model.
- **File Search** (`file_search`) — managed RAG over Vector Stores, configurable chunking strategies (auto/static with token size and overlap), ranking options (`ranker`, `score_threshold`), result annotations with file citations, multi-store queries, attribute-based metadata filtering.
- **Computer Use** (`computer_use_preview`) — UI automation via screenshot perception and structured actions (click, double_click, type, scroll, keypress, drag, wait, screenshot), safety model with `acknowledged_safety_checks`, sandboxed VM environment requirement, current limitations and preview status, CUA model benchmarks.

#### OpenAI Agents SDK

Open-source Python orchestration library (Node.js support planned), production-ready successor to the experimental "Swarm" SDK.

- **Core primitives** — `Agent`, `Runner`, `Tool`, `Handoff`, `Guardrail`.
- **Agent configuration** — `name`, `instructions` (static string or dynamic callable), `model`, `tools`, `handoffs`, `output_type` (structured output via Pydantic), `model_settings`.
- **Function tools** — `@function_tool` decorator with automatic JSON Schema generation from type hints and docstrings.
- **Hosted tool wrappers** — `WebSearchTool`, `FileSearchTool`, `ComputerTool` for using built-in tools within SDK agents.
- **Runner execution** — `Runner.run()` and `Runner.run_streamed()` with agentic loop mechanics (call model, handle tool calls, re-invoke).
- **Results** — `RunResult` / `RunResultStreaming` with `final_output`, `to_input_list()` for conversation continuation, `last_agent`, guardrail results.
- **Streaming events** — `RawResponsesStreamEvent`, `RunItemStreamEvent`, agent lifecycle events.
- **Typed context** — `Agent[TContext]` and `RunContextWrapper` for dependency injection across agent workflows.
- **Guardrails** — `@input_guardrail` / `@output_guardrail` decorators, concurrent execution with LLM calls, `GuardrailFunctionOutput` with `tripwire_triggered` for early termination.
- **Handoffs** — `handoff()` function and `Handoff` object, `input_filter` / `output_filter` for context control, `on_handoff` callbacks, LLM-driven delegation.
- **MCP integration** — `MCPServerStdio` and `MCPServerStreamableHTTP` for Model Context Protocol tool servers.
- **Lifecycle hooks** — `RunHooks` and `AgentHooks` with `on_start`, `on_end`, `on_handoff`, `on_tool_start`, `on_tool_end`.
- **Tracing** — automatic trace/span creation, `@trace` decorator, `custom_span`, `set_tracing_disabled`, `set_trace_processors`, OpenAI dashboard integration.
- **LiteLLM integration** — custom `ModelProvider` for non-OpenAI models.
- **Visualization** — `draw_graph()` utility for agent workflow diagrams.

#### Supporting Infrastructure

- **Vector Stores API** (`/v1/vector_stores`) — creation with chunking strategy and expiration policies, file attachment with polling, direct search queries, batch operations.
- **Files API** (`/v1/files`) — upload for fine-tuning, assistants, and batch; purpose-based organization.
- **Uploads API** (`/v1/uploads`) — multipart upload for large files.

#### Platform Management and Operations

- **Admin API** — organization and project administration, user management, invites, service accounts, API key lifecycle (creation, rotation, revocation), audit logs.
- **Fine-tuning API** — supervised and preference (DPO) methods, hyperparameter control, checkpoints, model permissions, JSONL training data formats.
- **Usage and cost monitoring** — Completions usage, Costs, and Audit Logs endpoints.
- **Security and data handling** — API key scoping (project-level), data retention policies, `store` parameter control, zero-data-training default policy.

#### Peripheral and Realtime APIs

- **Realtime API** (`/v1/realtime`) — voice agents via WebSocket/WebRTC transport, audio transcription, Voice Activity Detection (VAD), session configuration.
- **Audio API** — Text-to-Speech (TTS) and Speech-to-Text (STT).
- **Images API** — DALL-E generation and editing.
- **Embeddings API** — vector generation for semantic search.
- **Moderations API** — content safety classification.
- **Certificates API** (`/v1/organization/certificates`) — certificate management.

#### Advanced Architectural Patterns

Detailed design patterns for production agent systems.

- **Deterministic agent flows** — sequential pipelines with dedicated per-step agents for predictable behavior.
- **Handoffs and routing** — triage/dispatcher agents, language-based routing, escalation patterns.
- **Agents as tools** — controlled sub-processing via `agent.as_tool()`, orchestrator pattern for parallel information gathering.
- **LLM-as-a-Judge / self-correction loops** — iterative refinement with evaluator agents and quality thresholds.
- **Combining patterns** — composing the above for complex real-world workflows.

#### Feature Comparison

- **Responses API vs. Chat Completions API** — side-by-side feature matrix covering tool support, state management, streaming, structured output, and migration considerations.

#### Developer Reference: Detailed Addendum

Granular technical appendix covering:

- **API specifications** — full parameter tables, object schemas, rate limit headers for Responses API, built-in tools, and supporting APIs.
- **Trickiest parts and tips** — state management pitfalls, tool orchestration edge cases, Computer Use safety considerations, debugging strategies, cost optimization techniques, data preparation guidance, API/SDK versioning best practices.
- **Detailed examples addendum** — runnable code samples (Python, JavaScript, cURL) for: basic text generation, image input (multimodal), web search, file search, computer use, custom function tools, conversation state management, SSE streaming, structured output (JSON Schema), reasoning, agent definition and run, handoffs, guardrails, dynamic instructions, lifecycle hooks, SDK streaming, LiteLLM usage, graph visualization, fine-tuning data formats, Batch API formats, audio/image/embedding/moderation API calls, and admin API operations.

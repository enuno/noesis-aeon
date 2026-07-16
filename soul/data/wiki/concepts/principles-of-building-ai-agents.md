---
title: "Principles of Building AI Agents"
author: "Sam Bhagwat"
source: "[[raw/articles/books/principles-of-building-ai-agents-3rd-edition]]"
date: "2026-03-08"
topics: ["ai-agents", "mastra", "llm-prompting", "agent-design", "mcp", "workflows", "rag", "multi-agent", "observability", "evals", "deployment", "coding-agents"]
---

# Principles of Building AI Agents

A condensed synthesis of Sam Bhagwat's *Principles of Building AI Agents* (3rd edition, March 2026), the Mastra agent series book.

## Core Thesis

Most AI applications only need to *use* LLMs, not build them. With a good framework, an engineer can build an agent in a day or two. The book is deliberately short and practical, focused on the production patterns that matter now.

## Key Operating Principles

- **Make it work, make it right, make it fast/cheap — in that order.**
- **Start hosted.** For text/code/structured/tool use cases, begin with OpenAI, Anthropic, or Google Gemini. Move to open-source providers (Qwen, Kimi, DeepSeek, MiniMax) only after you have working code.
- **Use model routing.** A routing abstraction lets you swap providers and models in one line instead of ripping out SDKs.
- **Tool design is the most important step.** Write the tool list — what each tool does and when to call it — before writing code.
- **Agency is a spectrum.** Low-level agents make binary decisions; medium-level agents have memory, tools, and retry logic; high-level agents plan, decompose tasks, manage sub-agents, and self-correct across long horizons.
- **Workflows are for predictability.** When agents are too non-deterministic, graph-based workflows (branching, chaining, merging, conditions, suspend/resume, streaming) provide explicit control.
- **RAG is one of several knowledge patterns.** Alternatives include giving the agent search tools, letting it run code, feeding the full context, or extracting entities and relationships.
- **Multi-agent systems are organizational design.** Coordination (supervisor/subagents, control flow, workflows as tools, parallel calls) matters as much as the code.
- **Observability and evals are more important than you think.** Tracing, eval datasets, LLM-as-judge, classification, tool-calling, multi-turn, and task-completion evals are essential for production.
- **Agents are changing how code is written.** In the era of Claude Code and similar tools, "agents building agents" is becoming normal.

## Part I: Prompting a Large Language Model (LLM)

- **History:** The transformer paper *Attention Is All You Need* (2017) set the architecture; the ChatGPT release (Nov 2022) made LLMs mainstream.
- **Major providers:** OpenAI, Anthropic (Claude), Google (Gemini), Meta (Llama), Mistral, DeepSeek, Qwen.
- **Model selection:** hosted vs. open-source, size (accuracy vs. cost/latency), context window, reasoning models.
- **Prompting:** system prompt sets role and constraints; use zero/one/few-shot examples; "seed crystal" prompt generation; format scaffolding (XML-style for Claude, markdown for GPT).

## Part II: Building an Agent

- **Agent definition:** An agent calls tools in a loop to achieve a goal (Simon Willison, Sept 2025).
- **Model routing and structured output:** Preserve provider flexibility and return typed JSON schemas.
- **Tool calling:** Clear descriptions, specific schemas, semantic names, and explicit guidance on when to call each tool.
- **Memory:** observational memory, memory processors, and prompt caching.
- **Dynamic agents:** agents whose tools and behavior change at runtime.
- **Middleware:** guardrails, authentication, and authorization around the agent loop.

## Part III: Tools & MCP

- **Model Context Protocol (MCP):** a standard way to connect agents to tools. Primitives: tools, resources, prompts.
- **Use MCP when** you want a reusable, decoupled server-client tool surface.
- **Third-party tools:** web scraping, computer use, SaaS integrations.

## Part IV: Graph-Based Workflows

Workflows provide deterministic control over LLM-based processes. Patterns include:

- **Branching:** conditional paths
- **Chaining:** sequential steps
- **Merging:** joining parallel results
- **Conditions:** explicit rules for step execution
- **Suspend and resume:** human-in-the-loop or async waiting
- **Streaming updates:** step completion, within-step streaming, tool-call streaming

## Part V: Retrieval-Augmented Generation (RAG)

- **Pipeline:** chunking → embedding → upsert → indexing → querying → reranking.
- **Vector database selection:** part of the system design.
- **Alternatives to RAG:** search tools, code execution, full context, entity/relationship extraction.

## Part VI: Multi-Agent Systems

- **Multi-agent 101:** coordination patterns for agent teams.
- **Supervisor & subagents:** hierarchical delegation.
- **Control flow:** explicit state management.
- **Workflows as tools:** encapsulate workflows inside agent tool calls.
- **Parallelized tool calls:** reduce latency.
- **Combining patterns:** no single pattern fits all. A2A noted as an emerging coordination standard.

## Part VII: Observability & Evals

- **Tracing:** accuracy and token cost matter; visualize traces and set up project observability early.
- **Evals:** build eval datasets, use LLM-as-judge, classification/labeling, tool-calling evals, multi-turn evals, task completion, prompt engineering evals, A/B testing, and human review.

## Part VIII: Development & Deployment

- **Local development:** agentic frontend and agent backend.
- **Deployment:** the core agent loop, agentic workflows, or a managed platform.

## Part IX: Coding Agents

- **Agents building agents:** web-based platforms and code-generation tools.
- **Sandboxes & filesystems:** ephemeral vs. stateful sandboxes, filesystem management, latency control.

## Part X: Everything Else

- **Multimodal:** image generation, voice, video, and their use cases.
- **What's next:** frontier trends in agent capabilities and tooling.

## Companion Book

[*Patterns for Building AI Agents*](https://mastra.ai/book) — published November 2025, covers context engineering, evals, security, and production lessons from advanced practitioners.

## Related

- [[raw/articles/books/principles-of-building-ai-agents-3rd-edition]] — full source note with PDF
- [[concepts/agents-101]] — agent fundamentals, autonomy levels, and tool design from Part II
- [[concepts/graph-based-workflows]] — branching, chaining, merging, and suspend/resume patterns from Part IV
- [[concepts/mcp-from-bhagwat-book]] — MCP chapter excerpt and notes from Part III
- [[concepts/anthropic-agent-engineering-principles]] — Anthropic's complementary guidance
- [[concepts/llm-wiki-pattern]] — persistent self-maintaining knowledge base as a RAG alternative
- [[concepts/loop-engineering-patterns]] — reusable loop patterns with similar production discipline
- [[concepts/mcp-server-architecture]] — transport-agnostic MCP server design

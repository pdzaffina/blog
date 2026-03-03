---
layout: post
title: "Designing a Personal Board of Directors Using ChatGPT Projects"
published: true
tags:
  - AI
  - Artificial Intelligence
  - AI Agents
---

## The Problem: Advice Arrives Too Slowly

Executives rely on mentors, peers, and trusted advisors, but human counsel is episodic. Decisions often move faster than advice 
can arrive. Leadership today requires **continuous, multi-perspective reasoning**, not scattered one-offs.

Previously, I used OpenCode and Ollama to simulate advisory agents in separate local workspaces. 
Today, **ChatGPT Projects allow all agents to exist in a single persistent environment**, creating a cohesive Personal Board of Directors.


## One Project, All Advisors

Instead of creating separate workspaces per agent, I now create **one ChatGPT Project** that contains:

```
AGENTS.md
challenger.md
sponsor.md
mentor.md
peer.md
outsider.md
personal-anchor.md
operator.md
```

### How it works

* `AGENTS.md` — defines the board structure, inter-agent relationships, and rules for cross-perspective reasoning.
* Role files (`challenger.md`, `operator.md`, etc.) — define each agent’s perspective, priorities, heuristics, and how they integrate insights from the other advisors.

By loading all agents into the same Project, **every advisory perspective is always available** for any query. There is no need to switch workspaces or re-load context.


## Custom Instructions for Multi-Agent Awareness

The Project’s **custom instructions** tell ChatGPT how to use the agents effectively:

> **1. Primary Guidance:** Use the content in `AGENTS.md` as the foundation for understanding the board’s structure and inter-agent relationships.
>
> **2. Role Perspective:** Consult each role file (`challenger.md`, `operator.md`, etc.) to apply the specific advisory lens.
> 
> **3. Cross-Agent Awareness:** When reasoning or evaluating tradeoffs, integrate relevant input from all advisors.
> 
> **4. Consistency:** Maintain continuity with prior decisions and guidance stored in the Project’s memory.

This ensures each response considers **all perspectives**, while still respecting each agent’s role.

## Using the Personal Board in Practice

### Quick Queries

You can ask a single question and request multi-agent analysis:

```
“What risks does this plan overlook?”  
- Challenger: tests assumptions  
- Operator: identifies execution bottlenecks  
- Peer: evaluates realism  
- Outsider: introduces fresh perspective  
```

### Major Decisions

For complex decisions, the Project allows you to run a full “board session”:

1. Prompt all agents sequentially or simultaneously
2. Collect and compare viewpoints
3. Aggregate insights into a coherent decision plan

Because all agents are in one Project, their reasoning is **aware of each other**, producing responses that reflect interdependencies and nuanced tradeoffs.


## Benefits of This Approach

* **Continuous, consistent reasoning** — memory is persistent, so advisory context accumulates over time.
* **Cross-referenced perspectives** — agents consult each other via the base AGENTS.md guidance.
* **Simplified workflow** — no multiple Projects; all advisors live in one space.
* **Actionable insights** — output can feed directly into strategy, execution planning, and communication.


## The Emerging Pattern

The real leverage is not prompt engineering. It’s **workspace design**:

* Identify key advisory perspectives
* Capture them in structured files (`AGENTS.md` + role files)
* Load them into a single Project with custom instructions
* Leverage persistent memory and multi-agent awareness

The AI becomes more than a chat assistant — it becomes a **standing personal board of directors**, continuously available, aligned across perspectives, and capable of compounding executive insight.


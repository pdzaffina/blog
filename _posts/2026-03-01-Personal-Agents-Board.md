---
layout: post
title: "Your Personal Board of Directors as AI Agents for Budget Planning"
published: true
tags:
  - AI
  - Artificial Intelligence
  - AI Agents
  - OpenCode
---
Most leaders know the value of a mentor, but one person cannot cover every perspective you need. A **personal board of directors** fixes that by assembling a small, intentional group of 5 to 7 people who advise, challenge, and support your growth. Each seat has a distinct role, providing a combination of challenge, sponsorship, guidance, and grounding.  

Here are the core roles you might fill:

- **The Challenger** pushes back on your thinking, identifies blind spots, and stress-tests your ideas.  
- **The Sponsor** has influence in your field and advocates for your advancement.  
- **The Mentor in your field** is a few steps ahead on your career path and helps you avoid mistakes they made.  
- **The Peer** is at a similar level and offers real-time reality checks.  
- **The Outsider** comes from a different industry or background and provides fresh perspective.  
- **The Personal Anchor** knows you deeply and keeps you aligned with your values.  
- **The Operator** excels at execution and systems, translating vision into action.  

Relationships should feel reciprocal. Even informal connections work better when both parties benefit from engagement. Diversity of perspective is critical. Avoid filling the board with people too similar to yourself.  

---

## Converting the Board to AI Agents

OpenCode is a perfect tool to bring your personal board into the digital space. Each persona maps directly to a custom OpenCode agent. Agents are markdown files with YAML frontmatter, stored in `~/.config/opencode/agents/` for global access or `.opencode/agents/` for project-specific use.  

Each agent file includes:

- **Description** to appear in the TUI  
- **Mode** defining how you interact with it  
- **Temperature** controlling creativity versus focus  
- **How to Prompt** blocks, sample questions, and traits  

This lets you drop any persona into a session instantly and get advice as if the board member were in the room.  

---

## Installation

### Global Setup

```bash
cp .opencode/agents/*.md ~/.config/opencode/agents/
cp .opencode/commands/*.md ~/.config/opencode/commands/
cat AGENTS.md >> ~/.config/opencode/AGENTS.md
````

### Project-Specific Setup

```bash
cp -r .opencode/ /path/to/project/
cp AGENTS.md /path/to/project/
```

---

## Using Your AI Board

### Switch to a Single Agent

```bash
@challenger what are the risks of this approach?
@operator break down the Q3 execution plan
@outsider how would someone outside this industry approach this problem
```

You can cycle through agents using `Tab` or use the TUI to switch focus.

### Convene the Full Board

```bash
/board Should I approve these budget initiatives?
/pre-decision Accepting a VP role at a new company
/stuck My team is struggling to deliver on deadlines
```

### CLI Mode

```bash
opencode run --agent operator "Build a phased Q3 budget plan"
opencode run --agent peer "Do these priorities make sense?"
```

---

## Board File Structure

```
.
├── AGENTS.md
└── .opencode/
    ├── agents/
    │   ├── challenger.md
    │   ├── sponsor.md
    │   ├── mentor.md
    │   ├── peer.md
    │   ├── outsider.md
    │   ├── personal-anchor.md
    │   └── operator.md
    └── commands/
        ├── board.md
        ├── pre-decision.md
        └── stuck.md
```

Each agent file has YAML frontmatter like this:

```yaml
---
description: The Challenger stresses ideas to reveal blind spots
mode: primary
temperature: 0.4
---
```

You can override the model for each agent, for example using a faster or cheaper open-weight LLM for execution tasks.

---

## Using the Board in a Budget Scenario

Imagine it is budget season. You have rough initiative ideas, headcount estimates, and strategic priorities. Here's how the board comes into play:

1. **Gather Raw Inputs**
   Capture your initiatives, cost estimates, and goals into a plain text file. OpenCode will structure them for AI review.

2. **Write Initiative Briefs**
   Use the Mentor, Peer, and Operator agents to draft structured initiative briefs. The Challenger reviews assumptions, and the Outsider suggests alternative perspectives.

3. **Build the Consolidated Budget Model**
   Operator consolidates headcount, tooling costs, and total spend. The board ensures priorities align with strategy.

4. **Prioritization and Trade-Off Analysis**
   Challenger and Outsider stress-test assumptions. Personal Anchor keeps focus on organizational values. Operator calculates scenarios for constrained budgets.

5. **Executive Pitch**
   Sponsor reviews the final summary for clarity and advocacy. Peer validates the tone. Operator ensures the document is actionable.

6. **Iterate**
   Adjust inputs and rerun sessions with `/board` to reflect updated financials or executive feedback.

By mapping real-world advisory roles into AI agents, you get continuous, structured input on complex decisions. The board is always accessible, consistent, and grounded in the context you provide.

---

## Tips for Success

* **Provide real context** to get actionable insights.
* **Use individual agents** for quick questions and `/board` for major decisions.
* **Pair Challenger and Operator** for the most effective planning workflow.
* **Update AGENTS.md** with your goals, priorities, and personal context to keep sessions aligned with reality.

With this setup, your personal board becomes a live, interactive partner for planning, decision-making, and navigating complex challenges.

---

*Resources: [OpenCode](https://opencode.ai) · [AGENTS.md example](https://github.com/sst/opencode)*

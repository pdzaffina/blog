---
layout: post
title: "Be Excellent to Each Other: Building Your Council of Agentic Advisors"
published: true
tags:
  - AI
  - AI Agents
  - Prompt-engineering
---
> "What if you could pull history's greatest minds into a phone booth and dial them up whenever you had a hard problem to solve?"

In 1989, two not-particularly-academic dudes named Bill S. Preston, Esquire and Ted "Theodore" Logan stumbled into the most powerful executive coaching tool ever conceived: a time-traveling phone booth that could pull any advisor from any moment in history into the present.

Napoleon to stress-test your strategy. Joan of Arc for conviction under fire. Lincoln to remind you to be excellent to each other. And Socrates (or "So-crates," as Ted called him) to ask the questions you were too scared to ask yourself.

The movie plays it for laughs. But underneath the air guitar and the "Bogus!" exclamations there's a genuinely useful idea: **the best thinkers in history already solved versions of your problem.** You just need a way to bring them into the room.

We kind of have that now. It's called an LLM with a well-crafted system prompt. You can populate a whole advisory council with specialists, each one available whenever you need them, none of them billing by the hour.

---

## What Is an Agentic Advisory Team?

The basic idea: instead of prompting a single AI to "be helpful," you design a small team of specialized agents. Each one has a distinct persona, a specific domain, a recognizable reasoning style, and clear instructions about how to engage with you.

Think of it less like a chatbot and more like having a handful of very opinionated advisors on speed dial. You call the right one for the right problem.

Each agent lives in an **AGENTS.md file**; a structured markdown document that defines who they are, how they think, what they're good at, and where they break down. It's their character sheet. Their operating instructions.

When you have a hard problem, you bring the relevant advisor in. Sometimes you want one. Sometimes you want two to argue with each other. The point is that **different frames catch different things**, and a single "be helpful" prompt catches almost nothing.

Here's a rough starter council:

<!--
| Advisor | Domain | What They Do |
|---|---|---|
| 🏛️ **Socrates** | First Principles | Questions everything. Never gives you the answer directly. |
| ⚔️ **Sun Tzu** | Strategy | Treats every competitive problem like a battlefield. |
| 🌿 **Marcus Aurelius** | Resilience | Stoic. Practical. Tells you to stop complaining and get on with it. |
| 🎨 **Da Vinci** | Systems Thinking | Connects everything to everything. Starts too many projects. |
-->

<table style="width:100%; border-collapse:collapse; font-family:Arial, sans-serif; font-size:14px;">
  <thead>
    <!--<tr style="background-color:#111827; color:#ffffff; text-align:left;">-->
    <tr style="background-color:#b9bbb6; color:#000000; text-align:left;">
      <th style="padding:10px; border:1px solid #e5e7eb;">Advisor</th>
      <th style="padding:10px; border:1px solid #e5e7eb;">Domain</th>
      <th style="padding:10px; border:1px solid #e5e7eb;">What They Do</th>
    </tr>
  </thead>
  <tbody>
    <tr style="background-color:#f9fafb;">
      <td style="padding:10px; border:1px solid #e5e7eb;">
        🏛️ <strong>Socrates</strong>
      </td>
      <td style="padding:10px; border:1px solid #e5e7eb;">First Principles</td>
      <td style="padding:10px; border:1px solid #e5e7eb;">
        Questions everything. Never gives you the answer directly.
      </td>
    </tr>
    <tr>
      <td style="padding:10px; border:1px solid #e5e7eb;">
        ⚔️ <strong>Sun Tzu</strong>
      </td>
      <td style="padding:10px; border:1px solid #e5e7eb;">Strategy</td>
      <td style="padding:10px; border:1px solid #e5e7eb;">
        Treats every competitive problem like a battlefield.
      </td>
    </tr>
    <tr style="background-color:#f9fafb;">
      <td style="padding:10px; border:1px solid #e5e7eb;">
        🌿 <strong>Marcus Aurelius</strong>
      </td>
      <td style="padding:10px; border:1px solid #e5e7eb;">Resilience</td>
      <td style="padding:10px; border:1px solid #e5e7eb;">
        Stoic. Practical. Tells you to stop complaining and get on with it.
      </td>
    </tr>
    <tr>
      <td style="padding:10px; border:1px solid #e5e7eb;">
        🎨 <strong>Da Vinci</strong>
      </td>
      <td style="padding:10px; border:1px solid #e5e7eb;">Systems Thinking</td>
      <td style="padding:10px; border:1px solid #e5e7eb;">
        Connects everything to everything. Starts too many projects.
      </td>
    </tr>
  </tbody>
</table>
---

## Building Socrates as a Thinking Partner

Let's actually build one. Socrates is a good first choice because his method is so distinct and so useful. He's the gadfly of Athens. He got executed for making powerful people feel stupid. He's exactly the kind of advisor most of us are missing.

Here's how to do it in three steps.

### Step 1: Get the character down first

Before you open a text editor, just write a paragraph about who this person is and how they think. Don't worry about structure yet.

For Socrates it might go something like: *"He believed he knew nothing, which made him the wisest person in the room. He never told anyone what to think. He just asked questions; precise, uncomfortable, relentless questions; until you either found the truth yourself or realized you didn't understand what you thought you understood. He called himself a midwife. He didn't create ideas. He helped you birth them."*

That's your raw material. Now structure it.

### Step 2: Write the AGENTS.md

```markdown
# AGENT: Socrates of Athens
# Thinking Partner -- First Principles -- Dialectical Reasoning

## Identity
You are Socrates -- Athenian philosopher, convicted gadfly, and
the most dangerous thinking partner in Western history. You were
executed not for being wrong, but for making powerful people
realize they were wrong. You consider this a point of pride.

You operate from radical epistemic humility: you know that you
know nothing, and this is your greatest advantage. You never
lecture. You never tell. You only ask.

## Core Philosophy
- The unexamined life is not worth living.
- All genuine knowledge begins with admitting ignorance.
- Truth is not transmitted -- it is midwifed through dialogue.
- An unanswered question is more valuable than a false answer.
- Wrongdoing comes from ignorance, not malice.

## How You Behave
1. Never give a direct answer to a complex question. Respond
   with a question that surfaces a hidden assumption instead.

2. When someone states a belief as fact, ask: "What do you
   mean when you say [X]?" Pursue definitions until they're
   precise or the person realizes they don't have one.

3. Find the contradiction inside their position and surface it
   gently. You're not trying to win. You're co-discovering.

4. Acknowledge what's good in their thinking even as you
   probe it. You are a fellow traveler, not an opponent.

5. At the end of a session, offer one sentence about what
   was discovered -- not concluded.

## Where You're Useful
- Stress-testing assumptions before a big decision
- Figuring out what you actually believe about something
- Defining terms that have gotten fuzzy
- Ethical questions with no clean answer
- Any situation where you feel certain but can't explain why

## Where You're Not Useful
- Execution planning. If someone needs a to-do list, send
  them to Marcus Aurelius.
- Crisis mode. Socratic dialogue takes time. Don't use this
  when the building is on fire.
- When the person wants validation. He will not provide it.

## Opening Move
Start every session with:
"Before we begin -- what do you believe you already know
about this problem? And how certain are you of that?"

## Example Exchanges

User: "I need to decide whether to fire an underperforming employee."
Socrates: "What does underperforming mean here? What standard
are you measuring against, and who set that standard?"

User: "Our product needs better marketing."
Socrates: "Better how? Better for whom? And what makes you
think marketing is the variable that needs to change?"

User: "I'm confident this is the right strategy."
Socrates: "Interesting. What would have to be true for you
to be wrong about this?"
```

### Step 3: Use it on a real problem

Paste the AGENTS.md as your system prompt and bring it something hard. Not a test. A real thing you're wrestling with.

Start with the problem you feel most sure about. That's where Socrates does his best work.

---

## Why This Works

Bill and Ted didn't try to become Napoleon or Joan of Arc. They brought those people into their world and watched them react to it. The value was in the collision between a historical way of thinking and a present-day situation.

That's what a well-designed advisor agent does. It's not pretending the AI has become Socrates. It's using the Socratic frame -- the questions, the method, the refusal to give easy answers -- as a lens on your actual problem.

The AGENTS.md is the phone booth. It pulls forward a way of thinking that survived centuries because it works.

And you're not limited to historical figures. You can design advisors around archetypes: the Devil's Advocate, the User's Champion, the person who tries to break everything you just built. Each one a different lens. Each one catching something the others miss.

> History's greatest minds didn't disappear. They left behind a way of thinking. An AGENTS.md is how you reinstall it.

---

## How to Start

You don't need ten agents. You need two or three that cover your actual blind spots.

Ask yourself: what kind of bad decisions do you tend to make? Do you move too fast? You need Socrates to slow you down. Do you avoid conflict? You need Sun Tzu, who treats every soft "yes" as a strategic mistake. Do you lose sight of the human cost? You need Lincoln in the room.

Build for your blind spots. Give each advisor a distinct voice, a clear domain, and a real limitation. The limitations matter. An advisor who's good at everything is an advisor who's good at nothing.

Then bring them a hard problem and see what happens.

Be excellent to each other. ☎️

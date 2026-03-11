---
layout: prompt
category: Skills
title: AI Boardroom Claude Code Skills Prompt
published: true
credit: Allie K Miller (https://x.com/alliekmiller)
---
Create a Claude Code slash command at ~/.claude/commands/boardroom.md that does the following:

I want to specify [NUMBER] advisors aka real people whose strategic thinking I admire. Some folks I'd like you to start with are <name of first board member> and <name of second board member>. 

For each advisor, include:
- Their name
- A 2-3 sentence personality profile describing how they think, what they prioritize, and what biases they bring (you will find this online)

Prompt me for deep cut information on my business and types of decisions so we can select the right board of advisors (ie experts in my field, adjacent experts, naysayers, radical thinkers, impact-driven leaders, etc).

When I invoke /boardroom [my question], it should:

ROUND 1 (parallel):
- Spin up [NUMBER] agents as a team, one per advisor
- Each agent reads a business context document* I provide (a markdown file describing my business, revenue, team, products, goals, and positioning) 
- Each writes 800-1200 words arguing their position on my question (or as many words as needed - more or less - to convey 95% of their point)
- Each includes a YES/NO/CONDITIONAL vote, specific numbers, and projections on cost, revenue, impact, and team joy

ROUND 2 (parallel):
- Collect all Round 1 positions
- Send every advisor ALL the other positions
- Each writes a 400-800 word rebuttal that includes:
  - Who they disagree with most and WHY (referencing their actual argument)
  - Whether anyone changed their mind
  - Their FINAL vote (which can differ from Round 1)

DELIVERABLES:
- Create a folder named after the decision and save it <file path>
- Markdown file: vote tracker (Round 1 vs Final), consensus, key tensions, arguments, rebuttals, relevant decision framework 
- HTML file: branded, interactive sliders for key assumptions (price, participants, conversion rate, hours committed, complexity) that dynamically recalculate impact projections. Show vote changes visually. Styled cards for each advisor.
- PDF file: print-optimized version for sharing with team
Present back to me a synthesis: final votes, who changed their mind, biggest fights, sharpest insight, and likely decision.


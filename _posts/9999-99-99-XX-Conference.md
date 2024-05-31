---
layout: post
title: "Some Conference 2024: Day 1 Notes"
published: false
---


Last Updated: May 29, 2024
I’m in Vancouver this week at PGConf.dev, a conference is aimed at people who are either hacking on Postgres source code, or building extensions, or growing the community. I don’t really fit into any of those categories, but I’m here because I wanted to observe how Postgres is built.

Here were the sessions I attended on day 1, and what I took away from each of ’em. The hyperlinks to each session title has the presentation material if the presenter uploaded it.



WELCOME SESSION BY JONATHAN KATZ AND MELANIE PLAGEMAN

The overall PGConf.dev conference was explained as:
* Presentations about things the attendees want to build in the next year
* Meeting other people who want to build the same thing
* On Friday, having in-person unconference sessions to help brainstorm & plan work for the next year
* 
I love this concept, although lemme be clear that I’m not a developer, nor am I here to try to sway development in any way. I’m here out of professional curiosity, and I’m writing about my experiences here because I bet some of y’all are curious about how Postgres gets built too.

INTRO TO HACKING ON POSTGRES BY TOMAS VONDRA
This session explained the development process & workflows for Postgres. I love that this was arranged first in the agenda given that it’s necessary to onboard developers into the ecosystem.



Tomas explained that the ~30 committers (people who have permission to actually push code) come to PGConf.dev to meet hackers and network with them. Attendees shouldn’t be afraid to talk to a committer at the conference.

Annual releases come out in September, with a feature freeze in April. Along the way, Postgres runs commitfests: one month of work, one month off. You can see the current & future commitfests online. If you’re looking for a place to start, like a patch that would be useful for your workloads, search through the patches for the next commitfest, and help with reviewing those patches. Why? Because There’s an expectation that if you’re going to contribute patches, you should also be reviewing the patches of others.

After picking a patch to test, Tomas covered how to download the Postgres source code and compile it from scratch on your laptop with the right debugging configuration to make testing easier. He introduced the repo’s regression tests, isolation level tests, and the more advanced check-world multi-server tests (like replication testing.)

I only sat in the first 70 minutes of this session because after that, the next part was much more technically detailed, and it was going to soar over my head. This first hour was the perfect intro for me to remember how hard it is to do open source development. I switched over to the “regular” sessions, in which speakers talk about big-picture things that could be done in future versions of Postgres, and what work would be entailed.

SAVING SPACE IN VARIOUS SUBSYSTEMS BY MATTHIAS VAN DE MEENT
Matthias’s focus is reducing storage required when working with millions of databases. (Makes sense, given that his employer is Neon, a company that hosts serverless Postgres databases and has a free 0.5GB database tier.)



Matthias started by discussing more appropriate sizes for system catalogs, then moved on to more interesting scenarios with user tables such as logical column order to keep bits together, compressing page-level data, and the fixed 24 byte overhead per WAL record.

The session covered one of the big problems with using relational databases to store JSON data. If you update a tiny part of the JSON, Postgres copies the whole new JSON (not the tiny changed part) to the write-ahead log, plus builds a new copy of the TOAST.

I liked the interactivity in the session: some of the attendees piped right up during the presentation, talking about which space savings would be easier or harder to achieve.

ADAPTIVE QUERY OPTIMIZATION BY ALENA RYBAKINA
This session was about how the AQO extension gives the query planner memory to remember how selective various query parameters were, and then reusing that memory to predict cardinality of similar future incoming queries.



It’s like Microsoft SQL Server’s Query Store in the sense that it stores all known queries, their hashes, query texts, their query plans, and the selectivity and number of rows returned from each node.

However, it’s even more ambitious than Microsoft since it feeds details back into the query planner to correct plan issues based on the actual number of rows that came out of plan nodes. (Later at the conference, I happened to overhear the aqo developers discussing with various people about how to identify similar queries in an effort to improve their estimates as well – that’s pretty ambitious.)

I loved the test methodology that involved very complex join conditions from this IMDB data set. Those queries look horrific.

The audience immediately asked the right question that caused the most problem with SQL Server’s implementation: how do you intelligently cap how much data is kept around for learning and planning? (Just for reference: SQL Server’s implementation uses space in the user database, whereas this project just uses RAM.)

HOW POSTGRES IS MISUSED AND ABUSED BY KAREN JEX

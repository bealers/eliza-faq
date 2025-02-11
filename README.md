# Eliza FAQ mini sprint

Comms from Jin (via X DMs):
- plan is [this discord bot](https://needle.gg) for dedicated "ask AI" channel to keep channel list clean. Every question can spawn a new thread.
- look at FAQ [in this section](https://hackmd.io/@XR/elizaos-rpgf/)*, need to consolidate the questions / answers first, made a new branch but think they're moving docs to a new repo so gunna spin that up today
- I think good goal / hackathon project is making an Eliza loaded with this data


## Deliverable

Make a FAQ system for [ElizaOS](https://elizaos.github.io/eliza/) loaded with FAQ data from its own Discord.

## What does this entail?
- research ElizaOS option vs. Discord bot
    - How does Agent Scarlett work?
- analyse and consolodate the faq data in `src/` as a starting point
- agree output format best for RAG (use Eliza tools)
- convert to that format
- manually check each one

## Questions 
- how does agent learn? if new answers are presented to it?
- ideally we want a 'solved by' tag for each question tagged to a human

## Out of scope
- Write how tos based on popularity of questions
# FAQ January

[toc]

## Questions Answers

# Discord Q&A Summary - 💻-coders 2025-01-25

## Q1: hi guys, im trying to have multiple characteres running, how does secrets works ? shoulh I copy paste .env config that are customized for each character ? like TWITTER_USERNAME=xxxxx TWITTER_PASSWORD=xxxx etc. ?
**Asked by:** Pouncer

**Answer:** i haven't tried to run multiple agent in one command but what will i do , for quick test , just create a project for each agent then with that you can change all the settings for each agent project and you can both run it, in a separate terminal, because in cloud its the samething you will create a docker image one for each agent, but maybe there's a better way , i will search if there's a way to run multiple agent in one project and if that is possible
**Answered by:** [ai16z] <odilitime>

**Context:** Pouncer is asking about running multiple characters and how secrets work.

---

## Q2: my question is more about the "secrets" function than on the multi-agent running in parallel
**Asked by:** Pouncer

**Answer:** [elizaos] <warfreakzplays> if you check the defaultCharacter.ts  class you will see that there's secrets variable object there , so maybe you can look at that 1st, i haven't explore it my self but that's where you can start
**Answered by:** elizaos-bridge-odi

**Context:** Pouncer clarifies the focus on the "secrets" function.

---

## Q3: Is there zoom plugin
**Asked by:** dragonlord

**Answer:** No, there is no zoom plugin available.
**Answered by:** Not specified

---

## Q4: What is cabal and how to use it ?
**Asked by:** K2nans

**Answer:** i think its more reasonable to use a { } inside the characterfile, so every agent can have unique goals and actions... working on a tutorial for it, but it will take some days though
**Answered by:** D. Ratta

---

## Q5: Why the twitter client not working as expected
**Asked by:** shvedity

**Answer:** The Twitter login is failing due to incorrect login attempts. It seems to be retrying multiple times but ultimately fails. You may need to address the login issue directly with Twitter or check your login credentials.
**Answered by:** Not specified

**Context:** The user provided a detailed error log showing login attempts and failures.

---

## Q6: what can i do about this?
**Asked by:** shvedity

**Answer:** You may need to verify your Twitter login credentials and ensure they are correct. If the issue persists, consider reaching out to Twitter support for further assistance.
**Answered by:** Not specified

**Context:** The user expressed appreciation for any help provided.

---

## Q7: How to interact with aixvc agent please and cabal chat ? Or access marcs trusted leaderboard ? Please some kind explanations ?
**Asked by:** K2nans

**Answer:** don't know
**Answered by:** D. Ratta

**Context:** Technical question about interacting with aixvc agent and cabal chat, or accessing a trusted leaderboard.

---

## Q8: Is my penis enought big for you little suckers ?
**Asked by:** K2nans

**Answer:** No substantive answer provided.
**Answered by:** 

---

## Q9: Currently having an issue when attempting to interact with my agent. Worked before perfectly, came back and ran the client again, and it just keeps defaulting to the Eliza character. I only have my character file, any idea on what it could be?
**Asked by:** dxganta

**Answer:** delete the .sqlite file in agent/data folder
**Answered by:** ai16z <odilitime>

---

## Q10: idk why I'm getting this error, was working fine earlier, added a new action to solana plugin, reran pnpm install and rebuilt, next I tried running my agent, and voila ... this
**Asked by:** PsyxhCLONE

**Answer:** No substantive answer provided.
**Answered by:** 

---

## Q11: anyidea why I'm getting this I'm on develop branch and just inserted the apis and started trump character to test and I'm getting this
**Asked by:** Abderahman

**Answer:** No substantive answer provided.
**Answered by:** 

---

## Q12: I also get the @discordjs/opus install error.  Windows pc and I’ve tried several installations.
**Asked by:** [ai16z] <odilitime>

**Answer:** No substantive answer provided.
**Answered by:** 

---

## Q13: There is no way to use Eliza or agent-twitter-client with keys or access tokens?
**Asked by:** RL

**Answer:** You can use Eliza or agent-twitter-client with keys or access tokens. Make sure to properly configure the keys and access tokens in your environment variables.
**Answered by:** RL

**Context:** RL is questioning the usage of keys and access tokens with Eliza or agent-twitter-client.

---

## Q14: Best place to deploy an instance of eliza?
**Asked by:** miladyboy

**Answer:** render is a very easy way to deploy a docker. You can check out https://render.com/
**Answered by:** avirtualfuture

**Context:** miladyboy is seeking advice on deploying an instance of Eliza.

---

## Q15: Could anyone fix the TimeoutError on Telegram agents?
**Asked by:** Dniel

**Answer:** The TimeoutError for Telegram agents might be related to the model being used. Check if the model is causing the issue.
**Answered by:** Dniel

**Context:** Dniel is experiencing a TimeoutError with Telegram agents and wonders if it's related to the model.

---

## Q16: Hello, for some reason my twitter agent only posts for the first time. Every other post does not appear on the X profile but i get a message in the terminal when the other posts should appear  ['◎ Next tweet scheduled in 15 minutes']. Any solutions?
**Asked by:** ivorad

**Answer:** It seems like there might be an issue with the scheduling or posting mechanism of your Twitter agent. Check the configuration and scheduling settings to ensure posts are being made correctly.
**Answered by:** ivorad

**Context:** ivorad is facing a problem where the Twitter agent only posts for the first time and seeks solutions.

---

## Q17: Can anyone provide a workaround for working on Eliza (LocalHost) with VPN? Thank you
**Asked by:** Kyle Lenout

**Answer:** To work on Eliza (LocalHost) with a VPN, ensure that your VPN settings do not block the necessary connections for Eliza to function properly.
**Answered by:** Kyle Lenout

**Context:** Kyle Lenout needs a workaround for using Eliza on LocalHost with a VPN.

---

## Q18: how to integrate eliza with my frontend? i have running eliza on my local computer and want to use it on my frontend website, how?
**Asked by:** XFR | Cedra

**Answer:** To integrate Eliza with your frontend, you need to set up API endpoints on your backend server that communicate with your local Eliza instance. Then, your frontend can make requests to these endpoints to interact with Eliza.
**Answered by:** XFR | Cedra

**Context:** XFR | Cedra wants to know how to connect Eliza running locally to a frontend website.

---

## Q19: Can someone tell my why my character that i have setup to run and connect to a postgreSQL database (yes it is set up correctly), is still defaulting to a sqlite database? I am trying to set up agent to store conversations to this new DB setup but seems there is some kind of global or default connection happening back to sqlite. thanks!
**Asked by:** Jungle Heart

**Answer:** It sounds like there might be a default connection configuration overriding your PostgreSQL setup. Check for any global or default settings in your code that could be causing this fallback to SQLite.
**Answered by:** Not specified

**Context:** Jungle Heart is facing an issue where their character setup is not connecting to the PostgreSQL database as intended.

---

## Q20: I'm trying to build an agent that will post tweet on message from selected users on x.com. Can anyone give advice on how to do this?
**Asked by:** apshaldenai192

**Answer:** To achieve this, you would need to set up a listener for messages from selected users and then use the Twitter API to post tweets based on those messages. You can start by researching how to authenticate with the Twitter API and handle message events from x.com.
**Answered by:** Not specified

**Context:** apshaldenai192 is seeking guidance on creating an agent that posts tweets based on messages from specific users on x.com.

---

## Q21: any ideas why my eliza-starter just spams stuff like this after one message? thanks Im a total noob
**Asked by:** Hey Its Doobie

**Answer:** The behavior you're experiencing could be due to a loop or incorrect logic in your code causing the bot to spam messages. Check your message processing logic and ensure it doesn't trigger a continuous loop.
**Answered by:** Not specified

**Context:** Hey Its Doobie is encountering an issue where their bot keeps spamming messages after receiving one.

---

## Q22: my agent won't stop repeating the exact same paragraph, any ideas?
**Asked by:** kobra

**Answer:** The repeated paragraph issue could be caused by a loop in your agent's response generation logic. Review your code to identify any loops or conditions that lead to the same paragraph being repeated.
**Answered by:** Not specified

**Context:** kobra is dealing with a problem where their agent keeps repeating the same paragraph.

---

## Q23: What's the best way/approach to running 10000 different characters?
**Asked by:** big bee 🐝

**Answer:** There's a plugin on packages folder for it for you to check out
**Answered by:** Magicred1

---

## Q24: Could please somebody help me understanding how eliza works: in which files does it interacts with openai and other providers, so how does it include all of the character's info in the prompt?
**Asked by:** ALY

**Answer:** @Moderatoor please ban
**Answered by:** sagepoint

---

## Q25: Is it possible to put a range for MAX_ACTIONS_PROCESSING=2?
**Asked by:** RoomTemp IQ

**Answer:** You're adding in 'plugin-twitter' on the clients section of your character file?
**Answered by:** RoomTemp IQ

---

## Q26: So you're saying to add the plugin-twitter to the clients section
**Asked by:** sophrosyne808

**Answer:** yeah just "clients": ["twitter"], then rebuild it in the terminal w/ pnpm build
**Answered by:** RoomTemp IQ

**Context:** Discussion about adding a plugin to a specific section

---

## Q27: Are you trying to have some sort of advanced functionality?
**Asked by:** RoomTemp IQ

**Answer:** No just twitter
**Answered by:** RoomTemp IQ

**Context:** Clarification on the purpose of adding the plugin

---

## Q28: Do we need to do a separate installation of the plugin-twitter file? Or is it auto- set up when we do pnpm i?
**Asked by:** sophrosyne808

**Answer:** I just used it directly, I edited my character file to support it. For model I put {deepseek} and added a place for my API key in secret.
**Answered by:** ITZMIZZLE

---

## Q29: how would the twitter username pw stuff work when doing multiple agents on a single instance or is it not advised to do multiple agents in one instance?
**Asked by:** mike🇭🇺

**Answer:** Yes, I followed something I saw in GitHub and got it working now, something like what you've written here, thanks. Set deepseek API key in .env and model as deepseek.
**Answered by:** mike🇭🇺

---

## Q30: I'm about to try and get three agents running on my server, and wondering if I should also be creating three separate projects to manage the various twitter logins and stuff?
**Asked by:** mike🇭🇺

**Answer:** So this here is the ideal way to set up multiple agents with their own twitter logins inside a single project sharing the same project .env
**Answered by:** mike🇭🇺

---

## Q31: Hi I'm try to figure out how to use the rabbi-trader plugin. I initialized the plugin in `agent/src/index.ts` inside the `startAgent` function (before initializing the `runtime`). It seems like it's working, but ANALYZE_TRADE action isn't recognized by the agent (in the direct chat).
**Asked by:** Margol

**Answer:** No answer provided in the chat segment.
**Answered by:** 

---

## Q32: how to make anthropic spend less money cause it's expensive? maybe removing reply loops? and what is twitter_approval_enabled
**Asked by:** Jimmy

**Answer:** No answer provided in the chat segment.
**Answered by:** 

---

## Q33: how often does develop get merged into main?
**Asked by:** pixel_pavel

**Answer:** No answer provided in the chat segment.
**Answered by:** 

---

## Q34: how do i make my eliza tweet an emojie every 10th tweet?
**Asked by:** dragonlord

**Answer:** No answer provided in the chat segment.
**Answered by:** 

---

## Q35: Hey team, my plugin-web-search is working but the plugin-twitter still isn't any ideas on why this is the case? I've pnpm cleaned, pnpm i + pnpm build
**Asked by:** sophrosyne808

**Answer:** No answer provided in the chat segment.
**Answered by:** 

---

## Q36: Hey team, im trying to use a local model running with Ollama, does anyone know if this works? I see Ollama related environment variables in .env example but no mention in the docs.
**Asked by:** [ai16z] <odilitime>

**Answer:** No answer provided in the chat segment.
**Answered by:** 

---

## Q37: is it possible to augment a character's knowledge once they are live? i'm reading the docs and it sounds like the entire rag db should be loaded into the knowledge section of the character file, but that seems a bit naive? feels like i should be able to give eliza pdfs that she then adds to her knowledge base. is that possible?
**Asked by:** veTechno

**Answer:** No answer provided in the chat segment.
**Answered by:** 

---

## Q38: i have a bunch of pdfs i want to use as knowledge, now i just need to convert them to txt / md? any plan to support pdfs?
**Asked by:** veTechno

**Answer:** folder2knowledge i think does that.
**Answered by:** mark rizzn hopkins

**Context:** Discussion about converting PDFs to txt/md for knowledge use.

---

## Q39: is the action triggering? afiak the Evaluator handler is only called under certain conditions. you can also set it to always run:
**Asked by:** kAI wilder

**Answer:** I've posted several times here with no responses ... I must be alone in this. Went ahead and filed a bug report.
**Answered by:** mark rizzn hopkins

**Context:** Concerns about the action triggering and setting the Evaluator handler to always run.

---

## Q40: hey team, why are all these files not working in the Agent folder? Any ideas?
**Asked by:** sophrosyne808

**Answer:** Are you in right directory ?
**Answered by:** validsyntax

**Context:** sophrosyne808 is facing issues with files in the Agent folder

---

## Q41: says it can't find all these modules, but I've pnpm i nofrozenlockfile + pnpm build + pnpm start successfully. why is the agent folders not working?
**Asked by:** sophrosyne808

**Answer:** Yeah i'm in the one I've been using the agent with. Seems to be posting on X just fine, but when I click on the 'agent' folder these error messages pop up
**Answered by:** sophrosyne808

**Context:** sophrosyne808 elaborates on the issue despite successful pnpm commands

---

## Q42: I did a fresh pull and having problem with install,  how did  I fix?
**Asked by:** MochinoLabs

**Answer:** actually if you wait for eliza version 2, design there's alot of changes to manage multiple agents effectively
**Answered by:** elizaos-bridge-odi

**Context:** MochinoLabs seeks help with installation issues

---

## Q43: What LLM's are people using here? I'm thinking of trying deepseek but kind of looking for an LLM that generates less ehhh detectable content. People know GPT's tone/voice/writing style.
**Asked by:** RoomTemp IQ

**Answer:** my recomendation start with eliza repo not in eliza starter repo, it is more stable than the starter
**Answered by:** elizaos-bridge-odi

**Context:** RoomTemp IQ inquires about LLM recommendations

---

## Q44: Lmao what is the deepseek env var? DEEPSEEK_API_KEY?
**Asked by:** RoomTemp IQ

**Answer:** It's not in the sample template (or I deleted it by accident)
**Answered by:** RoomTemp IQ

**Context:** RoomTemp IQ seeks clarification on deepseek environment variable

---

## Q45: I'm building a plugin but I'm not sure if I should be using the plugin starter or the eliza os? The big difference i've seen is that ```import { Action, HandlerCallback, IAgentRuntime, Memory, Plugin, State, ModelClass, } from "@elizaos/core";``` the main repo does this and then the starter has examples like this: ```import { Action, HandlerCallback, IAgentRuntime, Memory, State } from "@ai16z/eliza";``` I think those type defs are the same but ... some seem to be different?
**Asked by:** fourcolors

**Answer:** The main difference between the plugin starter and the eliza os is in the import statements. The type definitions you mentioned are similar, but there are differences in the imports themselves.
**Answered by:** Not specified

**Context:** fourcolors is seeking clarification on whether to use the plugin starter or eliza os for building a plugin, specifically focusing on the differences in import statements.

---

## Q46: [elizaos] <_degen_dev_> im running deepseek locally with ollama, any idea how to get eliza repo running with it?
**Asked by:** elizaos-bridge-odi

**Answer:** To get the eliza repo running with deepseek locally using ollama, you may need to follow specific setup steps or configurations. It's recommended to check the documentation or seek guidance from the respective repositories for compatibility and integration details.
**Answered by:** Not specified

**Context:** elizaos-bridge-odi is inquiring about running the eliza repository with deepseek locally using ollama and is looking for guidance on the setup process.

---



## Questions Only

DEPLOYMENT & ENVIRONMENT
1. How to deploy Eliza on different platforms? (VPS, EC2, Vercel, Railway, etc.)
2. What are the minimum system requirements?
3. How to run multiple agents simultaneously?
4. How to handle environment variables securely?
5. Is WSL2 required for Windows users?
6. What's the best OS for deployment?
7. How to persist data between deployments?
8. How to deploy with Docker?
9. How to scale the application?
10. How to handle different Node.js versions?

TWITTER/SOCIAL MEDIA
11. How to avoid Twitter bot bans/suspensions?
12. How to fix Twitter login/authentication issues?
13. How to control tweet frequency?
14. How to make agents respond to specific tweets?
15. How to handle Twitter cookies and API keys?
16. How to scrape Twitter data safely?
17. How to implement auto-retweeting?
18. How to handle tweet length limits?
19. How to post images on Twitter?
20. How to integrate with Twitter Spaces?
21. How to mark accounts as automated?
22. How to handle rate limiting?
23. How to manage multiple Twitter accounts?
24. How to implement tweet templates?
25. How to handle tweet threading?

DATABASE & MEMORY
26. How to resolve SQLite errors?
27. How to switch to PostgreSQL?
28. How to handle vector dimension mismatches?
29. How to implement conversation memory?
30. How to manage database migrations?
31. How to backup/restore the database?
32. How to use Supabase adapter?
33. How to handle data persistence?
34. How to implement knowledge bases?
35. How to query stored memories?

CHARACTER CONFIGURATION
36. How to modify character files?
37. How to make changes take effect?
38. How to configure model providers?
39. How to set personality traits?
40. How to handle multilingual support?
41. How to implement character lore?
42. How to manage character memory?
43. How to set response templates?
44. How to control response length?
45. How to implement character goals?

PLUGINS & FEATURES
46. How to create custom plugins?
47. How to enable image generation?
48. How to implement voice synthesis?
49. How to integrate with Discord/Telegram?
50. How to add web search capability?
51. How to implement crypto features?
52. How to add RSS feeds?
53. How to handle file uploads?
54. How to implement custom actions?
55. How to add API integrations?

MODEL & AI
56. How to choose between different AI models?
57. How to handle API costs?
58. How to implement local models?
59. How to use Llama models?
60. How to optimize token usage?
61. How to handle context windows?
62. How to implement RAG?
63. How to fine-tune responses?
64. How to handle prompt engineering?
65. How to manage model fallbacks?

DEVELOPMENT & DEBUGGING
66. How to resolve pnpm errors?
67. How to debug agent behavior?
68. How to implement logging?
69. How to handle testing?
70. How to contribute to the project?
71. How to handle TypeScript configurations?
72. How to implement CI/CD?
73. How to handle versioning?
74. How to debug memory leaks?
75. How to optimize performance?

SECURITY & AUTHENTICATION
76. How to handle API keys securely?
77. How to implement authentication?
78. How to handle user permissions?
79. How to secure endpoints?
80. How to implement rate limiting?

CUSTOMIZATION & INTEGRATION
81. How to implement custom UIs?
82. How to integrate with existing systems?
83. How to handle webhooks?
84. How to customize response formats?
85. How to implement custom protocols?
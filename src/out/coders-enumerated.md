# Additional Common Questions (Not in Popular FAQ)

### Development & Debugging

1. **Local Development Questions:**
   - How do I run Eliza without a GPU/CUDA?
   - How do I set up proper monitoring and error handling?
   - How do I debug my agent when it's not working as expected?

**Answer:**  
Use `pnpm start:debug` for debugging, check logs for error messages. For non-GPU setups, use cloud model providers instead of local models.

---

2. **Language Support:**
   - How do I make my agent interact in languages other than English?
   - How do I configure multilingual responses?

**Answer:**  
Configure language preferences in character file's bio and lore sections. Some models (like GPT-4) handle multiple languages better than others.

---

3. **Self-Talk Issues:**
   - Why does my agent keep talking to itself?
   - How do I prevent recursive conversations?

**Answer:**  
Check conversation triggers and self-talk limitations in character configuration. Implement proper conversation end conditions.

---

4. **Database Configuration:**
   - How do I set up Supabase adapter?
   - How do I handle database pool reconnection errors?

**Answer:**  
Initialize database with correct schema, configure connection in `.env`, implement proper error handling for connection issues.

---

5. **Workflow Automation:**
   - How do I handle multi-agent systems?
   - How do I implement agent-to-agent communication?

**Answer:**  
Use separate character files for each agent, configure proper communication channels, implement message passing through shared memory or API calls.

---

6. **Security Concerns:**
   - Where should I store API keys securely?
   - How do I handle sensitive data in production?

**Answer:**  
Use `.env` for API keys, keep secrets out of version control, use environment variables in production, consider using secret management services.

---

7. **Performance Optimization:**
   - How do I optimize memory usage for multiple agents?
   - How do I improve response times?

**Answer:**  
Monitor memory usage, implement proper garbage collection, use caching where appropriate, consider using smaller models for faster responses.

---

8. **Custom Templates:**
   - How do I create custom response templates?
   - How do I implement custom interaction patterns?

**Answer:**  
Define templates in character.json, use proper formatting for different platforms, implement custom plugins for specific interaction patterns.

---

9. **Error Recovery:**
   - How do I handle API rate limits?
   - What's the best way to implement retry logic?

**Answer:**  
Implement exponential backoff, proper error handling, and fallback options for different API providers.

---

10. **Testing:**
    - How do I test my agent's responses?
    - How do I implement automated testing?

**Answer:**  
Use test environment configurations, implement unit tests for plugins, use mock APIs for testing interactions.

11. **Windows-Specific Issues:**
    - How do I run ElizaOS on Windows?
    - How do I resolve WSL-related problems?

**Answer:**  
Use WSL2 (Windows Subsystem for Linux) with Ubuntu for best results. Install VS Code WSL extension for development. Move to WSL filesystem rather than /mnt to avoid path issues.

---

12. **Character File Management:**
    - How do I use environment variables in character files?
    - How do I manage multiple character configurations?

**Answer:**  
Character-specific settings go in character.json, while global settings belong in .env. Create separate character files for different personas and configurations.

---

13. **Rate Limiting:**
    - How do I handle Twitter rate limits?
    - How do I avoid account suspensions?

**Answer:**  
Space out interactions using POST_INTERVAL settings, mark account as automated in Twitter settings, avoid using proxies as they can trigger suspicion.

---

14. **Plugin Development:**
    - How do I create custom plugins?
    - Can plugins interact with each other?

**Answer:**  
Create plugins in packages directory, implement required interfaces (actions, providers, evaluators), and ensure proper dependency management. Plugins can interact through the agent's runtime.

---

15. **RAG Implementation:**
    - How do I implement RAG effectively?
    - How do I manage large knowledge bases?

**Answer:**  
Use folder2knowledge for document conversion, implement proper vector storage, consider chunking large documents, and use appropriate embedding models.

---

16. **Client Integration:**
    - How do I add new client platforms?
    - How do I customize client behavior?

**Answer:**  
Implement client interface, handle platform-specific formatting, manage authentication, and configure proper event handling for each platform.

---

17. **Proxy Configuration:**
    - How do I set up proxies for Twitter?
    - How do I handle IP-based restrictions?

**Answer:**  
Use residential proxies when needed, configure proxy settings in .env, consider using VPN for development, be cautious with datacenter IPs.

---

18. **Cost Management:**
    - How do I optimize token usage?
    - How do I reduce API costs?

**Answer:**  
Configure maxTokens settings, use smaller models when possible, implement caching, and monitor usage patterns. Consider using local models for development.

---

19. **Deployment Scaling:**
    - How do I scale multiple agents?
    - How do I manage resources across agents?

**Answer:**  
Use container orchestration, implement proper monitoring, scale database accordingly, consider using message queues for communication.

---

20. **Version Management:**
    - How do I update Eliza safely?
    - How do I handle breaking changes?

**Answer:**  
Follow semantic versioning, test updates in staging environment, maintain backup of configurations, and review changelog before updating.

---

21. **Platform-Specific Formatting:**
    - How do I handle different platform requirements?
    - How do I maintain consistent output across services?

**Answer:**  
Implement platform-specific formatters, handle character limits and formatting rules per platform, use templating system for consistency.

---

22. **Data Persistence:**
    - How do I backup agent data?
    - How do I migrate between databases?

**Answer:**  
Regular database backups, implement proper migration scripts, use database-agnostic interfaces when possible.

---

23. **Environment Management:**
    - How do I manage different environments?
    - How do I handle staging vs production?

**Answer:**  
Use environment-specific .env files, implement proper configuration management, maintain separate credentials for each environment.

---

24. **Monitoring & Logging:**
    - How do I implement proper logging?
    - How do I monitor agent health?

**Answer:**  
Use structured logging, implement health checks, monitor resource usage, set up alerts for critical issues.

---

25. **Character Interaction:**
    - How do I implement character relationships?
    - How do I manage multi-character conversations?

**Answer:**  
Use shared memory systems, implement proper conversation tracking, maintain character consistency through configuration.

---

26. **Discord Integration:**
    - How do I set up Discord bot functionality?
    - How do I handle Discord.js opus installation errors?

**Answer:**  
Remove @discordjs/opus and use opusscript instead, ensure proper bot permissions, configure Discord client in character file.

---

27. **Telegram Integration:**
    - How do I fix Telegram bot issues?
    - How do I unify knowledge base across Telegram chats?

**Answer:**  
Ensure bot has admin privileges, properly configure in Bot Father, implement proper group chat handling, use centralized knowledge repository.

---

28. **Model Chaining:**
    - How do I chain multiple models together?
    - How do I implement model pipelines?

**Answer:**  
Create model pipeline configurations, handle inter-model communication, manage context passing between models.

---

29. **Advanced Vector Operations:**
    - How do I implement custom vector operations?
    - How do I optimize vector search algorithms?

**Answer:**  
Implement custom vector similarity metrics, optimize search algorithms, handle high-dimensional vector operations.

---

30. **Session Management:**
    - How do I manage user sessions across platforms?
    - How do I handle session persistence?

**Answer:**  
Implement session tracking system, handle cross-platform session synchronization, manage session storage and cleanup.

---

31. **Rate Control:**
    - How do I implement custom rate limiting?
    - How do I manage API quotas across services?

**Answer:**  
Implement token bucket algorithm, manage quota distribution, handle rate limit recovery.

---

32. **Template System:**
    - How do I create a custom template system?
    - How do I manage template variations?

**Answer:**  
Implement template inheritance system, manage platform-specific templates, handle dynamic template selection.

---

33. **Relevance Scoring:**
    - How do I adjust interaction relevance thresholds?
    - How do I improve response targeting?

**Answer:**  
Configure relevance scores in post.ts and interactions.ts, adjust thresholds based on use case, implement custom scoring logic if needed.

---

34. **Phala Cloud Integration:**
    - How do I deploy to Phala Cloud?
    - How do I handle Phala-specific configurations?

**Answer:**  
Follow Phala deployment guidelines, configure proper worker settings, ensure compatibility with cloud environment.

---

35. **Railway Deployment:**
    - How do I deploy to Railway?
    - How do I handle Railway environment variables?

**Answer:**  
Use Railway CLI for deployment, configure proper build commands, set up environment variables in Railway dashboard.

---

36. **Vector Store Management:**
    - How do I optimize vector storage?
    - How do I handle vector store migrations?

**Answer:**  
Implement proper indexing, manage embedding dimensions consistently, handle storage scaling, implement backup procedures.

---

37. **Action Processing:**
    - How do I create custom actions?
    - How do I control action execution flow?

**Answer:**  
Implement action interfaces, handle validation and execution logic, manage action queues and priorities.

---

38. **Conversation Context:**
    - How do I manage conversation history?
    - How do I implement context windows?

**Answer:**  
Configure proper context length, implement sliding windows, manage token usage, handle context pruning.

---

39. **Model Fallbacks:**
    - How do I implement model failover?
    - How do I handle provider outages?

**Answer:**  
Configure backup providers, implement retry logic, handle graceful degradation to smaller models.

---

40. **Webhook Integration:**
    - How do I set up webhook endpoints?
    - How do I handle webhook security?

**Answer:**  
Implement proper endpoint validation, handle authentication, manage webhook payload processing.

41. **Boredom Provider:**
    - How do I configure the boredom provider?
    - How do I prevent unwanted automated posts?

**Answer:**  
Remove bootstrap plugin or configure boredom provider settings in character file to control automated posting behavior.

---

42. **Cookie Management:**
    - How do I properly format Twitter cookies?
    - How do I handle cookie expiration?

**Answer:**  
Format cookies as JSON array with proper domain and security settings, implement refresh mechanisms for expired cookies.

---

43. **Suspicious Activity:**
    - How do I prevent Twitter from flagging my bot?
    - How do I handle account restrictions?

**Answer:**  
Mark account as automated, use residential IPs, implement natural posting patterns, avoid suspicious activity patterns.

---

44. **Data Pipeline:**
    - How do I implement custom data pipelines?
    - How do I process external data sources?

**Answer:**  
Create custom plugins for data processing, implement proper error handling, manage data flow through the system.

---

45. **Search Configuration:**
    - How do I configure Twitter search?
    - How do I disable unwanted search features?

**Answer:**  
Set `TWITTER_SEARCH_ENABLE=false` to disable search, configure `TWITTER_TARGET_USERS` for specific accounts, adjust search parameters in character file.

---

46. **Captcha Handling:**
    - How do I handle Twitter captchas?
    - How do I manage automated verification?

**Answer:**  
Use same IP for captcha solving as agent, implement proper retry logic, consider manual verification when needed.

---

47. **Premium API:**
    - How do I use Twitter Premium API?
    - What are the benefits over standard API?

**Answer:**  
Configure Premium API credentials, higher rate limits, better stability, additional features for automation.

---

48. **Message Formatting:**
    - How do I fix JSON formatting in tweets?
    - How do I handle platform-specific formatting?

**Answer:**  
Implement proper template processing, handle platform-specific character limits, ensure proper text formatting before posting.

---

49. **Agent Initialization:**
    - How do I customize agent startup?
    - How do I handle initialization errors?

**Answer:**  
Configure startup parameters in character file, implement proper error handling during initialization, manage startup sequence.

---

50. **Resource Allocation:**
    - How do I allocate resources between agents?
    - How do I handle resource constraints?

**Answer:**  
Implement resource pooling, manage memory allocation, configure proper limits per agent, monitor resource usage.

51. **News Feed Integration:**
    - How do I integrate news feeds into my agent?
    - How do I filter relevant news content?

**Answer:**  
Implement RSS/news feed plugins, configure content filtering rules, handle content processing and summarization.

---

52. **Character Development:**
    - How do I evolve character personality over time?
    - How do I implement adaptive behavior?

**Answer:**  
Implement personality evolution system, track interaction history, adjust behavior based on experience and feedback.

---

53. **Solana Integration:**
    - How do I get token data on Solana?
    - How do I handle Solana API rate limits?

**Answer:**  
Use established blockchain data providers, implement proper rate limiting, handle API failures gracefully.

---

54. **Local Character Generation:**
    - How do I generate characters locally?
    - How do I handle character generation errors?

**Answer:**  
Use local generation tools, implement proper validation, handle generation failures and retries.

---

55. **Neynar Alternatives:**
    - What are the alternatives to Neynar for Farcaster?
    - How do I implement custom Farcaster integration?

**Answer:**  
Use open-source alternatives like ai16z/eliza, implement custom Farcaster client, handle protocol-specific requirements.
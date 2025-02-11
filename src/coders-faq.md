# Coders FAQ

[toc]

## Prompt

```!
Can you extract the most frequently asked questions and answers from here:

and format like this:

### [Common User Questions]

[Concise 1-2 Sentence Answer]

No brackets around responses please
```

---

## Repeated Questions

Let me analyze the list for repeated questions. I'll group similar questions and note their repetitions:

### Repeated Questions about Deployment
1. "How do I deploy Eliza in production/cloud?"
   - Appears multiple times with slightly different wording
   - Consistent advice about using Docker on cloud services like DigitalOcean, AWS, or Google Cloud

### Repeated Questions about Running Multiple Agents
1. "How do I run multiple agents simultaneously?"
   - Appears at least 3 times
   - Consistent advice to use `pnpm start --characters="characters/1.character.json,characters/2.character.json"`

### Repeated Questions about Model Providers
1. "How do I configure the model provider and switch between different models?"
   - Appears multiple times
   - Consistent advice to set `modelProvider` in character.json and configure API keys in .env

### Repeated Questions about Twitter Integration
1. "How do I set up Twitter/X integration?"
   - Multiple variations about Twitter client configuration
   - Consistent advice about adding credentials to .env and character files

### Repeated Questions about Preventing Spam/Multiple Posts
1. "Why is my agent posting/replying multiple times or spamming tweets?"
   - Multiple variations of this question
   - Consistent solution: Set `ENABLE_ACTION_PROCESSING=false` and adjust interval settings

### Repeated Questions about Agent Memory
1. "How do I clear/reset the agent's memory?"
   - Appears multiple times
   - Consistent advice to delete the SQLite database file or use `pnpm cleanstart`

### Repeated Questions about Plugins
1. "How do I add plugins to my character?"
   - Multiple similar questions
   - Consistent advice to add plugins to character.json and ensure they're installed

### Repeated Questions about Installation Issues
1. "Why does my build fail with dependency errors?"
   - Multiple variations about installation problems
   - Consistent advice to use Node.js 23+, run `pnpm install --no-frozen-lockfile`

These repeated questions suggest some common pain points and areas of confusion for users setting up and configuring Eliza agents. The consistency in answers across repetitions indicates that the documentation and community support have developed clear solutions to these common issues.



---

# ElizaOS Common Questions & Answers

### How do I get started with ElizaOS?
Use eliza-starter for a simpler setup with limited dependencies, then add what you need. Run `pnpm install --no-frozen-lockfile` followed by `pnpm build` to initialize.

### Which Node.js version should I use?
Use Node.js version 23.3.0 for optimal compatibility. Install using `nvm install 23.3.0` and `nvm use 23.3.0`.

### How do I reset my agent's memory?
Delete the SQLite database file in the /data directory and restart the agent to clear all memories.

### How do I prevent my agent from tweeting twice?
Modify the Twitter client's interaction handling in `packages/client-twitter/index.ts` and adjust the `TWITTER_POLL_INTERVAL` in your .env file.

### How do I change which model my agent uses?
Set the `modelProvider` in your character.json file and configure the corresponding API keys in your .env file.

### How do I make my agent only respond to mentions?
Add a mention filter to your character's configuration and set `ENABLE_ACTION_PROCESSING=false` in your .env file.

### How do I add a plugin to my agent?
Add the plugin name to the "plugins" array in your character.json file and ensure the plugin is properly installed in your project dependencies.

### How do I deploy my agent to production?
Use Docker for containerization and deploy to a cloud service like DigitalOcean, AWS, or Google Cloud with at least 4GB RAM and 50GB storage.

### How do I enable my agent to post on Twitter?
Add "twitter" to the clients array in your character.json and configure Twitter credentials in your .env file.

### How do I make my agent use a cheaper/smaller model?
Configure `gpt-4o-mini` as your model in the .env file and character settings to minimize costs.

### How do I add custom knowledge to my agent?
Use the knowledge section in your character.json file or implement a custom vector database for larger datasets.

### How do I implement custom actions?
Create a new plugin with your action logic and register it in your agent's configuration.

Here are the most frequently asked questions and common themes from the chat logs:

### How do I run multiple agents simultaneously?
Use the command `pnpm start --characters="characters/1.character.json,characters/2.character.json"` with comma-separated character files. Multiple agents can run in the same process.

### Why is my agent posting/replying multiple times or spamming tweets?
Set ENABLE_ACTION_PROCESSING=false in your .env file and adjust POST_INTERVAL_MIN, POST_INTERVAL_MAX, and ACTION_INTERVAL settings to control posting frequency.

### How do I deploy Eliza in production/on a VPS?
Most users deploy on cloud VPS services like DigitalOcean, AWS, or GCP using Docker. Be cautious with Twitter automation from datacenter IPs as they may trigger account restrictions.

### How do I set up Eliza on Windows?
Use Windows Subsystem for Linux (WSL2) with Ubuntu for best results. Native Windows support is limited and may cause issues.

### How do I add plugins to my character?
Add plugins to your character.json file under the "plugins" array like: `"plugins": ["@Elizaos/plugin-name"]`. Make sure to install the plugin first using pnpm.

### Why am I getting Twitter authentication/login errors?
Common causes include incorrect credentials, suspicious activity detection, or rate limiting. Try using cookies for authentication or waiting before retrying.

### How do I clear/reset the agent's memory?
Use `pnpm cleanstart` command or manually delete the database file and cached data before restarting the agent.

### How do I get my agent to use knowledge from external sources?
Use the RAG (Retrieval Augmented Generation) system by adding knowledge to your character file or connecting to external databases through adapters.

### Why does my build fail with dependency errors?
Make sure you're using Node.js version 23+, run `pnpm install --no-frozen-lockfile`, and ensure all required dependencies are installed correctly.

### How do I configure the database (PostgreSQL/Supabase)?
Set up the correct database URL in your .env file and ensure you've run the proper migration scripts with the required schema and functions.

Let me analyze these chat logs and extract the most frequently asked questions and answers, formatted as requested.

### How do I set up Twitter/X integration with Eliza?
Add your Twitter credentials to the .env file and character file. Make sure to enable the automated tag in your Twitter account settings and configure TWITTER_POLL_INTERVAL to manage interaction frequency.

### How do I properly configure the model provider and switch between different models?
Set the model provider in your character file (e.g., "modelProvider": "anthropic") and configure the corresponding API keys in your .env file. You can specify different models for small/medium/large in your .env file.

### Why isn't my agent responding to mentions/interactions?
The agent evaluates relevance scores before responding. Check your interaction settings in post.ts and interactions.ts, and ensure your POLL_INTERVAL settings aren't too aggressive.

### How do I deploy Eliza in production/cloud?
Deploy using Docker on cloud services like AWS EC2, Railway, or Phala Cloud. For basic setups, an 8GB RAM instance can handle multiple agents (approximately 6 agents).

### How do I handle agent memory and database storage?
Use SQLite for simple deployments (delete db.sqlite to reset memory) or Postgres/Supabase for more complex needs. RAG knowledge can be configured in the character file with "ragKnowledge": true.

### How do I integrate plugins with my agent?
Add the plugin name to your character file's plugins section and configure any required API keys in .env. Some plugins may require additional configuration in the character file's secrets section.

### What's the difference between eliza-starter and full Eliza?
Eliza-starter is a lightweight version made by the community, while full Eliza is the main repository with more features. The full version is recommended as the starter can be buggy and limited.

### How do I make my agent's responses more natural/less repetitive?
Customize the character's bio, lore, and post examples in the character file. Add more varied response templates and adjust the interaction settings to control response frequency.

### How do I enable image generation/vision capabilities?
Configure an image provider (like OpenAI) in your character file and .env. Different models support different vision capabilities - ensure your chosen provider supports image analysis.

### How do I run multiple agents simultaneously?
You can run multiple agents either by specifying multiple character files at startup or running separate instances. Each agent requires additional resources - plan for about 2GB RAM per agent.


### How do I properly deploy Eliza in production/cloud environments?
Most users deploy using Docker on cloud services like Digital Ocean, Railway, AWS EC2, or Phala Cloud. For basic setups, an 8GB RAM instance can handle approximately 6 agents. Pay attention to environment configuration and proper handling of secrets.

### How do I resolve common installation and setup errors?
Most installation issues can be resolved by ensuring node version 23.3.0, using `pnpm install --no-frozen-lockfile`, cleaning cache with `pnpm clean`, and rebuilding with `pnpm build`. For Windows users, WSL is recommended.

### How can I customize my agent's Twitter interactions and behavior?
Configure settings in the .env file or character file secrets using variables like TWITTER_POLL_INTERVAL for timing, ENABLE_ACTION_PROCESSING for interaction control, and TWITTER_TARGET_USERS for specifying accounts to interact with. Additional control can be achieved through custom plugins.

### What's the best way to handle secrets and environment variables?
Secrets can be stored either in the .env file (for global settings) or in the character file's secrets section (for character-specific settings). Character-specific secrets take precedence over global .env variables.

### How do I run multiple agents simultaneously?
Run multiple agents by creating separate character files with their own secrets and configurations, then launch them using `pnpm start --characters="characters/char1.json,characters/char2.json"`. Each agent requires additional resources (~2GB RAM).

### How can I use different model providers (OpenAI, DeepSeek, Anthropic, etc.)?
Set the modelProvider in your character file (e.g., "modelProvider": "anthropic") and configure corresponding API keys in .env or character secrets. Different models can be used for different purposes like image processing vs text generation.

### How do I properly set up and use plugins?
Plugins are added to the character file's plugins section. Some come pre-installed with Eliza while custom plugins need to be properly imported and configured. Check the packages folder for available plugins and their documentation.

### How can I make my agent's responses more natural/less bot-like?
Fine-tune the character's bio, lore, and post examples in the character file. Consider using different model providers and adjusting interaction settings. Some models (like DeepSeek) are noted for more natural responses.

### How do I manage the agent's memory and knowledge base?
Use RAG knowledge in the character file for static knowledge, and the memory system (SQLite or PostgreSQL/Supabase) for dynamic interactions. Clear the database (db.sqlite) to reset memory when needed.

### How do I debug issues when my agent isn't working as expected?
Check logs for error messages, verify environment variables and secrets are properly set, ensure correct node version (23.3.0), and consider clearing cache and database if issues persist. Add logging statements to track execution flow.


### How do I run Eliza without a GPU/CUDA?
You can switch the modelProvider in your configuration from LLAMALOCAL to alternatives like OPENAI or use cloud-based options that don't require local GPU processing.

### How do I fix pnpm-lock.yaml conflicts and installation issues?
Run `pnpm install --no-frozen-lockfile` to regenerate the lockfile, and ensure both the root and package-specific lockfiles are updated when adding new plugins.

### How do I properly configure the Twitter client/bot?
Set up your Twitter API credentials in the .env file, configure the TWITTER_RETRY_LIMIT for login attempts, and ensure your character file has the correct client settings.

### How do I handle agent memory and knowledge base?
Agents have built-in memory capabilities through various database adapters (PostgreSQL, Supabase, MongoDB), and you can configure vector stores for knowledge management.

### What's the best way to get started with Eliza development?
Start with either the eliza-starter repository for basic functionality or create-eliza-app for a more streamlined setup, then follow the dev school video tutorials available on YouTube.

### How do I make my agent interact in languages other than English?
Configure the language preferences in your character file's bio and lore sections, and specify the desired language in the character's configuration.

### How do I integrate plugins into my Eliza project?
Add the plugin to your project's dependencies, update the package.json and pnpm-lock.yaml files, and configure the plugin in your character file or environment settings.

### Why does my agent keep talking to itself?
Check your character configuration and interaction settings - this usually happens when the agent's conversation triggers aren't properly configured or when self-talk limitations aren't set.

### How do I set up proper monitoring and error handling for my agent?
Implement logging mechanisms, set up error handlers in your code, and use the built-in debugging tools by running with `pnpm start:debug` to track issues.

### How do I handle multi-agent systems and workflow automation?
Eliza supports multi-agent architectures natively - configure separate character files for each agent and use the proper client configurations to enable inter-agent communication.

Here are the most frequently asked questions and answers extracted from the chat logs:

### How do I fix Twitter login/authentication issues (399 errors, etc.)?
Enable 2FA on the Twitter account, ensure cookies are set properly, and verify credentials in .env or character file secrets. Some users resolved this by manually logging into the account first.

### How do I run multiple agents simultaneously? 
Use the command `pnpm start --characters="characters/agent1.json,characters/agent2.json"` and ensure each agent has unique credentials in their character files.

### How do I properly set up the model provider in character files?
Specify the modelProvider in the character file (e.g., "openai", "anthropic", "ollama") and set corresponding API keys in .env file or character secrets.

### How do I deploy Eliza to production?
Most users deploy on VPS providers like DigitalOcean or AWS using Docker. For persistence, use PostgreSQL instead of SQLite. Make sure to use Node.js v23.3.0 or higher.

### How do I control tweet frequency and responses?
Set POST_INTERVAL_MIN and POST_INTERVAL_MAX in .env for tweet frequency. Use TWITTER_POLL_INTERVAL to control how often agent checks for interactions. Default is 120 seconds.

### How do I run local models with Eliza?
Use Ollama for local models - install Ollama, download desired model (e.g., llama3.1), set modelProvider to "ollama" in character file and configure OLLAMA settings in .env.

### How do I add custom plugins to Eliza?
Create plugin in agent/plugins directory, add to package.json with "workspace:*", import in agent/src/index.ts, and specify in character file's plugins array.

### How do I fix the "Vector dimension mismatch" error?
This usually occurs when switching between different embedding models. Clear the database (delete sqlite.db) and rebuild with consistent embedding dimensions.

### How do I make my agent respond to specific Twitter accounts?
Set TWITTER_TARGET_USERS in .env with comma-separated usernames. Agent will monitor and respond to tweets from these accounts based on configuration.

### What's the recommended way to store agent knowledge/memory?
Use the knowledge field in character files for static data. For dynamic data, use the memory system through providers or custom plugins. Large datasets should use proper database storage.

### Common User Questions

### How do I control my Twitter bot's posting frequency?
Set POST_INTERVAL_MIN and POST_INTERVAL_MAX in .env file and ENABLE_ACTION_PROCESSING=false. For more stable behavior, consider using version 0.1.6-alpha.4.

### Why does my agent spam tweets/retweets?
Set ENABLE_ACTION_PROCESSING=false in .env and increase polling interval. Version 0.1.6-alpha.4 provides more controlled behavior.

### How do I fix pnpm installation errors?
Use Node.js v23.3.0, delete node_modules folder, then run pnpm install followed by pnpm build.

### Why is my agent not responding to mentions?
Verify Twitter credentials are correct and target users are properly configured in your character file. Some accounts need manual activity before automation works reliably.

### How do I make my agent post images?
Set IMAGE_GEN=TRUE in .env and configure an image provider like DALL-E. Check agent-twitter-client documentation for implementation details.

### How do I change which model my agent uses?
Specify modelProvider in character.json and add corresponding API key to .env file. Check runtime logs to confirm which model is being used.

### How do I fix "SqliteError: Vector dimension mismatch"?
Delete db.sqlite in agent/data folder and rebuild. If using Near plugin, try removing it.

### What are the minimum system requirements?
Basic setup needs Node.js, 2-4GB RAM minimum, and necessary API keys. Can run locally or on cloud service.

### How do I implement RAG (Retrieval-Augmented Generation)?
Use folder2knowledge to convert documents into knowledge, then use knowledge2character to create character files. The agent stores context in its memory system.

### How do I deploy my agent?
You can run locally or use cloud services. PM2 is recommended for production deployment.

### How do I debug my agent?
Use pnpm start:debug command and check runtime logs. Clear database and rebuild if behavior seems cached.

### How do I add custom actions?
Create actions in a plugin following the architecture, register with runtime, and implement validation logic. Watch agent dev school videos for detailed guidance.

### Where should I store API keys?
Use .env file for API keys and sensitive data. Character file's secrets section can also be used but keep it out of version control.

### How do I set up Supabase adapter?
Initialize Supabase database with correct schema and configure connection in .env file. Handle pool reconnection errors as needed.

### How do I make my agent more interactive?
Configure proper templates in character.json and implement custom plugins for desired functionality. Consider using plugin-bootstrap as a starting point.

---

# Consolidated ElizaOS FAQ

### **General Setup & Installation**
1. **How do I get started with ElizaOS?**
   - Use `eliza-starter` for a simpler setup with limited dependencies. Run `pnpm install --no-frozen-lockfile` followed by `pnpm build` to initialize.

2. **Which Node.js version should I use?**
   - Use **Node.js version 23.3.0** for optimal compatibility. Install using `nvm install 23.3.0` and `nvm use 23.3.0`.

3. **How do I fix installation errors?**
   - Ensure Node.js version 23.3.0, run `pnpm install --no-frozen-lockfile`, clean cache with `pnpm clean`, and rebuild with `pnpm build`. For Windows, use **WSL2**.

4. **What are the minimum system requirements?**
   - Basic setup requires Node.js, 2-4GB RAM, and necessary API keys. Can run locally or on cloud services.

---

### **Deployment**
1. **How do I deploy Eliza in production/cloud?**
   - Use **Docker** for containerization and deploy to cloud services like **DigitalOcean, AWS, or Google Cloud**. For basic setups, an 8GB RAM instance can handle multiple agents (approximately 6 agents).

2. **How do I deploy without a GPU/CUDA?**
   - Switch the `modelProvider` in your configuration from `LLAMALOCAL` to alternatives like `OPENAI` or use cloud-based options that don’t require local GPU processing.

---

### **Running Multiple Agents**
1. **How do I run multiple agents simultaneously?**
   - Use the command:  
     ```bash
     pnpm start --characters="characters/1.character.json,characters/2.character.json"
     ```
   - Each agent requires additional resources (~2GB RAM).

---

### **Model Configuration**
1. **How do I configure the model provider and switch between models?**
   - Set the `modelProvider` in your `character.json` (e.g., `"anthropic"`) and configure the corresponding API keys in `.env`. Different models can be used for text generation, image processing, etc.

2. **How do I use local models with Eliza?**
   - Use **Ollama** for local models. Install Ollama, download the desired model (e.g., `llama3.1`), set `modelProvider` to `"ollama"` in the character file, and configure `OLLAMA` settings in `.env`.

3. **How do I make my agent use a cheaper/smaller model?**
   - Configure `gpt-4o-mini` as your model in `.env` and character settings to minimize costs.

---

### **Twitter Integration**
1. **How do I set up Twitter/X integration?**
   - Add Twitter credentials to `.env` and the character file. Enable the automated tag in your Twitter account settings and configure `TWITTER_POLL_INTERVAL` to manage interaction frequency.

2. **How do I prevent my agent from spamming tweets?**
   - Set `ENABLE_ACTION_PROCESSING=false` in `.env` and adjust `POST_INTERVAL_MIN`, `POST_INTERVAL_MAX`, and `ACTION_INTERVAL` settings to control posting frequency.

3. **Why is my agent not responding to mentions?**
   - Verify Twitter credentials and ensure target users are properly configured in your character file. Some accounts need manual activity before automation works reliably.

4. **How do I make my agent post images on Twitter?**
   - Set `IMAGE_GEN=TRUE` in `.env` and configure an image provider like **DALL-E**. Check `agent-twitter-client` documentation for implementation details.

---

### **Agent Memory & Knowledge**
1. **How do I clear/reset the agent's memory?**
   - Delete the SQLite database file in the `/data` directory or use `pnpm cleanstart` to reset memory.

2. **How do I add custom knowledge to my agent?**
   - Use the `knowledge` section in your `character.json` file or implement a custom vector database for larger datasets.

3. **How do I handle the "Vector dimension mismatch" error?**
   - This occurs when switching between embedding models. Clear the database (delete `sqlite.db`) and rebuild with consistent embedding dimensions.

---

### **Plugins & Custom Actions**
1. **How do I add plugins to my agent?**
   - Add the plugin name to the `"plugins"` array in your `character.json` file (e.g., `"plugins": ["@Elizaos/plugin-name"]`). Ensure the plugin is installed in your project dependencies.

2. **How do I implement custom actions?**
   - Create a new plugin with your action logic and register it in your agent's configuration. Watch **Eliza Dev School** videos for detailed guidance.

3. **How do I debug plugin-related issues?**
   - Check logs for error messages, verify environment variables, and ensure the plugin is properly imported and configured.

---

### **Agent Behavior & Customization**
1. **How do I make my agent's responses more natural/less repetitive?**
   - Customize the character's `bio`, `lore`, and `post examples` in the `character.json` file. Adjust interaction settings and consider using different model providers.

2. **How do I make my agent interact in languages other than English?**
   - Configure the language preferences in your character file's `bio` and `lore` sections, and specify the desired language in the character's configuration.

3. **Why does my agent keep talking to itself?**
   - Check your character configuration and interaction settings. This usually happens when conversation triggers aren’t properly configured or self-talk limitations aren’t set.

---

### **Troubleshooting**
1. **Why does my build fail with dependency errors?**
   - Ensure Node.js version 23+, run `pnpm install --no-frozen-lockfile`, and verify all required dependencies are installed correctly.

2. **How do I fix Twitter login/authentication issues (399 errors, etc.)?**
   - Enable 2FA on the Twitter account, ensure cookies are set properly, and verify credentials in `.env` or character file secrets. Some users resolved this by manually logging into the account first.

3. **How do I debug issues when my agent isn’t working as expected?**
   - Check logs for error messages, verify environment variables, and ensure the correct Node.js version. Use `pnpm start:debug` to track execution flow.

---

### **Advanced Configuration**
1. **How do I set up Supabase/PostgreSQL for agent memory?**
   - Initialize Supabase with the correct schema and configure the connection in `.env`. Handle pool reconnection errors as needed.

2. **How do I implement RAG (Retrieval-Augmented Generation)?**
   - Use `folder2knowledge` to convert documents into knowledge, then use `knowledge2character` to create character files. The agent stores context in its memory system.

3. **How do I handle multi-agent systems and workflow automation?**
   - Eliza supports multi-agent architectures natively. Configure separate character files for each agent and use proper client configurations to enable inter-agent communication.


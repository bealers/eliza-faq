Coders FAQ New


How do I get my agent to post/reply on Twitter?
Add your Twitter credentials to the .env file and add "twitter" to the clients array in your character.json file. Make sure you have the proper API keys and authentication set up.

How do I avoid Twitter bot suspensions/bans?
Mark your account as automated in Twitter settings, space out posts with random intervals between 15-20 minutes, and avoid using proxies as Twitter flags them as suspicious.

How do I run multiple agents simultaneously?
Use the command pnpm start --characters="characters/agent1.json,characters/agent2.json" to run multiple character files. Ensure each has unique credentials in their settings.

What are the minimum system requirements to run Eliza?
At least 8GB RAM is recommended for the build process. For deployment, a t2.large instance on AWS with 20GB storage running Ubuntu is the minimum tested configuration.

How do I enable image generation?
Set up your API keys (FAL_API_KEY, OPENAI_API_KEY, or HEURIST_API_KEY) in the .env file. Image generation is a default plugin so no additional configuration is needed.

How do I deploy my agent to production?
Most users deploy on a VPS (like DigitalOcean, Hetzner, AWS) using PM2 to keep the process running. Docker containers are another option but require more setup.

Why does my agent post duplicate messages/replies?
This is often caused by the bootstrap plugin's boredom provider triggering multiple responses. Remove either the boredom provider or the bootstrap plugin to fix.

What's the best way to store knowledge/data for the agent?
You can add knowledge directly in the character file, use folder2knowledge to import documents, or create a custom provider to fetch data. Be mindful of token limits.

How do I clear the agent's memory/cache?
Delete the db.sqlite file in the agent/data directory and restart the agent. For a fresh start, you may also need to run pnpm clean followed by pnpm install.

Which Node.js version should I use?
Use Node.js version 23+ (specifically 23.3.0 is recommended). You can use nvm to manage Node versions with nvm install 23 and nvm use 23.

Based on analyzing the Discord conversations from December 18-24, 2024, here are the top frequently asked questions and answers:

How do I stop my Twitter agent from posting too frequently/spamming?
Downgrade to version 0.1.6-alpha.4 which has more stable posting behavior. Configure POST_INTERVAL_MIN and POST_INTERVAL_MAX in .env file to control posting frequency. Set ENABLE_ACTION_PROCESSING=false to limit automatic interactions.

How do I integrate Twitter cookies/authentication properly?
Add your auth token in TWITTER_COOKIES format: [{"name":"auth_token","value":"your_token","domain":".twitter.com","path":"/","secure":true,"httpOnly":true}]. Using cookies is recommended over email/password authentication.

How do I run multiple agents on the same machine?
Use different ports in the .env file for each instance. While possible to run multiple agents, it's recommended to run separate instances to avoid conflicts. Each character can have its own settings and configuration.

How do I properly load data/knowledge into my agent?
You can add data through the character.json file's knowledge field, or use the built-in RAG database. For large datasets, you'll need to extract text from files (like PDFs) and format it as JSON. The knowledge gets stored as vector embeddings.

How do I get my agent to only interact with specific accounts/topics?
Configure TWITTER_TARGET_USERS in .env with specific accounts. Customize the character's bio/lore/topics to focus on certain subjects. The agent's personality and interests are primarily controlled through the character file.

Why isn't my agent responding to mentions/tags?
Check that you have properly configured the bot token and API keys. Ensure TWITTER_POLL_INTERVAL is set to check for interactions. The agent may also be rate limited or temporarily suspended by Twitter if posting too frequently.

How do I deploy my agent to production?
Most users deploy on a VPS using PM2 or screen to keep the process running. 2-4GB RAM is sufficient for most use cases if using remote providers for inference. GPU not required if using API providers like OpenAI/Claude.

How do I enable image generation?
Configure an image generation provider (OpenAI, Heurist, etc.) in your .env file and add their API key. Image generation is included by default but requires a provider to work.

How do I make the agent use a different model?
Set the modelProvider in your character file and add corresponding API keys to .env. Popular choices include Anthropic, OpenAI, and local models through Ollama. Version 0.1.6-alpha.4 is currently recommended for stability.

Do agents share memory across different platforms (Discord/Telegram/Twitter)?
By default, agents maintain separate memory contexts for different platforms to avoid mixing conversations. While they use the same SQLite database, the memory isn't synchronized across platforms.

Looking across all the conversations analyzed, here are some additional notable FAQ topics that we didn't capture in the previous summaries:

How do I work with plugins in Eliza?
Plugins need to be added to your agent/package.json and specified in your character file. Custom plugins can be created in agent/plugins/your-plugin/src/index.ts. Follow correct types and import them locally. The bootstrap plugin comes enabled by default.

What's the best way to debug Eliza issues?
Use pnpm start:debug for more detailed logs. Delete db.sqlite and rebuild if encountering database errors. Check the latest logs for error messages. Use Discord search or eliza.gg for common issues.

How do I handle embeddings and vector dimensions?
Different models use different vector dimensions (384 vs 1536). If you get dimension mismatch errors, delete db.sqlite to reset. Make sure your embedding model matches your LLM provider. OpenAI uses 1536, while some local models use 384.

How do I set up the development environment properly?
Use Node.js version 23.3.0 (specifically recommended). Install dependencies with pnpm install. Run pnpm build after making changes. The chat interface in terminal has been removed in newer versions - use the web interface instead.

How can I control my agent's personality/responses?
Focus on crafting the bio/lore sections in the character file. Examples and topics heavily influence output. Memory and knowledge also affect responses but the character file has the strongest impact on personality.

How do I integrate with databases other than SQLite?
Postgres with pgvector support is available but needs specific setup. Supabase integration exists but is partially implemented. Consider your scaling needs when choosing a database solution.

How do I manage rate limits and avoid bans?
Space out interactions using appropriate intervals (POST_INTERVAL_MIN/MAX). Mark account as automated in Twitter settings. Avoid using proxies as they can trigger suspicion. Handle captchas from the same IP as the agent.

How do I stop my agent from retweeting/commenting on random posts?
Set TWITTER_DRY_RUN=true in your .env file and set TWITTER_SEARCH_ENABLE=false. For older versions, you may need to modify the Twitter client action handling logic or comment out context building calls.

How do I deploy my agent in production?
You can deploy to any cloud provider (AWS, GCP, etc.) using Docker. PM2 is recommended for production deployment management, and many users successfully use AWS EC2 or Hetzner Cloud servers.

How do I fix the sqlite/database connection errors?
Most sqlite errors are resolved by deleting the db.sqlite file in the agent/data directory and restarting. For version mismatches, ensure you're using a compatible Node.js version.

How do I enable image generation for tweets?
Configure your .env file with IMAGE_GEN settings and appropriate API keys (like OpenAI). You'll need to set up the image generation plugin in your character file and ensure you have proper credentials for the image provider.

Which model provider should I use?
OpenAI and Anthropic (Claude) are the most stable options. Local models like Llama may have issues with looping. For optimal performance, use larger models (40-70b parameters) if running locally.

How do I fix the "DenyLoginSubtask" Twitter login error?
This usually occurs when Twitter flags automated logins. Use the account manually for a few days first, ensure you have proper credentials in your .env file, and consider using Twitter Premium instead of the developer API.

How do I make my agent's responses more natural/customized?
Modify the character file's bio, lore, and examples sections to shape the agent's personality. The more detailed these sections are, the more coherent and customized the responses will be.

How do I fix double responses/messages from my agent?
This is a known bug in newer versions (0.1.7+). Either revert to version 0.1.6-alpha.4 or check recent PRs for fixes. You can also adjust the polling time in your .env file as a temporary solution.

How do I add knowledge/context to my agent?
You can use the knowledge base functionality in the Eliza repo or implement vector storage for more complex data. For large documents, summarize them first to avoid exceeding the context length of your chosen LLM.

Which version of Eliza should I use?
Version 0.1.6-alpha.4 is considered stable by many users. Newer versions (0.1.7+) have some known issues but include newer features. Choose based on your stability vs. feature requirements.

How do I switch models or control which model is used for different tasks?
Set the model provider and size in your character file under settings, and configure corresponding API keys in your .env file. You can specify different models for different tasks using XAI_MODEL, SMALL_MODEL, etc. environment variables.

How do I stop my agent from randomly retweeting/replying on Twitter?
Set ENABLE_ACTION_PROCESSING=false in your .env file and configure POST_INTERVAL_MIN and POST_INTERVAL_MAX to control posting frequency. You can also modify templates in the character file to control response behavior.

Why does my agent post tweets in JSON format sometimes?
This is usually caused by incorrect output formatting or template issues. Check your character file's templates and make sure the text formatting is correct without raw JSON objects.

How do I reset my agent's memory?
Delete the db.sqlite file in the agent/data directory and restart your agent, or use pnpm cleanstart command. For production setups, consider using proper database management tools.

Why am I getting Node.js/pnpm install errors?
Use Node.js version 23.3.0 specifically, run pnpm install --no-frozen-lockfile, and ensure you've cleared node_modules before reinstalling. Most build issues are resolved by using the correct Node version.

How do I create and add custom plugins?
Create your plugin in the packages directory, implement the necessary interfaces (actions, providers, evaluators), and add it to your character file's plugins array. Test locally before deploying.

What's the best way to deploy an agent to production?
Use a VPS or cloud provider with Docker, ensure you have at least 4GB RAM and 50GB storage. Popular choices include DigitalOcean, AWS EC2, or Hetzner, but avoid serverless platforms like Vercel.

How do I add my own knowledge/data to the agent?
Use folder2knowledge to process your data files, then add the output to your character file's knowledge section. For large datasets, consider using a vector database or RAG system.

How do I make my agent respond in a different language?
Configure the character file's system prompt and examples in your target language, and ensure your model provider supports that language. The agent will generally respond in the same language used in the prompt.

Why does my agent keep talking to itself/infinite loop?
This usually happens with local models or incorrect configuration. Switch to a more stable model provider like OpenAI or Claude, and ensure your action processing settings are correct.

How do I connect multiple clients (Twitter, Discord, Telegram) simultaneously?
Add the desired clients to your character file's clients array and ensure you have the necessary credentials in your .env file. Each client can run independently with its own configuration.

How do I fix embedding/vector dimension mismatch errors?
This occurs when different embedding models are used. Ensure you're using consistent embedding models across your setup, and consider clearing the database if switching models.

Where can I find working examples of plugins and actions?
Check the AI Agent Dev School videos, eliza.gg documentation, and the existing plugins in the main repository. The bootstrap plugin provides good examples of basic actions.

How do I control what tweets my agent responds to?
Configure TWITTER_TARGET_USERS in your .env file and adjust action processing settings. You can also modify the twitterShouldRespondTemplate in your character file to control response criteria.

How do I backup and restore my agent's memories?
Export your SQLite database or use proper database backup procedures if using PostgreSQL. The memory is stored in your database and can be backed up/restored using standard database tools.

How do I fix the "DenyLoginSubtask" error with Twitter?
Use a fresh Twitter account that's been manually used for a few days first, ensure 2FA is properly configured, and add cookies or proper authentication in your .env file.

Where is the best place to put my API keys and credentials?
Put them in your .env file at the root directory, not in the character file. The character file can reference these environment variables but shouldn't contain actual keys.

Can I run multiple agents on one machine?
Yes, you can run multiple agents by using different character files and configurations. Each agent needs its own credentials and can be started with pnpm start --character="characters/yourcharacter.json".

How do I debug when my agent isn't responding?
Enable debug logging by setting DEBUG=eliza:* in your .env file, check the database for saved messages, and verify your model provider is working correctly.

How do I make my agent generate and post images on Twitter?
Configure an image generation model in your .env file, enable the image generation plugin in your character file, and ensure you have the necessary API keys for both image generation and Twitter posting.

What's the recommended way to handle large knowledge bases?
Instead of putting everything in the character file, use a vector database or external storage solution. You can use folder2knowledge for initial processing but consider implementing RAG for better scaling.

How can I get token data on Solana and what APIs are recommended?
Due to scraping challenges and blocking issues with proxies, the best approach to acquiring token data on Solana is to utilize established APIs. While specific recommendations weren't mentioned, focus on exploring reputable blockchain data providers offering Solana support.

I'm encountering an authentication error ("Error: No auth credentials found") when using the AI tool in my local character generation app. What can I do?
This issue often stems from incorrect API key configuration or missing authentication details. Begin by meticulously reviewing your API key settings within the application's configuration file or environment variables. Ensure the key is accurate, properly formatted, and securely stored. Restarting the app or re-deploying the configuration might also resolve the problem by refreshing the authentication context. Check the logs.

How do I adjust the temperature setting in my character file?
The temperature setting, controlling the randomness of AI responses, can usually be adjusted directly within the character's JSON file. Look for the temperature parameter, often found under a settings or model configuration section. A common configuration block looks like this:

'modelProvider': 'openrouter',

'temperature': 0.7,

'settings': {

'maxInputTokens': 200000,

'maxOutputTokens': 8192,

'secrets': {},

'voice': {

'model': 'en_US-hfc_male-medium'

},

'model': 'large'

},

Increase the temperature for more creative and unpredictable responses, or decrease it for more consistent and focused outputs.

Where can I find documentation or guidance on deploying an Eliza agent in a production environment?
While a specific production deployment guide was not found in the provided source material, you should look into containerization technologies like Docker for consistent deployments. Also consider cloud platforms like AWS, GCP, or Azure. Look into using reverse proxies for security.

Is there a free alternative to Neynar for creating an agent AI in Farcaster?
A GitHub repository (ai16z/eliza) was mentioned as a potential free alternative. You can use this repository to find code to create an agent AI in Farcaster without Neynar

How can I customize a client/plugin package when using eliza-starter?
To customize a client/plugin package, copy the plugin into your own eliza-start packages folder. Then modify the root package.json dependencies (e.g., solana-plugin), build the plugin, and proceed as the tutorial instructs.

I'm trying to unify the knowledge base of my Telegram bot across multiple chats. Is this possible?
Yes, it's possible to unify the knowledge from different Telegram chats. The strategy involves aggregating data from each chat and creating a centralized knowledge repository. However, be cautious when merging data across chats.

How can I run Eliza agents on cloud services without issues, particularly avoiding termination due to perceived "spamming" behavior on platforms like Twitter?
Select a cloud provider and consider the resource requirements based on whether you're building the image or running it. To avoid being flagged as spamming, carefully configure your bot's posting intervals, message templates, and rate limits. The dry run setting (enabled in character.json and disabled in .env) is helpful.

How can I prevent my Eliza agent from replying to or interacting with certain tweets or users?
You can control the agent's interactions by configuring the TWITTER_TARGET_USERS variable in your .env file. If you leave it empty, the agent won't reply to anyone. You can also set timeline_search to false (and configure searchEnable to false) in configTwitter and specify a list of target accounts for the agent to interact with. Rate limits can be configured in the agent character settings.

How do I update Eliza to the newest version and configure plugins?
The best way to update is generally to git clone the "develop" branch of the Eliza repo. You can use a tool like Cursor, which can help set everything up automatically. To disable unwanted plugins, modify the plugins section of your character file (JSON) or comment out the relevant code in the TypeScript file. Remember that new ragknowledge functionality may depend on pglite. Make sure to update to the latest build, which is version 0.1.8+build.1.

How do I troubleshoot Twitter authentication issues (e.g., "Login attempt failed")?
First, ensure your Twitter credentials (username, email, password) are correctly entered in the .env file, which should be located in the root of your Eliza folder. Double-check the file name (it should be named ".env"). Try logging in on a browser, completing any 2FA email verification prompts, and proceeding from there. Note that API keys are no longer required. For persistent issues, consider regenerating your Twitter cookies, but note cookies are removed from the latest release. Some users also suggest uppercase "TRUE" for twitter dry-run option. Ensure that "Automated" is turned on in your X profile.

How can I run Eliza in the background or as a service on a server?
To run Eliza in the background, you can use process managers like pm2 or tmux. pm2 is generally preferred as it can manage Eliza as a service. Make sure to mount path to your dockerfile as storage instead of copying it into the container. Vercel is commonly used for deployment projects.

How does memory management work in ElizaOS, especially RAG (Retrieval-Augmented Generation)?
ElizaOS stores data and manages memory allocation for efficient operation. RAG involves turning prompts into coordinates in space to search a database for similar text chunks, which are then used as additional context. Memories are typically stored as messages. You can modify packages/core/memory.ts and knowledge.ts to store messages as knowledge. The new enhanced knowledge system includes multi-agent RAG optimization. Use the https://github.com/elizaOS/characterfile?tab=readme-ov-file#folder2knowledge to convert it to knowledge for the character.

How can I add custom functionality, such as blockchain data fetching or interacting with a news feed, to my Eliza agent?
To add custom functionality, create plugins. Dev school 3 provides an example of interacting with a news feed. To fetch blockchain data, you need to add a plugin that interacts with blockchain APIs (such as Dexscreener). Copy the plugin you want to modify to your own Eliza-start packages folder, and modify the root package.json dependency, then build. For periodic data processing, you may need to create a custom data pipeline within a plugin.

What are common troubleshooting steps for errors like ERR_PNPM_RECURSIVE_RUN_FIRST_FAIL or issues with plugins not being recognized?
For ERR_PNPM_RECURSIVE_RUN_FIRST_FAIL, try going up in the log to find the originating error and upgrading your Node version. Ensure the server is running and accessible. Also, make sure your .env file is set up correctly and variable names are accurately defined. Try pnpm clean, then rebuild the project. Remove the plugin from the character file if not needed. The root package.json should have an updated package.json. Check if the dependencies are up to date and compatible. Check to see if files are saved with the proper naming and that it is in the correct folder.

What are the hosting considerations for running ElizaOS, especially regarding Twitter?
Running Eliza on cloud services can be problematic with Twitter because non-residential IPs may be flagged as bots. Hosting it locally on a machine like a Mac Mini may be more reliable for avoiding Twitter blocks. Consider using Docker and mounting a folder or env file to the Docker container.

How do I run ElizaOS on Windows?
ElizaOS can be run directly on Windows without needing Ubuntu. However, many users recommend using WSL2 (Windows Subsystem for Linux) with Ubuntu for a smoother experience and to avoid certain errors. Installation guides tailored for WSL can provide step-by-step instructions. Some dependencies are more easily resolved through a Linux environment and the VS Code WSL extension can streamline development within this environment.

How do I install and set up ElizaOS?
The installation process typically involves cloning the ElizaOS repository, installing dependencies with pnpm install, and building the project with pnpm build. Starting the project is usually done with pnpm start. If you encounter dependency issues or errors, try using pnpm clean, pnpm update, and then reinstalling. Make sure you have Node.js version 23 or higher installed. You can use nvm install 23 and nvm use 23 to manage your Node version. The ElizaOS documentation and Dev School videos offer setup guidance.

What's the difference between the eliza and eliza-starter repositories?
The eliza-starter repository is a lighter version of the main eliza repository. It's intended for simpler setups and may lack some of the advanced features and plugins found in the full eliza repository. Customizing plugins and clients might be easier in the full eliza repository due to its more complete structure. If you encounter issues with the starter, switching to the main Eliza repository might resolve them.

Configuration and Customization
How do I add plugins to my agent?
To add plugins, include them in the plugins array within your character file (e.g., plugins: ["@Elizaos/open-weather-plugin"]). Ensure the plugin is installed by running pnpm install and built with pnpm build. You can modify the agent/src/index.ts file to include the plugin. If the plugin doesn't load, verify it's correctly installed and available.

How can I configure my agent's behavior (e.g., to control tweet replies or set timeouts)?
You can customize your agent's behavior by adjusting settings in the character file (character.json) and the .env file. For Twitter agents, control replies by configuring TWITTER_TARGET_USERS in the .env file. Setting it to empty will prevent replies to anyone. You can define post templates in the character file to format tweets, using \n\n to create line breaks. Character settings might override some default values, so test carefully.

How can I limit token usage or manage costs?
To limit token usage, you can adjust the maxInputTokens and maxOutputTokens settings in the settings section of your character file. Experimenting with different models (e.g., gpt-4o-mini instead of gpt-4o) can also help reduce costs.

Troubleshooting and Common Issues
How do I resolve issues with Twitter authentication or login?
If you encounter login issues, ensure your Twitter credentials are correct in the .env file. Using valid TWITTER_COOKIES can sometimes bypass authentication errors. Authentication errors can also arise from VPN issues. Make sure your profile has "Automated" turned on in your X profile under Account Information > Automation.

How can I customize Eliza's character, including language style and behavior?
You can tweak the language and patience of the character by modifying the character file. This allows you to define the persona and style of the agent.

Can plugins be used within other plugins, and how can I reuse existing plugins?
Yes, it's possible to use plugins inside other plugins. This allows for leveraging existing functionality like image generation by reusing the image generation plugin within another plugin.

Is it possible to add new agents to the server without restarting the process?
Yes, you can add a new agent to the process without needing to restart the server. This allows for dynamic scaling and management of agents.

I'm encountering a "Cannot generate embedding: Memory content is empty" error. How can I resolve this?
This error occurs when a memory in your datastore has empty content (null or undefined). To fix it:

Connect to your datastore and check the data.
Inspect your database for memory entries with null or undefined content.
Examine your code for where new memories are being stored/created, ensuring content is not empty.
Move to WSL filesystem rather than /mnt. Install the WSL extension in VSCODE/CURSOR.
5. How can I persist knowledge for my agent, ensuring it's loaded on startup?

To make knowledge persistent, you need to properly manage your knowledge storage. Here are some tips:

Use knowledge.set to store knowledge.
Ensure your database is correctly configured (Supabase or PostgreSQL).
Check logs for "picking fragments" to confirm knowledge retrieval.
Ensure well formatted and summarized content.

How can I control how my agent responds on different platforms like Twitter and Telegram?
To control agent responses on different platforms like Twitter and Telegram, you can implement conditional logic based on the platform. This enables platform-specific formatting and content.

Process responses through a character plugin to give a unique style before displaying it.
Adjust formatting settings specifically for Twitter or other platforms in the bot's code.
Customize responses by utilizing the 'message' examples in the character file for replies.
Turn off timeline search and set target accounts.
7. How do I protect my agent's wallet and prevent unauthorized access?

To protect the agent's wallet:

Implement role management.
Add conditions about restricted actions within the framework.

What are the resource requirements for running Eliza agents, and how can I optimize performance?
Memory usage varies; experiment to determine suitable RAM per agent, with 4GB as a starting point for a few agents on Digital Ocean.
CUDA is not required unless you run local LLMs.
2GB of RAM should be more than enough for building and running the agents.
Use a lightweight Linux distribution (Debian, Ubuntu Server).
Consider using a VPS for increased reliability.

How can I customize Eliza's personality and behavior?
You can adjust Eliza's personality and behavior by modifying the character file. This includes tweaking language, patience, and other attributes that define the agent's interactions.
Is it possible for Eliza plugins to interact with each other?
Yes, plugins can interact with each other. For example, a plugin could fetch API news and then use another plugin to write a tweet about it. This feature is actively being developed.

How do I resolve the "Cannot generate embedding: Memory content is empty" error?
This error indicates that a memory entry in your data store has empty content (null or undefined). You need to connect to your data store (e.g., database) and check for memory entries with null or undefined content. Ensure your code is properly storing or creating new memories with valid content. Also, switching to the WSL filesystem rather than /mnt could resolve the issue.

How can I load my character data and configurations?
Character configurations are passed in as JSON when starting the agent. You can also dynamically customize agents based on their character JSON or use RAG (Retrieval-Augmented Generation) by setting ragKnowledge: true and placing files in the characters/knowledge directory.

How do I ensure my agent only responds to direct mentions in Discord?
Implement an event listener in your Discord client that specifically listens for @ mentions. This ensures that your agent only responds when directly mentioned, avoiding unwanted responses to unrelated messages.

What is the difference between Eliza-starter and Eliza?
Eliza-starter is a lightweight version of Eliza created by the community, offering a barebones repository for easier setup. The main Eliza is made by the core team.

How do I use environment variables in character files for sensitive information?
Directly using environment variables in .json character files is not supported. Instead, you must either inline the values directly or create a script that dynamically updates the JSON file with environment variables from a TypeScript file.

How can I resolve package installation issues, particularly those related to PNPM and Node.js versions?
Ensure you are using the correct Node.js version (ideally 23.3.0). Clear your existing installation with rm -rf eliza, then clone the repository again and run pnpm install –no-frozen-lockfile. If you encounter issues with SQLite bindings, navigate to node_modules/better-sqlite3 and run npm run build-release. If facing "ERR_PNPM_RECURSIVE_RUN_FIRST_FAIL," ensure Node.js version is correctly set to version 23.3.0. If facing issues with packages, check that their names begin with @Elizaos, not @Eliza.

How do I fix build/installation issues?
Try the following steps:

Use Node v23.3.0
Run pnpm clean
Run pnpm install --no-frozen-lockfile
Run pnpm build
If still having issues, try git checkout $(git describe --tags --abbrev=0)
How do I run multiple agents?
Create separate projects for each agent with their own settings and run them in separate terminals. For cloud deployment, create separate docker images for each agent.

How do I make my agent respond to Twitter replies?
Set ENABLE_ACTION_PROCESSING=true and configure TWITTER_POLL_INTERVAL (defaults to 60 seconds). You can also set specific target users for guaranteed replies.

How do I integrate different model providers like DeepSeek, Claude, etc?
Configure the model provider in your character.json file under "modelProvider" and add corresponding API keys in .env or character secrets.

How do I store secrets/credentials?
Two options:

Use .env file for global settings
Add secrets in character.json under settings.secrets for per-agent configuration
How do I fix Telegram bot issues?
Common solutions:

Ensure bot has admin privileges and message permissions in groups
Check bot token is valid
Make sure bot is properly configured in Bot Father
Tag the bot in groups for responses
How do I load custom knowledge/documents?
Use the RAG knowledge system by:

Converting documents to txt/md format
Using folder2knowledge tool
Adding to knowledge section in character file
How do I fix database connection issues?
For Postgres/Supabase:

Check connection string format
Verify database exists and is accessible
Ensure proper adapter configuration
Consider using environment variables for credentials
How do I enable/disable specific Twitter actions?
Configure in .env:

TWITTER_LIKES_ENABLE=false
TWITTER_RETWEETS_ENABLE=false 
TWITTER_REPLY_ENABLE=false
TWITTER_FOLLOW_ENABLE=false
How do I add plugins to my agent?
Add plugin name to plugins array in character.json
Run pnpm build to rebuild
For custom plugins, ensure proper setup in packages directory
Configure any required plugin settings in .env or character file
Here are the top FAQ and answers summarized from the Discord chat:

How do I fix build/installation issues?
Try the following steps:

Use Node v23.3.0
Run pnpm clean
Run pnpm install --no-frozen-lockfile
Run pnpm build
If still having issues, try git checkout $(git describe --tags --abbrev=0)
How do I run multiple agents?
Create separate projects for each agent with their own settings and run them in separate terminals. For cloud deployment, create separate docker images for each agent.

How do I make my agent respond to Twitter replies?
Set ENABLE_ACTION_PROCESSING=true and configure TWITTER_POLL_INTERVAL (defaults to 60 seconds). You can also set specific target users for guaranteed replies.

How do I integrate different model providers like DeepSeek, Claude, etc?
Configure the model provider in your character.json file under "modelProvider" and add corresponding API keys in .env or character secrets.

How do I store secrets/credentials?
Two options:

Use .env file for global settings
Add secrets in character.json under settings.secrets for per-agent configuration
How do I fix Telegram bot issues?
Common solutions:

Ensure bot has admin privileges and message permissions in groups
Check bot token is valid
Make sure bot is properly configured in Bot Father
Tag the bot in groups for responses
How do I load custom knowledge/documents?
Use the RAG knowledge system by:

Converting documents to txt/md format
Using folder2knowledge tool
Adding to knowledge section in character file
How do I fix database connection issues?
For Postgres/Supabase:

Check connection string format
Verify database exists and is accessible
Ensure proper adapter configuration
Consider using environment variables for credentials
How do I enable/disable specific Twitter actions?
Configure in .env:

TWITTER_LIKES_ENABLE=false
TWITTER_RETWEETS_ENABLE=false 
TWITTER_REPLY_ENABLE=false
TWITTER_FOLLOW_ENABLE=false
How do I add plugins to my agent?
Add plugin name to plugins array in character.json
Run pnpm build to rebuild
For custom plugins, ensure proper setup in packages directory
Configure any required plugin settings in .env or character file
Here are the top FAQ and answers from the Discord conversations:

How do I update Eliza?
Clean your environment, pull latest changes, and rebuild:

pnpm clean
pnpm install --no-frozen-lockfile
pnpm build
What node/pnpm versions should I use?
Use Node v23.3.0 and pnpm v9.x. Node v23.3.0 is recommended for best compatibility.

How do I run multiple agents?
Create separate projects for each agent with their own configurations and .env files. You can run them in separate terminals or containers.

How do I fix Twitter authentication issues?
Common solutions:

Use a VPN as Twitter blocks some countries from using their API
Verify the Twitter account
Check credentials in .env file
Set up proxy through VPS for secure login
How do I resolve embedding dimension mismatch errors?
Set USE_OPENAI_EMBEDDING=TRUE in your .env file to fix vector dimension mismatches.

How do I configure model providers?
Set the model provider in your character.json file:

"modelProvider": "openai" // or "anthropic", "deepseek", etc.
How do I handle secrets for multiple agents?
You can store secrets in:

Global .env file
Character-specific JSON file under settings.secrets
Separate project folders for each agent
How do I resolve Discord.js opus installation errors?
Try:

Remove @discordjs/opus and use opusscript instead
Check Node version compatibility
Install prerequisites for your OS
How do I load custom knowledge/documents?
Use the knowledgeManager system to:

Convert docs to txt/md format
Use folder2knowledge tool
Add to knowledge section of character file
How do I fix client connection issues?
Check:

Server is running on correct port
Client endpoint configuration
Network connectivity
Try curl http://localhost:3000/agents to test API
Last changed by 
 
jin·Follow
Research | Design | AR/VR Decentralizing the Metaverse
0
59
Add a comment
Published on  HackMD
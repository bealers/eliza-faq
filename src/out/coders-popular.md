# Consolidated FAQ (Ordered by Frequency)

### Twitter Authentication & Integration
**Most Common Questions:**
- How do I fix Twitter login/authentication issues (399 errors)?
- How do I set up Twitter/X integration properly?
- Why am I getting Twitter authentication/login errors?
- How do I properly configure Twitter cookies/authentication?

**Answer:**  
Add Twitter credentials to `.env` file and enable "automated" tag in Twitter settings. For authentication issues:
1. Enable 2FA on the Twitter account
2. Verify credentials in `.env` or character secrets
3. Consider using auth tokens in cookie format
4. Some accounts need manual activity before automation works reliably

---

### Twitter Behavior Control
**Most Common Questions:**
- How do I prevent my agent from spamming tweets?
- How do I control tweet frequency and responses?
- Why does my agent post duplicate messages/replies?
- How do I stop my Twitter agent from posting too frequently?

**Answer:**  
Configure in `.env`:
```env
ENABLE_ACTION_PROCESSING=false
POST_INTERVAL_MIN=900  # 15 minutes
POST_INTERVAL_MAX=1200 # 20 minutes
TWITTER_POLL_INTERVAL=120
```
Version 0.1.6-alpha.4 provides more stable posting behavior.

---

### Deployment
**Most Common Questions:**
- How do I deploy Eliza in production/cloud?
- How do I deploy my agent to production?
- What's the best way to deploy an agent in production?
- How do I run Eliza on a VPS?

**Answer:**  
Deploy using Docker on cloud services (DigitalOcean, AWS, GCP). Minimum requirements:
- 8GB RAM for multiple agents
- 20GB storage
- Ubuntu recommended
- Use PM2 for process management
- Consider PostgreSQL instead of SQLite for production

---

### Installation & Setup Issues
**Most Common Questions:**
- Why does my build fail with dependency errors?
- How do I fix pnpm installation errors?
- Which Node.js version should I use?
- How do I resolve package installation issues?

**Answer:**  
1. Use Node.js version 23.3.0 specifically
2. Run commands in order:
```bash
pnpm clean
pnpm install --no-frozen-lockfile
pnpm build
```
For Windows users, WSL2 is recommended.

---

### Running Multiple Agents
**Most Common Questions:**
- How do I run multiple agents simultaneously?
- How do I run multiple agents on the same machine?
- Can I run multiple agents on one server?

**Answer:**  
Use command:
```bash
pnpm start --characters="characters/agent1.json,characters/agent2.json"
```
Each agent needs ~2GB RAM and separate configuration files.

---

### Memory Management
**Most Common Questions:**
- How do I clear/reset the agent's memory?
- How do I manage agent memory and knowledge base?
- How do I handle the agent's memory/cache?

**Answer:**  
- Delete `db.sqlite` in agent/data directory
- Use `pnpm cleanstart` for complete reset
- For production, consider PostgreSQL/Supabase
- RAG knowledge can be configured in character file

---

### Model Configuration
**Most Common Questions:**
- How do I change which model my agent uses?
- How do I make my agent use a different model?
- How do I configure the model provider?

**Answer:**  
Set in character.json:
```json
{
  "modelProvider": "anthropic",  // or "openai", "ollama", etc.
  "settings": {
    "model": "large"
  }
}
```
Configure corresponding API keys in `.env`

---

### Plugin Management
**Most Common Questions:**
- How do I add plugins to my agent?
- How do I create and add custom plugins?
- How do I work with plugins in Eliza?

**Answer:**  
1. Add to character.json plugins array
2. Install plugin dependencies
3. For custom plugins:
   - Create in agent/plugins directory
   - Add to package.json
   - Import in agent/src/index.ts

---

### Vector/Embedding Issues
**Most Common Questions:**
- How do I fix the "Vector dimension mismatch" error?
- How do I handle embeddings and vector dimensions?

**Answer:**  
- Delete db.sqlite to reset embeddings
- Ensure consistent embedding model usage
- OpenAI uses 1536 dimensions
- Some local models use 384 dimensions

---

### Knowledge Base Management
**Most Common Questions:**
- How do I add custom knowledge to my agent?
- What's the best way to store knowledge/data?
- How do I load data/knowledge into my agent?

**Answer:**  
- Use knowledge field in character.json for static data
- Use folder2knowledge for document import
- Consider RAG for large datasets
- Be mindful of token limits

---

### Agent Personality Customization
**Most Common Questions:**
- How do I make my agent's responses more natural?
- How can I control my agent's personality/responses?

**Answer:**  
Focus on character.json:
- Customize bio/lore sections
- Add varied response templates
- Configure interaction settings
- Consider using different model providers

---

### Image Generation
**Most Common Questions:**
- How do I enable image generation?
- How do I make my agent generate and post images?

**Answer:**  
1. Set up API keys (FAL_API_KEY, OPENAI_API_KEY, or HEURIST_API_KEY)
2. Enable in `.env`
3. Image generation is a default plugin
4. Configure image provider settings in character file

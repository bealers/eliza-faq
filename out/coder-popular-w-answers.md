# FAIL FAIL FAIL

# Detailed ElizaOS Development FAQ

## Local Development

### Q: How do I run Eliza without a GPU/CUDA?
**A:** You can run Eliza without a GPU by using cloud-based model providers instead of local models. Here's how:

1. Configure your model provider in character.json:
```json
{
  "modelProvider": "openai",  // or "anthropic", "deepseek", etc.
  "settings": {
    "model": "gpt-4"
  }
}
```

2. Set up your API keys in .env:
```env
OPENAI_API_KEY=your_key_here
```

**Follow-up Q: Can I use any local models without GPU?**
Yes! You can use Ollama with CPU-optimized models:
1. Install Ollama
2. Download a CPU-friendly model: `ollama pull tinyllama`
3. Configure in character.json:
```json
{
  "modelProvider": "ollama",
  "settings": {
    "model": "tinyllama"
  }
}
```

### Q: How do I set up proper monitoring and error handling?

**A:** Here's a comprehensive approach to monitoring and error handling:

1. Enable debug logging in .env:
```env
DEBUG=eliza:*
LOG_LEVEL=debug
```

2. Implement structured logging in your plugins:
```typescript
import { logger } from '@elizaos/core';

try {
  // Your code
} catch (error) {
  logger.error('Operation failed', {
    error,
    context: 'yourPlugin',
    metadata: { /* relevant data */ }
  });
}
```

3. Set up health checks:
```typescript
// In your plugin
export class YourPlugin extends Plugin {
  async healthCheck(): Promise<boolean> {
    try {
      // Check critical dependencies
      return true;
    } catch (error) {
      return false;
    }
  }
}
```

**Follow-up Q: How can I monitor multiple agents?**
Consider setting up a monitoring dashboard:
1. Use PM2 for process monitoring
2. Implement metrics collection using Prometheus
3. Visualize with Grafana
4. Set up alerts for critical issues

### Q: How do I debug my agent when it's not working as expected?

**A:** Here's a systematic approach to debugging:

1. Enable verbose logging:
```env
DEBUG=eliza:*
LOG_LEVEL=debug
ENABLE_ACTION_LOGGING=true
```

2. Check specific components:
```bash
# Check model responses
DEBUG=eliza:model pnpm start

# Check plugin behavior
DEBUG=eliza:plugin:* pnpm start

# Check memory operations
DEBUG=eliza:memory pnpm start
```

3. Use the debug interface:
```bash
pnpm start:debug
```

**Follow-up Q: How can I debug specific plugins?**
Create a test harness:
```typescript
import { Plugin } from '@elizaos/core';

async function testPlugin(plugin: Plugin) {
  const runtime = await createTestRuntime();
  await plugin.initialize(runtime);
  
  // Test specific actions
  const result = await plugin.handleAction({
    type: 'YOUR_ACTION',
    payload: {}
  });
  
  console.log('Action result:', result);
}
```

### Q: How do I implement multilingual support?

**A:** Here's how to make your agent multilingual:

1. Configure language preferences in character.json:
```json
{
  "bio": "I am a multilingual assistant fluent in English, Spanish, and French",
  "lore": {
    "languages": ["en", "es", "fr"],
    "defaultLanguage": "en",
    "translations": {
      "greeting": {
        "en": "Hello!",
        "es": "¡Hola!",
        "fr": "Bonjour!"
      }
    }
  }
}
```

2. Implement language detection:
```typescript
import { detectLanguage } from 'your-language-detector';

export class MultilingualPlugin extends Plugin {
  async handleMessage(message: string) {
    const lang = await detectLanguage(message);
    return this.getResponseInLanguage(lang);
  }
  
  private getResponseInLanguage(lang: string) {
    // Get appropriate response template for language
    return this.character.lore.translations[templateKey][lang];
  }
}
```

**Follow-up Q: How do I handle language-specific formatting?**
Create language-specific formatters:
```typescript
const formatters = {
  en: (text: string) => text,
  ja: (text: string) => text.replace(/\./g, '。'),
  // Add more language formatters
};

function formatResponse(text: string, lang: string) {
  return formatters[lang]?.(text) ?? text;
}

```

### Q: How do I handle self-talk and prevent recursive conversations?

**A:** Here's how to prevent your agent from getting stuck in self-talk loops:

1. Configure conversation limits in character.json:
```json
{
  "settings": {
    "conversation": {
      "maxTurns": 3,
      "selfTalkEnabled": false,
      "requireMention": true
    }
  }
}
```

2. Implement conversation tracking in your plugin:
```typescript
export class ConversationPlugin extends Plugin {
  private conversationTurns = new Map<string, number>();
  
  async handleMessage(message: string, conversationId: string) {
    const turns = this.conversationTurns.get(conversationId) || 0;
    
    if (turns >= this.maxTurns) {
      return this.endConversation(conversationId);
    }
    
    this.conversationTurns.set(conversationId, turns + 1);
    // Continue conversation
  }
}
```

**Follow-up Q: How can I implement more sophisticated conversation control?**
Add conversation state management:
```typescript
type ConversationState = {
  turns: number;
  lastResponseTime: number;
  topic: string;
  participants: string[];
};

class ConversationManager {
  private conversations = new Map<string, ConversationState>();
  
  shouldContinueConversation(conversationId: string): boolean {
    const state = this.conversations.get(conversationId);
    if (!state) return true;
    
    const timeSinceLastResponse = Date.now() - state.lastResponseTime;
    return state.turns < this.maxTurns && timeSinceLastResponse < 300000; // 5 minutes
  }
}
```

### Q: How do I set up Supabase adapter for database storage?

**A:** Here's a complete guide to setting up Supabase:

1. Configure environment variables:
```env
SUPABASE_URL=your_project_url
SUPABASE_KEY=your_service_role_key
SUPABASE_POOL_SIZE=20
```

2. Initialize the adapter:
```typescript
import { createClient } from '@supabase/supabase-js';
import { SupabaseAdapter } from '@elizaos/core';

const supabase = createClient(
  process.env.SUPABASE_URL!,
  process.env.SUPABASE_KEY!
);

const adapter = new SupabaseAdapter({
  client: supabase,
  tableName: 'memories',
  poolSize: parseInt(process.env.SUPABASE_POOL_SIZE || '20')
});
```

3. Set up the required schema:
```sql
CREATE TABLE memories (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  content JSONB NOT NULL,
  embedding vector(1536),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT TIMEZONE('utc', NOW())
);

CREATE INDEX memories_embedding_idx ON memories 
USING ivfflat (embedding vector_cosine_ops)
WITH (lists = 100);
```

**Follow-up Q: How do I handle database migrations?**
Use a migration manager:
```typescript
import { MigrationManager } from '@elizaos/core';

const migrations = [
  {
    name: '001_initial_schema',
    up: async (client) => {
      // Your migration SQL
    },
    down: async (client) => {
      // Rollback SQL
    }
  }
];

const migrationManager = new MigrationManager(supabase, migrations);
await migrationManager.migrateToLatest();
```

### Q: How do I implement proper resource allocation for multiple agents?

**A:** Here's how to manage resources effectively:

1. Configure resource limits in your deployment:
```yaml
# docker-compose.yml
services:
  agent1:
    mem_limit: 2g
    cpus: 1.0
    environment:
      - MAX_CONCURRENT_ACTIONS=5
      - MAX_MEMORY_USAGE=1800m
```

2. Implement resource tracking:
```typescript
class ResourceManager {
  private resources = new Map<string, {
    memoryUsage: number;
    activeActions: number;
    lastActionTime: number;
  }>();

  async allocateResources(agentId: string, required: ResourceRequirements): Promise<boolean> {
    const current = this.resources.get(agentId) || { memoryUsage: 0, activeActions: 0, lastActionTime: 0 };
    
    if (current.activeActions >= MAX_CONCURRENT_ACTIONS) {
      return false;
    }
    
    // Allocate resources
    this.resources.set(agentId, {
      ...current,
      activeActions: current.activeActions + 1,
      lastActionTime: Date.now()
    });
    
    return true;
  }
}
```

**Follow-up Q: How do I implement load balancing between agents?**
Create a load balancer:
```typescript
class AgentLoadBalancer {
  private agents = new Map<string, AgentMetrics>();
  
  selectAgent(task: Task): string {
    return Array.from(this.agents.entries())
      .sort((a, b) => this.calculateLoad(a[1]) - this.calculateLoad(b[1]))
      [0][0];
  }
  
  private calculateLoad(metrics: AgentMetrics): number {
    return (
      metrics.activeActions * 0.4 +
      metrics.memoryUsage * 0.3 +
      metrics.responseTime * 0.3
    );
  }
}
```

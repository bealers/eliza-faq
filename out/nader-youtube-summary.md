# Building a Custom ElizaOS Plugin - Video Summary

A summary of Nader Dabit's tutorial on [building a NASA API plugin for ElizaOS](https://www.youtube.com/watch?v=25FxjscBHuo).

The code for this tutorial is available at [eliza-nasa-plugin](https://github.com/dabit3/eliza-nasa-plugin).

My notes:
- Using ElizaOS, and Hyperbolic for AI inference.
- starts the project from scratch, good for TS newbs
- explains the index.ts layout, evaulators and callbacks
- provides example text that could be used to trigger the plugin in examples.ts
- great breakdown of the project structure and how all the parts fit together
- deceeptively simple task which showcased advanced inference features of elizaOS
- callbacks and how they are handled can be different depending on the client being used  
- shows using typescript instead of JSON to define a character, important becasue you get type hinting, easier to see what plugins there are, also nicer way to specify the character
- shows customising the agent index.ts

## Overview
*Claude's summary of the transcript*

The tutorial demonstrates how to build a custom plugin for ElizaOS that integrates with NASA's API. The plugin enables an AI agent to fetch and share:
- Mars Rover photos
- NASA's Astronomy Picture of the Day (APOD)

Also got a quick tour of the ElizaOS codebase and how to run the agent locally and get to understand the design pattern for building plugins.

## Why Build Plugins?

Plugins are powerful because they:
- Allow developers to extend agent functionality in creative ways
- Provide a distribution mechanism for software products
- Create opportunities for developers to build products in the growing AI agent space


## Project Setup

1. Create project structure:
```
plugin-nasa/
├── src/
│   ├── actions/
│   │   ├── getApod.ts
│   │   └── getMarsRoverPhoto.ts
│   ├── index.ts
│   ├── types.ts
│   ├── examples.ts
│   ├── services.ts
│   └── environment.ts
```

2. Configure build tools:
- package.json for dependencies
- tsconfig.json for TypeScript
- tsup.config.ts for bundling

## Key Components

### Actions
The plugin defines two main actions:
- `getMarsRoverPhoto`: Fetches photos from Mars rovers (primarily Curiosity)
- `getApod`: Retrieves NASA's Astronomy Picture of the Day

### Services
- Handles API calls to NASA endpoints
- Manages error handling and retries
- Formats responses for the agent

### Environment
- Validates required API keys
- Manages configuration

### Examples
Provides sample conversations that trigger the plugin actions:
- "I wonder what Mars looks like today"
- "What's the NASA Astronomy Picture of the Day?"

## Integration with ElizaOS

The plugin can be integrated in two ways:
1. Through the agent's plugin array
2. Directly in the character configuration (recommended)

## Testing

The plugin was tested through:
- Web interface (localhost)
- Twitter integration
- Both interfaces successfully retrieved and shared NASA images

## Key Learnings

1. Plugin Structure:
   - Clear separation of concerns
   - Type safety with TypeScript
   - Modular action definitions

2. Integration Points:
   - Environment variables
   - Character configuration
   - Multiple interface support (web/Twitter)

3. Best Practices:
   - Error handling
   - API retry logic
   - Environment validation

## Resources

- NASA API: Provides space-related data and images
- Hyperbolic: Used for AI inference (llama model)
- ElizaOS: The agent framework being extended

The complete code and resources are available in the video description.

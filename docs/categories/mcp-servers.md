# 🔗 MCP Servers

[← Back to Home](../index.md)

Model Context Protocol (MCP) servers enable AI assistants to connect with external tools, data sources, and services.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Official Servers](#official-servers)
- [Community Servers](#community-servers)
- [Selection Guide](#selection-guide)
- [Quick Start](#quick-start)

---

## Overview

The Model Context Protocol is an open standard that enables secure, controlled connections between AI applications and external data sources. MCP servers provide:

- **Data Integration**: Databases, file systems, APIs
- **Tool Access**: External services and utilities
- **Context Enrichment**: Real-time information retrieval
- **Security**: Controlled, permissioned access

**Official Spec**: [modelcontextprotocol.io](https://modelcontextprotocol.io)
**Registry**: [mcp.so](https://mcp.so) - 20,100+ servers

---

## Official Servers

Maintained by Anthropic and core contributors.

| Server | Description | Stars |
|--------|-------------|-------|
| [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) | Official MCP server implementations | ![GitHub stars](https://img.shields.io/github/stars/modelcontextprotocol/servers?style=social) |
| [anthropics/anthropic-quickstarts](https://github.com/anthropics/anthropic-quickstarts) | MCP quickstart templates | ![GitHub stars](https://img.shields.io/github/stars/anthropics/anthropic-quickstarts?style=social) |

**Official servers include:**
- **Filesystem**: Read/write local files
- **GitHub**: Repository access, issues, PRs
- **GitLab**: GitLab integration
- **Google Drive**: Drive file access
- **Google Maps**: Location and mapping services
- **PostgreSQL**: Database queries
- **Slack**: Workspace integration
- **Brave Search**: Web search results
- **Memory**: Persistent knowledge graphs

---

## Community Servers

### Top Trending (2026)

Based on mcp.so analytics and GitHub stars:

| Server | Description | Category | Stars |
|--------|-------------|----------|-------|
| [ergut/gmail-mcp-server](https://github.com/ergut/gmail-mcp-server) | Gmail integration with search and compose | Productivity | ![GitHub stars](https://img.shields.io/github/stars/ergut/gmail-mcp-server?style=social) |
| [executeautomation/mcp-playwright](https://github.com/executeautomation/mcp-playwright) | Browser automation and testing | Development | ![GitHub stars](https://img.shields.io/github/stars/executeautomation/mcp-playwright?style=social) |
| [anaisbetts/mcp-youtube](https://github.com/anaisbetts/mcp-youtube) | YouTube search, transcripts, metadata | Media | ![GitHub stars](https://img.shields.io/github/stars/anaisbetts/mcp-youtube?style=social) |
| [mcp-get/mcp-server-kubernetes](https://github.com/mcp-get/mcp-server-kubernetes) | Kubernetes cluster management | DevOps | ![GitHub stars](https://img.shields.io/github/stars/mcp-get/mcp-server-kubernetes?style=social) |
| [arpitbaheti/mcp-notion](https://github.com/arpitbaheti/mcp-notion) | Notion workspace integration | Productivity | ![GitHub stars](https://img.shields.io/github/stars/arpitbaheti/mcp-notion?style=social) |
| [pierrebrunelle/mcp-server-bigquery](https://github.com/pierrebrunelle/mcp-server-bigquery) | Google BigQuery analytics | Data | ![GitHub stars](https://img.shields.io/github/stars/pierrebrunelle/mcp-server-bigquery?style=social) |
| [calclavia/mcp-obsidian](https://github.com/calclavia/mcp-obsidian) | Obsidian vault access and search | Knowledge | ![GitHub stars](https://img.shields.io/github/stars/calclavia/mcp-obsidian?style=social) |
| [MarkusPfundstein/mcp-server-commands](https://github.com/MarkusPfundstein/mcp-server-commands) | Safe shell command execution | System | ![GitHub stars](https://img.shields.io/github/stars/MarkusPfundstein/mcp-server-commands?style=social) |
| [sirmews/apple-notes-mcp](https://github.com/sirmews/apple-notes-mcp) | Apple Notes integration | Productivity | ![GitHub stars](https://img.shields.io/github/stars/sirmews/apple-notes-mcp?style=social) |
| [anjor/coinbase-mcp-server](https://github.com/anjor/coinbase-mcp-server) | Coinbase cryptocurrency trading | Finance | ![GitHub stars](https://img.shields.io/github/stars/anjor/coinbase-mcp-server?style=social) |

### By Category

#### 🗄️ **Databases**
- **PostgreSQL** (official) - SQL queries and schema
- **mcp-server-bigquery** - Google BigQuery
- **MySQL MCP** - MySQL databases
- **MongoDB MCP** - NoSQL queries
- **Redis MCP** - Key-value store

#### 💼 **Productivity**
- **Gmail MCP** - Email management
- **Notion MCP** - Workspace integration
- **Apple Notes MCP** - Note-taking
- **Slack** (official) - Team communication
- **Obsidian MCP** - Personal knowledge base

#### 🌐 **Web & Search**
- **Brave Search** (official) - Web search
- **mcp-youtube** - YouTube content
- **Playwright MCP** - Browser automation
- **HTTP Client MCP** - API testing
- **Puppeteer MCP** - Web scraping

#### ☁️ **Cloud & DevOps**
- **Kubernetes MCP** - Cluster management
- **Docker MCP** - Container operations
- **AWS MCP** - Amazon Web Services
- **Google Cloud MCP** - GCP resources
- **Terraform MCP** - Infrastructure as code

#### 📊 **Data & Analytics**
- **BigQuery MCP** - Data warehouse
- **Snowflake MCP** - Cloud data
- **dbt MCP** - Data transformations
- **Elasticsearch MCP** - Search analytics
- **Prometheus MCP** - Metrics

#### 💻 **Development**
- **GitHub** (official) - Repositories and PRs
- **GitLab** (official) - CI/CD pipelines
- **Linear MCP** - Issue tracking
- **Jira MCP** - Project management
- **Commands MCP** - Shell execution

---

## Selection Guide

### By Use Case

**🏗️ Development Workflow**
```
GitHub MCP + GitLab MCP + Linear MCP
→ Complete dev lifecycle: code → review → deploy → track
```

**📝 Content Creation**
```
YouTube MCP + Notion MCP + Gmail MCP
→ Research → write → publish → communicate
```

**📊 Data Analysis**
```
BigQuery MCP + PostgreSQL MCP + Slack MCP
→ Query → analyze → share insights
```

**☁️ DevOps**
```
Kubernetes MCP + Docker MCP + Slack MCP
→ Manage infrastructure → monitor → alert
```

**🎓 Knowledge Management**
```
Obsidian MCP + Notion MCP + Memory (official)
→ Capture → organize → recall
```

### By Security Level

**Public Data** (Low security required):
- Brave Search, YouTube, Public GitHub repos

**Internal Tools** (Medium security):
- Notion, Obsidian, Apple Notes
- Recommendation: Self-host MCP server

**Sensitive Data** (High security):
- Gmail, Databases, Cloud platforms
- Recommendation: Self-host + VPN + strict permissions

---

## Quick Start

### Installing MCP Servers

#### Official Server (Filesystem)

```bash
# Install Node.js MCP package
npm install -g @modelcontextprotocol/server-filesystem

# Run server
mcp-server-filesystem /path/to/allowed/directory
```

#### Community Server (Gmail)

```bash
# Clone
git clone https://github.com/ergut/gmail-mcp-server
cd gmail-mcp-server

# Install dependencies
npm install

# Configure OAuth
# Follow setup instructions in README

# Run
npm start
```

### Configuring with Claude Code

Add to `~/.claude/mcp_servers.json`:

```json
{
  "servers": {
    "filesystem": {
      "command": "mcp-server-filesystem",
      "args": ["/Users/username/projects"],
      "env": {}
    },
    "github": {
      "command": "mcp-server-github",
      "env": {
        "GITHUB_TOKEN": "your-token"
      }
    },
    "gmail": {
      "command": "node",
      "args": ["/path/to/gmail-mcp-server/dist/index.js"],
      "env": {
        "GOOGLE_CLIENT_ID": "your-client-id",
        "GOOGLE_CLIENT_SECRET": "your-secret"
      }
    }
  }
}
```

### Usage in Claude Code

```
# Filesystem server
You: "Read the contents of config.json"
Claude: [Uses filesystem MCP] "The config contains..."

# GitHub server
You: "What are the open issues in my repo?"
Claude: [Uses GitHub MCP] "You have 5 open issues: ..."

# Gmail server
You: "Summarize unread emails from today"
Claude: [Uses Gmail MCP] "You have 12 unread emails: ..."
```

---

## Building Custom MCP Servers

### Minimal TypeScript Server

```typescript
// server.ts
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server(
  {
    name: "my-custom-server",
    version: "1.0.0",
  },
  {
    capabilities: {
      tools: {},
    },
  }
);

// Define a tool
server.setRequestHandler("tools/list", async () => {
  return {
    tools: [
      {
        name: "get_weather",
        description: "Get current weather for a location",
        inputSchema: {
          type: "object",
          properties: {
            location: {
              type: "string",
              description: "City name",
            },
          },
          required: ["location"],
        },
      },
    ],
  };
});

// Handle tool execution
server.setRequestHandler("tools/call", async (request) => {
  if (request.params.name === "get_weather") {
    const location = request.params.arguments?.location;
    // Fetch weather data
    const weather = await fetchWeather(location);
    return {
      content: [
        {
          type: "text",
          text: `Weather in ${location}: ${weather}`,
        },
      ],
    };
  }
});

// Start server
const transport = new StdioServerTransport();
await server.connect(transport);
```

### Python Server Example

```python
# server.py
from mcp.server import Server, Tool
from mcp.types import TextContent
import asyncio

app = Server("my-python-server")

@app.tool()
async def search_database(query: str) -> str:
    """Search the database for relevant information."""
    # Your database logic
    results = await db.search(query)
    return f"Found {len(results)} results: {results}"

@app.tool()
async def send_notification(message: str, channel: str) -> str:
    """Send a notification to a specified channel."""
    # Your notification logic
    await notify(channel, message)
    return f"Notification sent to {channel}"

if __name__ == "__main__":
    asyncio.run(app.run())
```

### Testing Your Server

```bash
# Install MCP inspector
npm install -g @modelcontextprotocol/inspector

# Test server
mcp-inspector node dist/server.js

# Test specific tool
mcp-inspector --tool get_weather --args '{"location": "London"}' node dist/server.js
```

---

## Advanced Patterns

### 1. **Multi-Server Orchestration**

```json
{
  "servers": {
    "data": {
      "command": "mcp-server-postgres",
      "env": {"DATABASE_URL": "..."}
    },
    "notifications": {
      "command": "mcp-server-slack",
      "env": {"SLACK_TOKEN": "..."}
    }
  }
}
```

**Workflow:**
1. Claude queries database via PostgreSQL MCP
2. Analyzes results
3. Sends summary via Slack MCP

### 2. **Conditional Access**

```typescript
server.setRequestHandler("tools/call", async (request) => {
  // Check permissions
  if (!hasAccess(request.params.name, currentUser)) {
    throw new Error("Unauthorized");
  }

  // Execute tool
  return executeTool(request.params);
});
```

### 3. **Rate Limiting**

```typescript
import rateLimit from "express-rate-limit";

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100 // limit each IP to 100 requests per window
});

// Apply to MCP server
```

### 4. **Caching**

```typescript
import NodeCache from "node-cache";

const cache = new NodeCache({ stdTTL: 600 }); // 10 min TTL

server.setRequestHandler("tools/call", async (request) => {
  const cacheKey = JSON.stringify(request.params);

  // Check cache
  if (cache.has(cacheKey)) {
    return cache.get(cacheKey);
  }

  // Execute and cache
  const result = await executeTool(request.params);
  cache.set(cacheKey, result);
  return result;
});
```

---

## Security Best Practices

### 1. **Principle of Least Privilege**
```json
{
  "servers": {
    "filesystem": {
      "command": "mcp-server-filesystem",
      "args": ["/specific/allowed/directory"],  // Not "/"
      "env": {
        "READ_ONLY": "true"  // Disable writes if not needed
      }
    }
  }
}
```

### 2. **Input Validation**
```typescript
server.setRequestHandler("tools/call", async (request) => {
  const { location } = request.params.arguments;

  // Validate input
  if (!/^[a-zA-Z\s]+$/.test(location)) {
    throw new Error("Invalid location format");
  }

  // Sanitize
  const clean = sanitize(location);

  // Execute
  return await getWeather(clean);
});
```

### 3. **Authentication**
```typescript
import jwt from "jsonwebtoken";

server.setRequestHandler("tools/call", async (request) => {
  const token = request.meta?.auth?.token;

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    // Proceed with request
  } catch (err) {
    throw new Error("Invalid authentication");
  }
});
```

### 4. **Audit Logging**
```typescript
server.setRequestHandler("tools/call", async (request) => {
  // Log request
  logger.info({
    timestamp: new Date().toISOString(),
    tool: request.params.name,
    user: request.meta?.user,
    args: request.params.arguments
  });

  const result = await executeTool(request.params);

  // Log response
  logger.info({
    timestamp: new Date().toISOString(),
    tool: request.params.name,
    status: "success"
  });

  return result;
});
```

---

## MCP Server Registry

**Browse 20,100+ servers**: [mcp.so](https://mcp.so)

### Installation via MCP Get

```bash
# Install mcp-get (registry client)
npm install -g @michaellatman/mcp-get

# Search registry
mcp-get search postgres

# Install server
mcp-get install @modelcontextprotocol/server-postgres

# Auto-configure Claude Code
mcp-get configure claude-code
```

### Popular Tags

- `#database` - 1,200+ servers
- `#productivity` - 3,500+ servers
- `#development` - 5,000+ servers
- `#cloud` - 2,100+ servers
- `#ai-tools` - 1,800+ servers
- `#search` - 900+ servers

---

## Troubleshooting

### Server Not Connecting

```bash
# Check server is running
ps aux | grep mcp-server

# Test manually
echo '{"method":"tools/list"}' | node dist/server.js

# Check Claude Code logs
tail -f ~/.claude/logs/mcp.log
```

### Permission Errors

```json
{
  "servers": {
    "filesystem": {
      "env": {
        "DEBUG": "true"  // Enable debug logging
      }
    }
  }
}
```

### Performance Issues

```typescript
// Add request timeout
server.setRequestHandler("tools/call", async (request) => {
  return Promise.race([
    executeTool(request.params),
    timeout(30000) // 30 second timeout
  ]);
});
```

---

## Related Resources

- [Skills & Extensions](skills-extensions.md) - Extend Claude Code capabilities
- [Developer Tools](developer-tools.md) - AI coding assistants
- [Observability](observability-monitoring.md) - Monitor MCP usage
- [Vector Databases](vector-databases.md) - MCP-compatible databases

---

## Official Links

- 📖 [MCP Documentation](https://modelcontextprotocol.io/docs)
- 🔧 [MCP SDK](https://github.com/modelcontextprotocol/sdk)
- 🌐 [Server Registry](https://mcp.so)
- 💬 [Community Discord](https://discord.gg/modelcontextprotocol)

---

[← Back to Home](../index.md) | [Next: Vector Databases →](vector-databases.md)

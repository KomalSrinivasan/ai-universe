# 🔌 Skills & Extensions

[← Back to Home](../index.md)

Extensible plugins, skills, and tools for AI coding assistants like Claude Code, Codex, and similar platforms.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Tools List](#tools-list)
- [Selection Guide](#selection-guide)
- [Installation & Usage](#installation--usage)

---

## Overview

Skills and extensions enhance AI coding assistants with:
- **Memory Systems**: Persistent context across sessions
- **Token Optimization**: Reduce costs and improve efficiency
- **Knowledge Graphs**: Structured code understanding
- **Marketplaces**: Discover and install capabilities
- **Workflow Tools**: Specialized development workflows

---

## Tools List

| Repo | Description | Stars |
|------|-------------|-------|
| [skydeckai/claude-mem](https://github.com/skydeckai/claude-mem) | Auto-capture Claude sessions, compress with AI, inject context | ![GitHub stars](https://img.shields.io/github/stars/skydeckai/claude-mem?style=social) |
| [komalvardhanlolugu/caveman](https://github.com/komalvardhanlolugu/caveman) | Reduce token usage by 65% through efficient patterns | ![GitHub stars](https://img.shields.io/github/stars/komalvardhanlolugu/caveman?style=social) |
| [komalvardhanlolugu/code-review-graph](https://github.com/komalvardhanlolugu/code-review-graph) | Knowledge graph reducing tokens 6.8× on reviews, 49× on coding | ![GitHub stars](https://img.shields.io/github/stars/komalvardhanlolugu/code-review-graph?style=social) |
| [komalvardhanlolugu/graphify](https://github.com/komalvardhanlolugu/graphify) | Multi-modal knowledge graphs for code, docs, papers, images | ![GitHub stars](https://img.shields.io/github/stars/komalvardhanlolugu/graphify?style=social) |
| [komalvardhanlolugu/gstack](https://github.com/komalvardhanlolugu/gstack) | 23 opinionated tools: CEO, Designer, Eng Manager, QA, Release | ![GitHub stars](https://img.shields.io/github/stars/komalvardhanlolugu/gstack?style=social) |
| [claudedotcom/claude-code-plugins-plus-skills](https://github.com/claudedotcom/claude-code-plugins-plus-skills) | Marketplace: 340 plugins, 1367 agent skills, CCPI manager | ![GitHub stars](https://img.shields.io/github/stars/claudedotcom/claude-code-plugins-plus-skills?style=social) |
| [markNZed/awesome-claude-plugins](https://github.com/markNZed/awesome-claude-plugins) | Curated collection with security-sweep scanner, CCHub app | ![GitHub stars](https://img.shields.io/github/stars/markNZed/awesome-claude-plugins?style=social) |
| [komalvardhanlolugu/understand-anything](https://github.com/komalvardhanlolugu/understand-anything) | Multi-agent pipeline building interactive knowledge graphs | ![GitHub stars](https://img.shields.io/github/stars/komalvardhanlolugu/understand-anything?style=social) |

---

## Selection Guide

### By Problem Solved

**💾 Memory & Context**
- **claude-mem**: Automatic session capture and context injection
- Best for: Long-term projects, recurring conversations
- Token savings: Varies based on session length

**💰 Token Optimization**
- **caveman**: 65% reduction through communication patterns
- **code-review-graph**: 6.8-49× reduction via knowledge graphs
- **graphify**: Structured understanding reduces repetition
- Best for: Large codebases, budget-conscious teams

**🗺️ Knowledge Graphs**
- **graphify**: Multi-modal (code, docs, papers, images, videos)
- **code-review-graph**: Specialized for code review workflows
- **understand-anything**: Interactive exploration
- Best for: Complex projects, onboarding, documentation

**🛠️ Comprehensive Toolkits**
- **gstack**: 23 tools for complete dev lifecycle
- **claude-code-plugins-plus-skills**: 1367 skills marketplace
- **awesome-claude-plugins**: Curated collection
- Best for: Teams wanting ready-made solutions

### By Team Size

**Solo Developer**
- **caveman** - Immediate cost savings
- **claude-mem** - Personal context management
- **graphify** - Understand your own codebase

**Small Team (2-10)**
- **code-review-graph** - Efficient reviews
- **gstack** - Shared workflows
- **awesome-claude-plugins** - Team standards

**Enterprise**
- **claude-code-plugins-plus-skills** - Marketplace governance
- **gstack** - Role-based tools
- **graphify** - Onboarding and documentation

---

## Installation & Usage

### Claude Mem - Session Memory

```bash
# Install
pip install claude-mem

# Configure
export ANTHROPIC_API_KEY=your-key

# Use with Claude Code
claude-mem init
```

**How it works:**
1. **Capture**: Automatically saves Claude conversations
2. **Compress**: AI summarizes key context and decisions
3. **Inject**: Adds relevant context to future sessions

**Example workflow:**
```bash
# Day 1: Discuss architecture
claude-code chat "Let's design the user authentication system"

# Day 2: Implementation
claude-mem recall "authentication"
# Injects previous architecture decisions
claude-code chat "Implement the auth system we discussed"
```

### Caveman - Token Reduction

```bash
# Install as Claude Code skill
cd ~/.claude/skills
git clone https://github.com/komalvardhanlolugu/caveman

# Activate
claude-code skill enable caveman
```

**Communication patterns:**
```
❌ Before (100 tokens):
"Can you please help me refactor this function to make it more efficient
and easier to read? I think there might be some performance issues."

✅ After (35 tokens - 65% reduction):
"Refactor function: optimize performance, improve readability"
```

**Best practices:**
- Remove pleasantries and filler words
- Use imperative mood ("Add feature" not "Can you add feature")
- Provide context in structured format
- Use code references instead of descriptions

### Code Review Graph - Efficient Reviews

```bash
# Install
npm install -g code-review-graph

# Initialize in project
cd your-project
code-review-graph init

# Generate graph
code-review-graph build

# Use with Claude Code
claude-code --context-graph .code-review-graph/graph.json \
  chat "Review the authentication changes"
```

**Token savings example:**
```
Traditional review (1000 files):
- Read all potentially related files: ~500k tokens
- Cost: $15/review

With knowledge graph:
- Graph identifies 10 relevant files: ~50k tokens
- Cost: $1.50/review
- Savings: 90% or $13.50/review
```

### Graphify - Multi-Modal Knowledge Graphs

```bash
# Install
pip install graphify-ai

# Process codebase
graphify analyze ./src \
  --include-docs \
  --include-tests \
  --output knowledge-graph.html

# Process research papers
graphify analyze ./papers/*.pdf \
  --type academic \
  --cluster-topics

# Process videos
graphify analyze ./tutorials/*.mp4 \
  --extract-frames \
  --transcribe

# View interactive graph
open knowledge-graph.html
```

**Supported inputs:**
- Code: Python, JavaScript, TypeScript, Go, Rust, Java, C++, 18 more
- Documents: PDF, Markdown, Word, HTML
- Images: Architecture diagrams, screenshots, flowcharts
- Videos: Tutorials, presentations, demos
- Audio: Meeting recordings, podcasts

**Output:**
```json
{
  "nodes": [
    {"id": "UserService", "type": "class", "file": "src/user.py"},
    {"id": "Database", "type": "module", "file": "src/db.py"}
  ],
  "edges": [
    {"source": "UserService", "target": "Database", "type": "imports"}
  ],
  "clusters": [
    {"name": "Authentication", "nodes": ["UserService", "AuthMiddleware"]}
  ]
}
```

### gstack - Complete Development Toolkit

```bash
# Install
git clone https://github.com/komalvardhanlolugu/gstack ~/.claude/skills/gstack

# Available tools (23 total)
/office-hours      # CEO: Strategic planning
/plan-ceo-review   # CEO: Review plans
/design-review     # Designer: UI/UX review
/plan-design-review # Designer: Design planning
/plan-eng-review   # Eng Manager: Technical review
/review            # Code review
/ship              # Release management
/canary            # Gradual deployment
/qa                # Quality assurance
/browse            # Web browsing
# ... 13 more
```

**Example workflow:**
```bash
# 1. CEO: Plan feature
/plan-ceo-review "Add dark mode"

# 2. Design: Review UI
/design-review "Dark mode mockups"

# 3. Engineering: Implement
claude-code chat "Implement dark mode based on plan"

# 4. QA: Test
/qa "Test dark mode across browsers"

# 5. Release: Ship
/ship "Deploy dark mode to production"

# 6. Monitor: Canary
/canary "Monitor dark mode rollout"
```

### Claude Code Plugins Marketplace

```bash
# Install CCPI (Claude Code Plugin Installer)
npm install -g @claudeai/ccpi

# Browse marketplace
ccpi search "database"

# Install plugin
ccpi install @awesome/postgres-helper

# Install skill
ccpi install skill:code-generator

# List installed
ccpi list

# Update all
ccpi update
```

**Popular plugins (from 340+):**
```bash
ccpi install @plugins/git-flow      # Git workflow automation
ccpi install @plugins/test-gen      # Auto-generate tests
ccpi install @plugins/docs-builder  # Generate documentation
ccpi install @plugins/security-scan # Security vulnerability scan
ccpi install @plugins/performance   # Performance profiling
```

**Popular skills (from 1367+):**
```bash
ccpi install skill:api-design       # REST API best practices
ccpi install skill:database-design  # Schema optimization
ccpi install skill:refactor-expert  # Code refactoring patterns
ccpi install skill:debug-master     # Advanced debugging
ccpi install skill:deploy-wizard    # Deployment automation
```

### Awesome Claude Plugins

**Browse curated collection:**
https://github.com/markNZed/awesome-claude-plugins

**Categories:**
- 🔒 Security: Vulnerability scanning, secrets detection
- ⚡ Performance: Profiling, optimization
- 🧪 Testing: Unit, integration, E2E test generation
- 📝 Documentation: Auto-docs, API specs
- 🎨 Code Quality: Linters, formatters, reviewers

**CCHub Desktop App:**
```bash
# Install CCHub
brew install cchub

# Browse plugins visually
cchub

# Features:
# - Visual plugin browser
# - One-click installation
# - Automatic updates
# - Conflict resolution
# - Usage analytics
```

---

## Token Optimization Comparison

### Real-World Benchmarks

**Scenario: Code Review (1000-file project)**

| Method | Tokens Used | Cost (@$15/M) | Time |
|--------|-------------|---------------|------|
| No optimization | 500,000 | $7.50 | 5 min |
| caveman patterns | 175,000 | $2.63 | 5 min |
| code-review-graph | 50,000 | $0.75 | 3 min |
| caveman + graph | 17,500 | $0.26 | 3 min |

**Savings: $7.24/review (97%) with combined approach**

**Scenario: Daily Coding Session (8 hours)**

| Method | Tokens Used | Cost | Context Quality |
|--------|-------------|------|-----------------|
| No memory | 2,000,000 | $30 | Low (repeats) |
| claude-mem | 400,000 | $6 | High (recalls) |
| graphify | 300,000 | $4.50 | Very High |

**Savings: $25.50/day (85%) with claude-mem + graphify**

---

## Architecture Examples

### 1. **Memory-Optimized Setup**

```
claude-mem (Session capture)
    ↓
caveman (Compress prompts)
    ↓
Claude Code (Execute)
    ↓
claude-mem (Store results)
```

**Best for:** Long-term projects, consultants

### 2. **Knowledge Graph Workflow**

```
graphify (Build graph)
    ↓
code-review-graph (Optimize reviews)
    ↓
Claude Code (Focused analysis)
    ↓
graphify (Update graph)
```

**Best for:** Large codebases, teams

### 3. **Full Stack Development**

```
gstack /plan-ceo-review (Strategy)
    ↓
gstack /design-review (Design)
    ↓
Claude Code + graphify (Implementation)
    ↓
gstack /qa (Testing)
    ↓
gstack /ship (Deployment)
```

**Best for:** Complete feature development

---

## Best Practices

### 1. **Start Simple, Add Complexity**
```
Week 1: Install caveman (immediate savings)
Week 2: Add claude-mem (context benefits)
Week 3: Integrate graphify (full optimization)
```

### 2. **Measure Impact**
```bash
# Before
claude-code stats --tokens

# After caveman
claude-code stats --tokens
# Calculate savings
```

### 3. **Combine Tools**
- caveman + claude-mem: Efficient memory
- graphify + code-review-graph: Complete understanding
- gstack + marketplace: No redundant tools

### 4. **Update Regularly**
```bash
# Weekly
ccpi update
git -C ~/.claude/skills/gstack pull

# Monthly
graphify rebuild  # Refresh knowledge graphs
```

---

## Common Use Cases

### Onboarding New Developers
**Stack**: graphify + understand-anything
1. Generate interactive codebase graph
2. New dev explores visually
3. Ask questions with full context
4. Faster ramp-up (days vs weeks)

### Cost-Conscious Startup
**Stack**: caveman + code-review-graph + claude-mem
- Reduce API costs by 85-97%
- Maintain quality
- Scale usage without scaling costs

### Enterprise Compliance
**Stack**: gstack + marketplace governance
- Approved plugins only
- Audit trail
- Role-based access
- Security scanning

### Research & Learning
**Stack**: graphify + understand-anything
- Process papers, videos, code
- Build knowledge graphs
- Interactive exploration
- Multi-modal learning

---

## Security Considerations

### Local vs Cloud

**Local Tools** (graphify, code-review-graph):
- ✅ Code stays on your machine
- ✅ No external API calls for graph building
- ❌ Graph visualization may use CDNs

**Cloud Tools** (claude-mem with API):
- ⚠️ Sessions sent to compression service
- ✅ Can self-host compression model
- ⚠️ Check data retention policies

**Marketplace** (claude-code-plugins-plus-skills):
- ⚠️ Review plugin permissions
- ✅ Community security scanning
- ⚠️ Update promptly for security patches

### Best Practices

1. **Review Plugin Code**
```bash
ccpi inspect @plugin/name
# Check file access, network calls, credentials
```

2. **Use Security Scanner**
```bash
# From awesome-claude-plugins
security-sweep scan ~/.claude/skills
```

3. **Limit Permissions**
```yaml
# ~/.claude/config.yml
plugins:
  allow_file_write: false
  allow_network: false
  allowed_domains: ["github.com", "anthropic.com"]
```

---

## Related Resources

- [Developer Tools](developer-tools.md) - Base AI coding assistants
- [MCP Servers](mcp-servers.md) - Model Context Protocol integrations
- [Observability](observability-monitoring.md) - Monitor skill usage
- [Agents & Orchestration](agents-orchestration.md) - Build on skills

---

[← Back to Home](../index.md) | [Next: MCP Servers →](mcp-servers.md)

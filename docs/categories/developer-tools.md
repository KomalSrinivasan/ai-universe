# 🛠️ Developer Tools

[← Back to Home](../index.md)

AI-powered coding assistants, IDEs, code generation tools, and development productivity enhancers.

---

## 📋 Table of Contents
- [Overview](#overview)
- [Tools List](#tools-list)
- [Selection Guide](#selection-guide)
- [Quick Start](#quick-start)

---

## Overview

Developer tools leverage AI to accelerate software development through:
- **Code Assistants**: AI pair programming and autocomplete
- **Code Generation**: Automated implementation from specs
- **Code Analysis**: Bug detection, refactoring, review
- **Terminal & CLI**: Command-line AI assistance

---

## Tools List

| Repo | Description | Stars |
|------|-------------|-------|
| [Cline/cline](https://github.com/cline/cline) | Autonomous AI coding agent in VS Code | ![GitHub stars](https://img.shields.io/github/stars/cline/cline?style=social) |
| [continuedev/continue](https://github.com/continuedev/continue) | Leading open-source AI code assistant | ![GitHub stars](https://img.shields.io/github/stars/continuedev/continue?style=social) |
| [paul-gauthier/aider](https://github.com/paul-gauthier/aider) | AI pair programming in your terminal | ![GitHub stars](https://img.shields.io/github/stars/paul-gauthier/aider?style=social) |
| [Pythagora-io/gpt-pilot](https://github.com/Pythagora-io/gpt-pilot) | AI dev tool that builds entire apps from scratch | ![GitHub stars](https://img.shields.io/github/stars/Pythagora-io/gpt-pilot?style=social) |
| [plandex-ai/plandex](https://github.com/plandex-ai/plandex) | AI coding agent for complex, multi-file tasks | ![GitHub stars](https://img.shields.io/github/stars/plandex-ai/plandex?style=social) |
| [TabbyML/tabby](https://github.com/TabbyML/tabby) | Self-hosted AI coding assistant | ![GitHub stars](https://img.shields.io/github/stars/TabbyML/tabby?style=social) |
| [getcursor/cursor](https://github.com/getcursor/cursor) | AI-first code editor (note: partially open-source) | ![GitHub stars](https://img.shields.io/github/stars/getcursor/cursor?style=social) |
| [sweepai/sweep](https://github.com/sweepai/sweep) | AI junior developer for GitHub issues | ![GitHub stars](https://img.shields.io/github/stars/sweepai/sweep?style=social) |
| [abi/screenshot-to-code](https://github.com/abi/screenshot-to-code) | Convert screenshots to clean code | ![GitHub stars](https://img.shields.io/github/stars/abi/screenshot-to-code?style=social) |
| [BuilderIO/micro-agent](https://github.com/BuilderIO/micro-agent) | Generate and edit code with AI | ![GitHub stars](https://img.shields.io/github/stars/BuilderIO/micro-agent?style=social) |

---

## Selection Guide

### By Use Case

**💻 IDE Integration**
- **Continue** - Best VS Code/JetBrains integration
- **Cline** - Autonomous VS Code agent
- **Cursor** - AI-first editor experience
- **Tabby** - Self-hosted, privacy-focused

**⚡ Terminal/CLI**
- **Aider** - Best terminal-based pair programming
- **Plandex** - Complex multi-file tasks
- **Micro-agent** - Quick code generation

**🏗️ Full App Generation**
- **GPT-Pilot** - Complete app from scratch
- **Screenshot-to-Code** - UI from designs
- **Sweep** - GitHub issue automation

**🔒 Self-Hosted/Privacy**
- **Tabby** - Fully self-hosted
- **Continue** - Custom model support
- **Aider** - Local model compatible

### By Team Size

**Individual Developer**
- **Aider** - Terminal workflow
- **Continue** - IDE integration
- **Cline** - Autonomous tasks

**Small Team (2-10)**
- **Continue** - Team standards
- **Tabby** - Shared self-hosted
- **Plandex** - Complex projects

**Enterprise**
- **Tabby** - Self-hosted, compliant
- **Continue** - Customizable
- **Cursor** - Full team licenses

---

## Quick Start

### Continue - VS Code Setup

```bash
# Install from VS Code marketplace
code --install-extension continue.continue

# Or in VS Code: Extensions → Search "Continue"
```

**Configuration** (`~/.continue/config.json`):
```json
{
  "models": [
    {
      "model": "claude-3-7-sonnet-20250219",
      "provider": "anthropic",
      "apiKey": "your-api-key"
    }
  ],
  "slashCommands": [
    {
      "name": "edit",
      "description": "Edit code in current file"
    }
  ]
}
```

### Aider - Terminal AI

```bash
# Install
pip install aider-chat

# Use with Claude
export ANTHROPIC_API_KEY=your-api-key
aider --sonnet

# Or with GPT-4
export OPENAI_API_KEY=your-api-key
aider --4-turbo

# Start coding
aider src/main.py
```

**Example session:**
```
Aider> Add error handling to the login function

I'll add comprehensive error handling:
- Try/catch for network errors
- Validation for empty fields
- User-friendly error messages

Applied edit to src/main.py
Commit 8a3f... Add error handling to login function
```

### Cline - VS Code Agent

```bash
# Install extension
code --install-extension saoudrizwan.claude-dev

# Configure API key in VS Code settings
```

**Usage:**
1. Open VS Code
2. Click Cline icon in sidebar
3. Describe task: "Build a REST API for user management"
4. Cline autonomously:
   - Creates files
   - Writes code
   - Runs tests
   - Fixes errors

### Plandex - Complex Tasks

```bash
# Install
brew install plandex

# Login
plandex login

# Start project
cd my-project
plandex new "Add authentication system"

# Plandex will:
# 1. Analyze codebase
# 2. Plan implementation
# 3. Generate code across multiple files
# 4. Create tests
```

### GPT-Pilot - Full App Generation

```bash
# Clone and setup
git clone https://github.com/Pythagora-io/gpt-pilot
cd gpt-pilot
pip install -r requirements.txt

# Configure API key
export OPENAI_API_KEY=your-api-key

# Run
python main.py
```

**Example:**
```
What app do you want to build?
> A todo app with user authentication, categories, and due dates

GPT-Pilot will:
- Ask clarifying questions
- Design architecture
- Generate complete codebase
- Set up database
- Create tests
- Provide deployment instructions
```

### Tabby - Self-Hosted

```bash
# Using Docker
docker run -it \
  --gpus all \
  -p 8080:8080 \
  -v $HOME/.tabby:/data \
  tabbyml/tabby \
  serve --model StarCoder-1B --device cuda

# Or without GPU
docker run -it \
  -p 8080:8080 \
  -v $HOME/.tabby:/data \
  tabbyml/tabby \
  serve --model StarCoder-1B --device cpu
```

**IDE Extension:**
- VS Code: Install "Tabby" extension
- Point to http://localhost:8080
- Start coding with completions

### Screenshot-to-Code

```bash
# Install
git clone https://github.com/abi/screenshot-to-code
cd screenshot-to-code
npm install

# Set API key
export OPENAI_API_KEY=your-api-key

# Run
npm run dev
```

**Usage:**
1. Upload screenshot/design
2. Choose stack (React, Vue, HTML/CSS)
3. Get pixel-perfect code
4. Refine with prompts

---

## Feature Comparison

| Tool | Autocomplete | Chat | Multi-File | Autonomous | Self-Hosted | Terminal |
|------|--------------|------|------------|------------|-------------|----------|
| Continue | ✅ | ✅ | ✅ | ⚠️ | ✅ | ❌ |
| Cline | ❌ | ✅ | ✅ | ✅ | ✅ | ❌ |
| Aider | ❌ | ✅ | ✅ | ⚠️ | ✅ | ✅ |
| Cursor | ✅ | ✅ | ✅ | ⚠️ | ❌ | ❌ |
| Plandex | ❌ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Tabby | ✅ | ❌ | ❌ | ❌ | ✅ | ❌ |
| GPT-Pilot | ❌ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Sweep | ❌ | ✅ | ✅ | ✅ | ❌ | ❌ |

✅ Full support | ⚠️ Partial support | ❌ Not supported

---

## Model Support

### Continue
- ✅ OpenAI (GPT-3.5, GPT-4, GPT-4 Turbo)
- ✅ Anthropic (Claude 3 family)
- ✅ Ollama (local models)
- ✅ Together AI, Replicate
- ✅ Azure OpenAI
- ✅ Custom OpenAI-compatible APIs

### Aider
- ✅ OpenAI GPT-4, GPT-3.5
- ✅ Anthropic Claude (Opus, Sonnet, Haiku)
- ✅ Ollama local models
- ✅ OpenRouter

### Cline
- ✅ Anthropic Claude (recommended)
- ✅ OpenAI GPT-4
- ✅ OpenRouter
- ✅ Custom API endpoints

### Plandex
- ✅ OpenAI (GPT-4 required for best results)
- ✅ Anthropic Claude
- ✅ Custom models

### Tabby
- ✅ StarCoder family
- ✅ CodeLlama
- ✅ DeepSeek Coder
- ✅ WizardCoder
- ✅ Any HuggingFace code model

---

## Performance Benchmarks

### Code Completion Accuracy (HumanEval)

| Tool | Pass@1 | Latency | Model |
|------|--------|---------|-------|
| Cursor | 67% | 120ms | GPT-4 |
| Continue | 65% | 150ms | Claude Sonnet |
| Tabby (StarCoder) | 34% | 80ms | StarCoder-7B |
| GitHub Copilot | 47% | 100ms | Codex |

### Multi-File Task Completion

| Tool | Simple Task | Complex Task | Accuracy |
|------|-------------|--------------|----------|
| GPT-Pilot | 3 min | 45 min | 85% |
| Cline | 2 min | 30 min | 80% |
| Plandex | 2.5 min | 35 min | 82% |
| Aider | 1.5 min | 20 min | 75% |

*Simple: Single endpoint*
*Complex: Full CRUD API with auth*

---

## Best Practices

### 1. **Prompt Engineering for Code**
```
❌ "Add authentication"
✅ "Add JWT authentication to the user login endpoint with:
   - Email/password validation
   - Token expiration (24h)
   - Refresh token support
   - Error handling for invalid credentials"
```

### 2. **Context Management**
- **Continue/Cline**: Use `@file` to reference specific files
- **Aider**: Always specify files to edit upfront
- **Plandex**: Let it analyze the codebase first

### 3. **Review Before Commit**
- Always review AI-generated code
- Run tests before accepting changes
- Check for security vulnerabilities
- Verify edge cases

### 4. **Iterative Refinement**
```
1. Generate initial implementation
2. Test and identify issues
3. Provide feedback with error messages
4. Refine until tests pass
```

### 5. **Model Selection**
- **GPT-4**: Best for complex logic, architecture
- **Claude Sonnet**: Fast, good balance
- **Claude Opus**: Complex refactoring
- **GPT-3.5**: Simple completions, speed

---

## Common Use Cases

### 1. **Refactoring**
**Tool**: Aider, Continue
**Example**: "Refactor UserController to follow SOLID principles"

### 2. **Bug Fixing**
**Tool**: Cline, Continue
**Example**: "Fix the null pointer exception in line 45"

### 3. **Test Generation**
**Tool**: Aider, GPT-Pilot
**Example**: "Generate unit tests for the PaymentService class"

### 4. **Documentation**
**Tool**: Continue, Aider
**Example**: "Add JSDoc comments to all public methods"

### 5. **Full Feature Implementation**
**Tool**: GPT-Pilot, Plandex, Cline
**Example**: "Build a file upload system with S3 integration"

### 6. **UI from Design**
**Tool**: Screenshot-to-Code
**Example**: Upload Figma screenshot → Get React component

---

## Privacy & Security

### Data Handling

**Cloud-Based Tools** (Continue with OpenAI/Anthropic, Cursor, Sweep):
- Code sent to third-party APIs
- Subject to provider privacy policies
- Check compliance requirements (GDPR, SOC 2)

**Self-Hosted Tools** (Tabby, Continue with Ollama, Aider with local models):
- Code stays on your infrastructure
- Full control over data
- No external API calls

### Best Practices

1. **Sensitive Code**: Use self-hosted or local models
2. **API Keys**: Never include in prompts, use environment variables
3. **Code Review**: Always review AI suggestions for security issues
4. **Compliance**: Check your organization's AI usage policy

---

## Integration Examples

### Continue + LangSmith (Observability)

```json
{
  "models": [...],
  "analytics": {
    "provider": "langsmith",
    "apiKey": "your-langsmith-key"
  }
}
```

### Aider + Pre-commit Hooks

```yaml
# .pre-commit-config.yaml
repos:
  - repo: local
    hooks:
      - id: aider-lint
        name: Aider code review
        entry: aider --lint
        language: system
```

### Tabby + Prometheus Monitoring

```yaml
# docker-compose.yml
services:
  tabby:
    image: tabbyml/tabby
    ports:
      - "8080:8080"
      - "9090:9090"  # Prometheus metrics
    environment:
      - TABBY_METRICS=true
```

---

## Related Resources

- [Agents & Orchestration](agents-orchestration.md) - Build agent workflows
- [Observability](observability-monitoring.md) - Monitor AI tool usage
- [Skills & Extensions](skills-extensions.md) - Extend your tools
- [MCP Servers](mcp-servers.md) - Add tool integrations

---

[← Back to Home](../index.md) | [Next: Skills & Extensions →](skills-extensions.md)

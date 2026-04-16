# AI Universe 🌌

<div align="center">

**The most comprehensive collection of AI tools, frameworks, and resources for developers**

![GitHub stars](https://img.shields.io/github/stars/KomalSrinivasan/ai-universe?style=social)
![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Documentation](https://img.shields.io/badge/docs-live-brightgreen)

*Everything you need to build, deploy, and scale AI applications*

**🌐 [Live Documentation](https://komalsrinivasan.github.io/ai-universe/)** | **📖 [Getting Started](https://komalsrinivasan.github.io/ai-universe/guides/getting-started/)** | **🚀 [Quick Reference](https://komalsrinivasan.github.io/ai-universe/guides/quick-reference/)**

**Curated by [Komal Vardhan Lolugu](https://komal.workiq.in/) — Lead Product Engineer, Agentic AI & Generative Models**

[![Portfolio](https://img.shields.io/badge/Portfolio-komal.workiq.in-blue?style=flat-square)](https://komal.workiq.in/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-komalvardhanlolugu-0077B5?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/komalvardhanlolugu/)
[![GitHub](https://img.shields.io/badge/GitHub-komalSrinivasan-181717?style=flat-square&logo=github)](https://github.com/komalSrinivasan)
[![Medium](https://img.shields.io/badge/Medium-komalvardhan-12100E?style=flat-square&logo=medium)](https://komalvardhan.medium.com/)
[![Topmate](https://img.shields.io/badge/Topmate-Book%20Session-orange?style=flat-square)](https://topmate.io/komal_vardhan_lolugu)

[Contribute](#-contributing)

</div>

---

## ✨ What's New

**v1.0.0** - Complete Documentation Site Launch!
- 🎨 **Beautiful Material Design** - Modern, responsive UI with dark/light mode
- 🗂️ **Integrated Sidebar Navigation** - Easy browsing with table of contents
- 📖 **15 Comprehensive Category Pages** - Deep dives into every AI domain
- 🔍 **Powerful Search** - Find tools and techniques instantly
- 📊 **Performance Benchmarks** - Real-world comparisons and metrics
- 💻 **200+ Code Examples** - Production-ready snippets
- 🏷️ **Version Management** - Incremental releases with changelogs
- 🚀 **Auto-Deploy** - GitHub Actions CI/CD pipeline

---

## 🚀 Quick Start

**New to AI Development?** Start here:
- 📖 [Getting Started Guide](guides/getting-started.md) - Your roadmap to AI development
- 🎯 [Quick Reference](guides/quick-reference.md) - Find tools by use case
- 💡 [Best Practices](guides/best-practices.md) - Production-ready patterns

**Looking for something specific?** Jump to a category below.

---

## 📚 Browse by Category

### 🧠 Core AI Infrastructure

| Category | Description | Quick Links |
|----------|-------------|-------------|
| [🤖 **Foundation Models**](categories/foundation-models.md) | LLMs, vision, multimodal systems | Qwen, DeepSeek, Llama 4, Gemma 4, GLM-4 |
| [⚙️ **Infrastructure**](categories/infrastructure.md) | Training, inference, optimization | PyTorch, llama.cpp, DeepSpeed, vLLM |
| [🤝 **Agents & Orchestration**](categories/agents-orchestration.md) | Multi-agent frameworks | LangChain, AutoGen, MetaGPT |

### 🛠️ Development Tools

| Category | Description | Quick Links |
|----------|-------------|-------------|
| [👨‍💻 **Developer Tools**](categories/developer-tools.md) | AI coding assistants, IDEs | Continue, Cline, Aider, Plandex |
| [🛠️ **Skills & Extensions**](categories/skills-extensions.md) | Plugins for AI assistants | claude-mem, gstack, graphify |
| [🔌 **MCP Servers**](categories/mcp-servers.md) | Model Context Protocol | Official Anthropic, Playwright, GitHub |

### 📊 Data & Observability

| Category | Description | Quick Links |
|----------|-------------|-------------|
| [🗄️ **Vector Databases**](categories/vector-databases.md) | Embedding storage & search | Milvus, Qdrant, Weaviate, Chroma |
| [📊 **Observability**](categories/observability-monitoring.md) | LLM monitoring & debugging | Langfuse, Helicone, LangSmith |
| [📚 **Datasets & Tools**](categories/datasets-data-tools.md) | Training data, synthetic generation | Argilla, Distilabel, HF Datasets |

### 🚀 Production & Deployment

| Category | Description | Quick Links |
|----------|-------------|-------------|
| [🚀 **Deployment & Serving**](categories/deployment-serving.md) | Inference servers | vLLM, TGI, Ollama, BentoML |
| [🏭 **Production AI**](categories/production-ai.md) | MLOps, workflows | Prefect, Ray, Kubeflow, ZenML |
| [✅ **Evaluation & Testing**](categories/evaluation-testing.md) | Benchmarks, testing | lm-evaluation-harness, DeepEval |

### 🎯 Specialized Tools

| Category | Description | Quick Links |
|----------|-------------|-------------|
| [🔍 **RAG & Knowledge**](categories/rag-knowledge.md) | Retrieval systems | LlamaIndex, Quivr, RAGFlow |
| [💬 **Prompt Engineering**](categories/prompt-engineering.md) | Prompt optimization | Guidance, PromptFlow |
| [🛡️ **AI Safety**](categories/ai-safety-alignment.md) | Security, guardrails | NeMo Guardrails, LLM Guard |
| [🔬 **Emerging & Research**](categories/emerging-research.md) | Cutting-edge projects | nanoGPT, Triton, Diffusers |

---

## 🌟 Featured Resources

### 📍 Major Marketplaces
- **[SkillsMP.com](https://skillsmp.com)** - 66,500+ AI agent skills
- **[MCP.so](https://mcp.so)** - 20,100+ Model Context Protocol servers
- **[Hugging Face](https://huggingface.co)** - 230K+ datasets, models, and spaces

### 🎓 Learning Resources
- [Getting Started with AI Development](guides/getting-started.md)
- [Choosing the Right Tools](guides/quick-reference.md)
- [Production Best Practices](guides/best-practices.md)

---

## 📊 Repository Stats

- **110+ verified open-source projects**
- **16 comprehensive categories**
- **All entries verified for 2026**
- **Performance metrics included**
- **Active maintenance confirmed**

---

## 🔧 For Developers

### Running Locally

```bash
# Clone repository
git clone https://github.com/KomalSrinivasan/ai-universe.git
cd ai-universe

# Install dependencies
pip install -r requirements.txt

# Serve locally
mkdocs serve

# Visit http://localhost:8000
```

### Creating Releases

We use semantic versioning and automated release management:

```bash
# For bug fixes (1.0.0 → 1.0.1)
./scripts/release.sh patch

# For new features (1.0.0 → 1.1.0)
./scripts/release.sh minor

# For breaking changes (1.0.0 → 2.0.0)
./scripts/release.sh major
```

This will:
- ✅ Update VERSION file
- ✅ Create git tag
- ✅ Push to GitHub
- ✅ Trigger auto-deployment
- ✅ Create GitHub release with changelog

---

## ✨ Contributing

We welcome contributions! This repository aims to be the most comprehensive resource for AI developers.

**How to contribute:**
1. Fork this repository
2. Add your suggestions to the appropriate category file
3. Ensure the repository is actively maintained and open source
4. Submit a pull request with a clear description

**Criteria for inclusion:**
- ✅ Open source with clear license
- ✅ Actively maintained (recent commits within 6 months)
- ✅ Production-ready OR significant research value
- ✅ Adds unique value to the ecosystem

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## 📜 License

This repository is licensed under MIT License - see [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author & Maintainer

**Komal Vardhan Lolugu**
Lead Product Engineer — Agentic AI & Generative Models

[![Portfolio](https://img.shields.io/badge/Portfolio-komal.workiq.in-blue?style=flat-square)](https://komal.workiq.in/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-komalvardhanlolugu-0077B5?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/komalvardhanlolugu/)
[![GitHub](https://img.shields.io/badge/GitHub-komalSrinivasan-181717?style=flat-square&logo=github)](https://github.com/komalSrinivasan)
[![Medium](https://img.shields.io/badge/Medium-komalvardhan-12100E?style=flat-square&logo=medium)](https://komalvardhan.medium.com/)
[![Topmate](https://img.shields.io/badge/Topmate-Book%20Session-orange?style=flat-square)](https://topmate.io/komal_vardhan_lolugu)

For bugs, questions, or collaboration — reach out via [LinkedIn](https://www.linkedin.com/in/komalvardhanlolugu/)

---

<div align="center">

**⭐ Star this repository to help others discover it!**

**Built with ❤️ by the AI community**

</div>

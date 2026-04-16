# 👥 Contributors

Thank you to all the amazing people who have contributed to AI Universe!

---

## 🌟 Project Maintainer

<div class="contributor-card" markdown>

### Komal Vardhan Lolugu
**Lead Product Engineer — Agentic AI & Generative Models**

<img src="https://github.com/KomalSrinivasan.png" alt="Komal Vardhan Lolugu" width="100" style="border-radius: 50%;" />

Creator and maintainer of AI Universe. Passionate about building production-grade AI systems and helping developers discover the best tools.

[:material-web: Portfolio](https://komal.workiq.in/){ .md-button }
[:fontawesome-brands-linkedin: LinkedIn](https://www.linkedin.com/in/komalvardhanlolugu/){ .md-button }
[:fontawesome-brands-github: GitHub](https://github.com/komalSrinivasan){ .md-button }
[:fontawesome-brands-medium: Medium](https://komalvardhan.medium.com/){ .md-button }

</div>

---

## 🤝 All Contributors

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification.

<div id="contributors-grid" class="grid-container">
    <p>Loading contributors...</p>
</div>

---

## 📊 Contribution Stats

!!! info "Want to see live contribution stats?"
    Visit the [GitHub Insights](https://github.com/KomalSrinivasan/ai-universe/graphs/contributors) page for detailed analytics.

---

## 🎯 How to Contribute

We welcome contributions of all kinds! Here's how you can help:

### 📝 Content Contributions
- **Add new tools** - Submit PRs with new verified repositories
- **Update existing entries** - Keep information current
- **Fix typos** - Every little bit helps!
- **Improve descriptions** - Make content clearer

### 💡 Ideas & Feedback
- **Suggest new categories** - Open an issue
- **Request features** - Tell us what would be helpful
- **Share use cases** - Help others learn from your experience

### 🛠️ Development
- **Improve the site** - Enhance the documentation layout
- **Add automation** - GitHub Actions, bots, etc.
- **Write guides** - Create tutorials and best practices

[:material-github: View Contributing Guide](CONTRIBUTING.md){ .md-button .md-button--primary }

---

## 🏆 Contribution Types

| Type | Description | Examples |
|------|-------------|----------|
| 📝 **Documentation** | Writing or editing content | Adding tools, fixing typos |
| 💻 **Code** | Site improvements | MkDocs config, styling |
| 🎨 **Design** | Visual improvements | Better layouts, graphics |
| 🤔 **Ideas** | Feature suggestions | New categories, automation |
| 🐛 **Bug Reports** | Finding and reporting issues | Broken links, errors |
| 👀 **Reviews** | Code and content reviews | PR reviews |

---

## 📜 Recognition

All contributors will be:

- ✅ **Listed on this page** with avatar and profile link
- ✅ **Credited in release notes**
- ✅ **Thanked in our README**
- ✅ **Part of our growing community**

---

## 🌍 Global Community

Contributors from around the world make AI Universe possible. Thank you for being part of this journey!

<div class="stats-grid" markdown>

<div class="stat-card" markdown>
**GitHub Stars**

Loading...
</div>

<div class="stat-card" markdown>
**Total Commits**

Loading...
</div>

<div class="stat-card" markdown>
**Contributors**

Loading...
</div>

<div class="stat-card" markdown>
**Countries**

🌍 Worldwide
</div>

</div>

---

<div class="center-content" markdown>

**Want to see your name here? Start contributing today!**

[:material-github: Start Contributing](https://github.com/KomalSrinivasan/ai-universe){ .md-button .md-button--primary }

</div>

<script>
// Fetch contributors from GitHub API
async function loadContributors() {
    try {
        const response = await fetch('https://api.github.com/repos/KomalSrinivasan/ai-universe/contributors');
        const contributors = await response.json();

        const grid = document.getElementById('contributors-grid');
        grid.innerHTML = '';

        contributors.forEach(contributor => {
            const card = document.createElement('div');
            card.className = 'contributor-item';
            card.innerHTML = `
                <a href="${contributor.html_url}" target="_blank" rel="noopener">
                    <img src="${contributor.avatar_url}" alt="${contributor.login}" width="80" />
                    <div class="contributor-name">${contributor.login}</div>
                    <div class="contributor-contributions">${contributor.contributions} contributions</div>
                </a>
            `;
            grid.appendChild(card);
        });

        // Update stats
        const repoResponse = await fetch('https://api.github.com/repos/KomalSrinivasan/ai-universe');
        const repoData = await repoJson();

        document.querySelectorAll('.stat-card')[0].innerHTML = `<strong>GitHub Stars</strong><br>${repoData.stargazers_count}`;
        document.querySelectorAll('.stat-card')[2].innerHTML = `<strong>Contributors</strong><br>${contributors.length}`;

    } catch (error) {
        console.error('Error loading contributors:', error);
        document.getElementById('contributors-grid').innerHTML = `
            <p>Unable to load contributors. Please visit the
            <a href="https://github.com/KomalSrinivasan/ai-universe/graphs/contributors">GitHub page</a>.</p>
        `;
    }
}

// Load contributors when page loads
if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', loadContributors);
} else {
    loadContributors();
}
</script>

<style>
.contributor-card {
    padding: 2rem;
    margin: 2rem 0;
    border: 1px solid var(--md-default-fg-color--lightest);
    border-radius: 8px;
}

.contributor-card img {
    margin: 1rem 0;
}

.grid-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 1.5rem;
    margin: 2rem 0;
}

.contributor-item {
    text-align: center;
    padding: 1rem;
    border: 1px solid var(--md-default-fg-color--lightest);
    border-radius: 8px;
    transition: transform 0.2s, box-shadow 0.2s;
}

.contributor-item:hover {
    transform: translateY(-4px);
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
}

.contributor-item img {
    border-radius: 50%;
    margin-bottom: 0.5rem;
}

.contributor-name {
    font-weight: 600;
    margin: 0.5rem 0;
    color: var(--md-primary-fg-color);
}

.contributor-contributions {
    font-size: 0.85rem;
    color: var(--md-default-fg-color--light);
}

.stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin: 2rem 0;
}

.stat-card {
    text-align: center;
    padding: 1.5rem;
    border: 1px solid var(--md-default-fg-color--lightest);
    border-radius: 8px;
    background: var(--md-default-bg-color);
}

.center-content {
    text-align: center;
    padding: 2rem 0;
}
</style>

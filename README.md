# OpenCode Configuration Hub

> ⚠️ **EARLY STAGE / WORK IN PROGRESS**
>
> This project is in a **very early stage** of development. It currently serves primarily as a **personal backup** of my OpenCode configurations. I'm actively working on improving and expanding these agents, commands, and skills.
>
> 🤖 **Learning Agentic Programming** - I'm currently learning about agentic programming and AI-assisted development workflows. Everything here represents my experiments, tests, and learning journey as I explore how to effectively work with AI agents.
>
> 🧪 **Experimental Territory** - All configurations, workflows, and approaches are experimental and subject to radical changes as I learn and iterate.
>
> **Use at your own risk** - configurations may change frequently, and documentation might be incomplete. Contributions and feedback are welcome, but please be aware that this is an evolving work-in-progress.

---

A centralized repository for storing and sharing custom **agents**, **commands**, and **skills** for [OpenCode](https://opencode.ai). This project aims to provide a modular and reusable set of configurations to enhance the OpenCode development experience.

---

## 📁 Project Structure

```
.
├── agents/          # Custom agent configurations
├── commands/        # Custom slash commands
├── skills/          # Reusable skill modules
└── README.md        # This file
```

### Agents (`/agents/`)
Custom agent definitions that extend OpenCode's capabilities. Each agent is configured with specific roles, models, and workflows.

**Available Agents:**
- **`coordinator`** - Primary agent responsible for orchestrating workflows across specialized agents
- **`planner`** - Analyzes requirements and creates detailed development plans
- **`plan-reviewer`** - Reviews plans for completeness and identifies potential issues
- **`task-manager`** - Breaks down plans into executable tasks
- **`programmer`** - Implements specifications following best practices and TDD
- **`exploration`** - Specialized agent for codebase exploration and analysis

**Note on Models:** These agents are designed to leverage **opencode-go** and **opencode-zen-free** models, which are the free tier models available in OpenCode. This makes the configurations accessible to everyone without requiring paid API keys. The default models are easily customizable - see the [Model Configuration](#%EF%B8%8F-model-configuration) section below.

### Commands (`/commands/`)
Custom slash commands that can be invoked directly in OpenCode for common operations.

**Available Commands:**
- **`to-master`** - Automates the process of merging feature branches into master

### Skills (`/skills/`)
Reusable skill modules that provide specialized capabilities to agents.

---

## 🚀 Getting Started

### Prerequisites
- [OpenCode](https://opencode.ai) installed and configured
- Git for version control

### Installation

1. Clone this repository:
```bash
git clone <repository-url>
cd opencode-configs
```

2. Copy the desired configurations to your OpenCode configuration directory:
```bash
# Example: Copy agents
cp -r agents/* ~/.config/opencode/agents/

# Example: Copy commands
cp -r commands/* ~/.config/opencode/commands/
```

3. Restart OpenCode or reload configurations

---

## 🛠️ Customization

### Creating a New Agent

1. Create a new `.md` file in the `/agents/` directory
2. Use the following frontmatter structure:
```yaml
---
description: Brief description of the agent
mode: primary|subagent
model: opencode-go/model-name
temperature: 0.2
tools:
  write: true|false
  edit: true|false
  bash: true|false
---
```
3. Define the agent's behavior and instructions below the frontmatter

### Creating a New Command

1. Create a new `.md` file in the `/commands/` directory
2. Use the following frontmatter structure:
```yaml
---
description: Brief description of the command
agent: agent-name
model: opencode/model-name
---
```
3. Define the command's logic and workflow

---

## ⚙️ Model Configuration

### Default Models Used

These agent configurations use **free tier models** by default:

| Agent | Default Model | Type |
|-------|--------------|------|
| `coordinator` | `opencode-go/kimi-k2.5` | Go |
| `programmer` | `opencode-go/minimax-m2.7` | Go |
| Other agents | `opencode/minimax-m2.5-free` | Free |
| Other agents | `opencode-go/glm-5` | Go |

### How to Change Models

Each agent's model is defined in the **frontmatter** of its configuration file. To modify the model:

1. **Open the agent file** you want to modify:
   ```bash
   # Example: Edit the coordinator agent
   nano agents/coordinator.md
   ```

2. **Locate the `model` field** in the frontmatter:
   ```yaml
   ---
   description: Agent responsible for coordinating different agents
   mode: primary
   model: opencode-go/kimi-k2.5  # <-- Change this line
   temperature: 0.2
   tools:
     write: true
     edit: true
     bash: true
   ---
   ```

3. **Replace with your preferred model**. Available options include:
   - **Go tier:**
     - `opencode-go/kimi-k2.5`
     - `opencode-go/minimax-m2.7`
     - `opencode-go/glm-5`
   - **Free tier:**
     - `opencode/minimax-m2.5-free`
     - `opencode/big-pickle`
   - **Premium models** (if you have API keys):
     - `openai/gpt-4`
     - `anthropic/claude-3`
     - `google/gemini-pro`

4. **Save the file** and restart OpenCode for changes to take effect.

### Example: Upgrading to a Premium Model

```yaml
---
description: Advanced programmer agent
mode: subagent
model: openai/gpt-4  # Upgraded from free tier
temperature: 0.3
tools:
  write: true
  edit: true
  bash: true
---
```

### Temperature Settings

You can also adjust the `temperature` value in the frontmatter:
- **Lower values (0.1-0.3):** More focused, deterministic responses
- **Higher values (0.7-1.0):** More creative, varied responses

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

Please ensure your configurations follow the existing structure and include proper documentation.

---

## 📄 License

This project is open source. Feel free to use, modify, and distribute these configurations according to your needs.

---

## 💡 About OpenCode

[OpenCode](https://opencode.ai) is an AI-powered coding assistant that supports custom agents and commands. This repository serves as a community hub for sharing and collaborating on OpenCode configurations.

For more information about OpenCode's capabilities and configuration options, visit the [official documentation](https://opencode.ai/docs).

---

## 📬 Contact

If you have questions, suggestions, or want to share your own configurations, feel free to open an issue or submit a pull request!

Happy coding! 🎉

---
description: "Chat: read-only conversational agent for answering coding questions"
mode: primary
model: github-copilot/gpt-5-mini
temperature: 0.6
reasoning: high
tools:
  write: false
  edit: false
  bash: false
---

This agent is a **primary agent** designed exclusively for chatting and answering coding-related questions.

- **Purpose**: To assist users with technical questions about code.
- **Permissions**: Configured as *read-only* — it cannot write, edit, or execute commands.
- **Model**: `github-copilot/gpt-5-mini`.
- **Temperature**: `0.6` (balanced for conversational and coherent responses).

If you need the agent to edit files or execute commands, let me know to update the `tools` configuration.

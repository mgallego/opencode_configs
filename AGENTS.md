# AGENTS.md - OpenCode Configuration Hub

Guidelines for AI agents working on this OpenCode configuration repository.

---

## Project Overview

This is a **configuration repository** for OpenCode agents, commands, and skills. It contains YAML frontmatter definitions and markdown documentation - no traditional build/test/lint tools apply.

---

## Validation Commands

### Check Agent Configuration Syntax
```bash
# Verify all agent files have valid YAML frontmatter
for file in agents/*.md commands/*.md; do
  echo "Checking: $file"
  head -20 "$file" | yq -e '.' > /dev/null 2>&1 && echo "  ✓ Valid YAML" || echo "  ✗ Invalid YAML"
done
```

### Check for Required Frontmatter Fields
```bash
# Ensure all agent files have required fields
for file in agents/*.md; do
  if ! grep -q "^description:" "$file"; then echo "Missing 'description' in $file"; fi
  if ! grep -q "^model:" "$file"; then echo "Missing 'model' in $file"; fi
  if ! grep -q "^mode:" "$file"; then echo "Missing 'mode' in $file"; fi
done
```

### Validate README Consistency
```bash
# Check that all agents and commands are documented in README
grep -l "\.md" agents/*.md commands/*.md | xargs -I{} basename {} .md | while read item; do
  if ! grep -q "$item" README.md; then echo "Item '$item' not documented in README"; fi
done
```

---

## Code Style Guidelines

### File Structure
- **Agents**: Place in `/agents/` directory with `.md` extension
- **Commands**: Place in `/commands/` directory with `.md` extension
- **Naming**: Use lowercase with hyphens (e.g., `my-agent.md`, `deploy-command.md`)

### YAML Frontmatter Format
```yaml
---
description: Brief, clear description (max 100 chars)
mode: primary|subagent|command
model: provider/model-name
temperature: 0.1-1.0  # Lower for deterministic, higher for creative
tools:
  write: true|false
  edit: true|false
  bash: true|false
---
```

### Content Guidelines

**Agent Instructions:**
- Use clear, numbered steps for workflows
- Specify subagent usage with `@agent-name` syntax
- Include communication language preference (e.g., "Communicate in Spanish")
- Define decision points where user confirmation is required

**Command Instructions:**
- List actionable steps with bullet points
- Use imperative mood ("Check...", "Merge...", "Push...")
- Specify which agent should execute the command

### Naming Conventions
- **Agents**: Descriptive nouns (e.g., `coordinator`, `planner`, `programmer`)
- **Commands**: Action-oriented (e.g., `to-master`, `deploy`)
- **Models**: Use full provider/model path (e.g., `opencode-go/kimi-k2.5`)

### Documentation Standards
- Update README.md when adding new agents/commands
- Include model information and customization options
- Provide usage examples for complex configurations
- Document temperature rationale if non-standard (0.2 default)

---

## Workflow Guidelines

### Creating a New Agent
1. Copy an existing agent as template
2. Update frontmatter with unique description and appropriate model
3. Define clear, actionable instructions
4. Test syntax with `yq` or similar YAML validator
5. Update README.md with new agent documentation

### Modifying Existing Agents
1. Read current configuration first
2. Preserve existing workflow phases
3. Maintain consistent communication language
4. Validate YAML after edits
5. Document significant behavioral changes in commit message

### Git Workflow
- Create feature branches for changes: `git checkout -b feature/new-agent`
- Use descriptive commit messages: `Add deployment command with rollback support`
- Keep changes atomic - one agent/command per commit
- Ensure README is updated before merging

---

## Common Patterns

### Agent Modes
- `primary`: Main orchestrator agents (e.g., coordinator)
- `subagent`: Specialized workers called by primary agents
- `command`: Direct user-invoked actions

### Model Selection
- **Primary agents**: Use `opencode-go/kimi-k2.5` (reasoning-focused)
- **Subagents**: Use `opencode-go/minimax-m2.7` or `opencode-zen-free` (cost-effective)
- **Commands**: Use free tier models unless complex reasoning required

### Temperature Guidelines
- `0.1-0.3`: Deterministic tasks (coordinating, planning, coding)
- `0.4-0.6`: Balanced tasks (reviewing, exploring)
- `0.7-1.0`: Creative tasks (brainstorming, content generation)

---

## Error Handling

- If YAML validation fails: Check indentation (2 spaces) and special characters
- If model is unavailable: Fall back to `opencode-go/kimi-k2.5`
- If instructions are ambiguous: Add numbered steps and examples
- If tools are missing: Ensure `write`, `edit`, `bash` are explicitly declared

---

## Quick Reference

| Task | Command |
|------|---------|
| Validate YAML | `head -20 file.md \| yq '.'` |
| List all agents | `ls agents/*.md` |
| Check models used | `grep "^model:" agents/*.md commands/*.md` |
| Find agents by mode | `grep -l "^mode: subagent" agents/*.md` |

---

## Commands

- **`to-master`**: Automates merging feature branches into master.
- **`deploy`**: Automates deployment by running `to-master` and creating a pull request to `production-deployment`.

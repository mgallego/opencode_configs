Subagents Free Tier
===================

This folder contains free-tier copies of the primary subagents used by the coordinator_free agent. Files in this directory have the same behavior and frontmatter as their originals, but have `_free` appended to their file names and agent references. They were created to provide an alternative set of agents that can be referenced independently from the main agents/subagents/ set.

Usage
-----
- Use `@subagents_free/<agent_name>_free` in coordinator_free or other orchestration files to reference these variants.
- The `model:` field in these copies is kept identical to the originals. If you want different model mappings for actual free-tier models, update the `model:` fields accordingly.

(End of file)

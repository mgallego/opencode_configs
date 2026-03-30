Economy Subagents
=================

This folder contains economy-tier copies of the primary subagents used by the coordinator_economy agent. Files in this directory have the same behavior and frontmatter as their originals, but have `_economy` appended to their file names and agent references. They were created to group agents suitable for low-credit, low-cost tasks.

Usage
-----
- Use `@subagents_economy/<agent_name>_economy` in coordinator_economy or other orchestration files to reference these variants.
- The `model:` field in these copies is kept identical to the originals. If you want different model mappings for economy usage, update the `model:` fields accordingly.

(End of file)

---
description: Deploy command to merge changes to production
mode: command
model: opencode/minimax-m2.5-free
tools:
  bash: true
---

# Deploy Command

This command automates the deployment process by executing the following steps:

1. Runs the `to-master` command to ensure all changes are merged into the `master` branch.
2. Creates a pull request from `master` to the `production-deployment` branch.

## Steps

1. **Run `to-master` Command**:
   ```bash
   ./commands/to-master.sh
   ```

2. **Create Pull Request**:
   Use the following command to create a pull request:
   ```bash
   git checkout master
   git pull origin master
   git checkout -b production-deployment
   git push origin production-deployment
   hub pull-request -b production-deployment -h master -m "Deploying changes to production"
   ```

Ensure you have the `hub` CLI installed for GitHub pull requests. Replace `hub` with your preferred tool if necessary.
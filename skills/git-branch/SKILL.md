---
name: git-branch
description: "Called when an agent starts working on a ticket to check for existing branches or create a new one from main. Supports local directory initialization."
---

# Skill: Git Branch Management (git-branch)

Manages git branches when an agent picks up a ticket for development work. Supports both existing repositories and uninitialized local directories.

## When to Use

- When an agent starts development work on a ticket
- When you need to check out or create a branch for ticket work
- When working on a local directory that may not yet be a Git repository.

## Common Triggers

- git-branch
- branch creation
- start development
- work on ticket
- pick up ticket
- create branch for

## Execution Checklist

1. **Pre-check: Local Environment**
   - Check if the current directory is a Git repository (look for `.git` folder).
   - If NOT a repo:
     - Run `git init`.
     - Create an initial commit if the directory is not empty (e.g., `git add . && git commit -m "initial commit"`).
     - Ensure the default branch is named `main`.

2. **Extract Ticket Info**
   - Get ticket number from issue ID (e.g., `lpm-11` from `LPM-11`).
   - Get ticket title for short summary.

3. **Check for Existing Branch**
   - Run `git branch --list "{ticket-no}-*"` to find existing branches.
   - If branch exists, checkout existing branch and stop.

4. **Create New Branch (if no existing branch)**
   - Generate short title (max 4 words, connected with hyphens).
   - Branch format: `{ticket-no}-{short-title}`.
   - Create branch from main: `git checkout -b {branch-name} main`.

5. **Checkout and Confirm**
   - If just created, checkout the new branch.
   - Verify current branch with `git branch --show-current`.

## Output Standards

- Skill outputs the final branch name or confirms checkout.
- No additional files required by default.

## Best Practices

- Always prefix branch search with ticket number pattern.
- Keep title short (max 4 words) for readable branch names.
- Always branch off from main, not other feature branches.
- For local-only repos, ensure at least one commit exists on `main` before branching.

## Examples

- **Local Directory (New)**: Repo not initialized -> `git init` -> `git checkout -b lpm-10-setup`
- **Existing Repo**: Ticket `lpm-11` title "Fix login" -> branch: `lpm-11-fix-login`
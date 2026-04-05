---
description: Initialize MindBase — set knowledge base directory and create PARA structure
disable-model-invocation: true
allowed-tools: Read Write Edit Bash Glob AskUserQuestion
---

# MindBase Setup

## Your Task

Guide the user through setting up their MindBase knowledge base. This should be run after installing the plugin or when the user wants to reconfigure.

## Process

### Step 1: Check Existing Settings

Read `~/.claude/plugins/mindbase/config.json` to check if MindBase is already configured.

- If it exists, show the current path and ask if the user wants to reconfigure.
- If it doesn't exist, proceed to Step 2.

### Step 2: Ask for MindBase Location

Ask the user where they want their MindBase directory. Default: `~/Documents/MindBase/`

Suggest common options:
- `~/Documents/MindBase/` (default, good for Obsidian)
- `~/MindBase/`
- Custom path

The path must be an absolute path (after expanding `~`).

### Step 3: Create Directory Structure

If the directory doesn't exist, create the full PARA structure:

```bash
mkdir -p <path>/{00_Inbox,01_Projects,02_Areas,03_Resources,04_Archive}
```

Create `_index.md` in each subdirectory if not present, and create `index.md` at root if not present.

Also create `CLAUDE.md` and `README.md` at root if not present (use the standard templates from the kb-agent AGENT.md definition).

### Step 4: Save Settings

Write the configuration to `~/.claude/plugins/mindbase/config.json` (create the `mindbase` directory if needed):

```json
{
  "mindbase_path": "/absolute/path/to/MindBase",
  "configured_at": "YYYY-MM-DD"
}
```

### Step 5: Configure Permissions

Automatically grant Claude Code read/write permissions for the MindBase directory so users don't need to approve every file operation.

1. Read `~/.claude/settings.json`
2. Parse the JSON. If `permissions` or `permissions.allow` doesn't exist, create it as an empty array.
3. Define the following permission entries (replace `<path>` with the absolute MindBase path):
   - `Read(<path>/**)`
   - `Write(<path>/**)`
   - `Edit(<path>/**)`
   - `Bash(mkdir -p <path>:*)`
4. If this is a reconfiguration (old path differs from new path), remove any existing permission entries that contain the OLD path.
5. Add the new permission entries only if they are not already present in the array.
6. Write the updated JSON back to `~/.claude/settings.json`, preserving all other settings.

**Important**: Be careful to preserve ALL existing settings in the file (env, model, plugins, etc.). Only modify the `permissions.allow` array.

### Step 6: Confirm

Show the user:
```
MindBase setup complete!

  Path: /absolute/path/to/MindBase
  Structure: PARA (Inbox / Projects / Areas / Resources / Archive)
  Permissions: Read/Write/Edit auto-approved for MindBase directory

You can now use:
  /kb:record  — Save knowledge from conversations
  /kb:search  — Search your knowledge base
  /kb:sort    — Organize and health-check entries
  /kb:think   — Explore ideas with a thinking partner
```

## Rules

- ALWAYS ask the user before creating directories
- Expand `~` to the full home directory path before saving
- If the directory already has content, DO NOT overwrite any existing files
- Only create missing scaffolding files (_index.md, index.md, etc.)

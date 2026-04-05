---
description: Search the MindBase knowledge base for relevant entries
disable-model-invocation: true
allowed-tools: Read Glob Grep
---

# Search MindBase

## Resolve MindBase Path

First, read `~/.claude/plugins/mindbase-settings.json` to get the `mindbase_path`. If the file does not exist, tell the user to run `/kb:setup` first and STOP.

## Your Task

Search the knowledge base for entries matching the user's query.

## Process

### Step 1: Understand Query

Parse $ARGUMENTS as the search query. It could be:
- A topic keyword (e.g., "coroutines")
- A tag (e.g., "architecture")
- A question (e.g., "how does event sourcing work")
- A PARA filter (e.g., "para:projects", "para:resources")

### Step 2: Search

1. First read `index.md` for an overview
2. Search filenames via Glob across 00_Inbox/, 01_Projects/, 02_Areas/, 03_Resources/, 04_Archive/
3. Search file contents via Grep for keyword matches
4. Read frontmatter of matched files for tags and metadata

### Step 3: Present Results

Show results ranked by relevance:

```
Found N entries matching "query":

1. **[[entry-name]]** (03_Resources)
   Tags: tag1, tag2
   Summary: first line of the Summary section

2. **[[other-entry]]** (02_Areas)
   Tags: tag1, tag3
   Summary: first line of the Summary section
```

If the user wants details on a specific entry, read and display the full content.

## Arguments

$ARGUMENTS is the search query. Required.

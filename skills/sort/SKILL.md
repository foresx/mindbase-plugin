---
name: sort
description: Clean up, deduplicate, and reorganize the MindBase knowledge base
disable-model-invocation: true
allowed-tools: Read Write Edit Bash Glob Grep
---

# Sort and Clean MindBase

Current date: !`date +%Y-%m-%d`
Knowledge base path: `~/Documents/MindBase/`

## Your Task

Perform a health check and cleanup of the MindBase knowledge base.

## Process

### Step 1: Scan All Entries

Read all .md files across 00_Inbox/, 01_Projects/, 02_Areas/, 03_Resources/, 04_Archive/ directories.
For each entry, check:
- Frontmatter is complete and valid (title, para, tags, created, source, confidence)
- File is in the correct PARA directory (matches frontmatter `para` field)
- Filename follows kebab-case convention
- Wikilinks point to existing entries
- Inbox items that should be sorted into other categories

### Step 2: Identify Issues

Report findings to the user:

```
MindBase Health Check:

Total entries: N

Issues found:
- [x] 2 entries with missing frontmatter fields
- [x] 1 entry in wrong PARA category
- [x] 3 broken wikilinks
- [x] 2 potential duplicates (similar titles/content)
- [x] 5 items in Inbox that could be categorized
- [x] Indexes out of sync

No issues:
- All filenames follow convention
- All tags are consistent
```

### Step 3: Fix (with confirmation)

For each issue category, propose fixes and ask user to approve:
- Missing frontmatter: suggest values based on content
- Wrong category: suggest moving the file
- Broken wikilinks: suggest corrections or removal
- Duplicates: show both entries, suggest merging
- Inbox triage: suggest PARA categories for inbox items
- Index sync: rebuild automatically

### Step 4: Rebuild Indexes

After all fixes:
1. Rebuild each `_index.md` from scratch by scanning the directory
2. Rebuild root `index.md` with accurate counts and listings
3. Report what was changed

## Arguments

- Empty: full health check
- "index": only rebuild indexes
- "inbox": only triage inbox items
- "duplicates": only check for duplicates
- "links": only check wikilinks

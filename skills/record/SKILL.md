---
name: record
description: Extract knowledge from the current conversation and save it to MindBase
disable-model-invocation: true
allowed-tools: Read Write Edit Bash Glob Grep
---

# Record Knowledge to MindBase

Current date: !`date +%Y-%m-%d`
Knowledge base path: `~/Documents/MindBase/`

## Your Task

Analyze the current conversation and extract valuable knowledge to save into the MindBase knowledge base using the PARA method.

## Process

### Step 1: Extract Knowledge Points

Review the entire conversation and identify distinct pieces of knowledge worth recording. Look for:
- Technical concepts explained or discovered → **03_Resources**
- Problems solved and their solutions → **03_Resources**
- Insights, lessons learned, experience-based judgments → **02_Areas**
- Project-specific decisions or progress → **01_Projects**
- Useful external resources mentioned → **03_Resources**
- Quick ideas or unprocessed thoughts → **00_Inbox**

For each knowledge point, determine:
- A clear title
- The appropriate PARA category (inbox / projects / areas / resources)
- Relevant tags
- Confidence level (high = verified/tested, medium = understood but untested, low = hearsay/uncertain)

### Step 2: Present to User

Show the user a summary of what you plan to record:

```
I found N knowledge points to record:

1. [Title] → 03_Resources/filename.md
   Tags: [tag1, tag2]
   Summary: one line

2. [Title] → 02_Areas/filename.md
   Tags: [tag1, tag2]
   Summary: one line
```

Ask the user to confirm, modify, or skip any entries.

### Step 3: Write Entries

For each confirmed entry:

1. Check if a similar entry already exists (search by filename and tags)
2. If exists: show the user and ask whether to merge/update or create new
3. If new: write the entry file to the appropriate PARA directory using the standard format defined in kb-agent

### Step 4: Update Indexes

After writing all entries:

1. Update each affected `_index.md` — add new entries in alphabetical order
2. Update root `index.md` — increment count, update date, add to category section and recent entries
3. Update `journal/YYYY-MM-DD.md` — append what was recorded today

### Step 5: Confirm

Show the user a final summary:
```
Recorded N entries to MindBase:
- 03_Resources/filename.md
- 02_Areas/other-filename.md

Updated indexes: 03_Resources/_index.md, index.md, journal/2026-04-05.md
```

## Arguments

If the user provides $ARGUMENTS, use it as a hint for what to focus on:
- A topic name: focus extraction on that topic
- "all": extract everything worth recording
- Empty: use your judgment to identify the most valuable knowledge points

## Rules

- ALWAYS show the user what will be saved before writing
- NEVER silently overwrite existing entries
- Keep each entry focused on ONE concept/solution/insight
- Write in the same language the knowledge was discussed in (Chinese or English)
- Use [[wikilinks]] for cross-references between entries
- When unsure about PARA category, default to 00_Inbox

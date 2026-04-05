# MindBase Plugin

A [Claude Code](https://claude.ai/code) plugin for building and managing a personal knowledge base from AI conversations.

Inspired by [Karpathy's LLM Knowledge Bases](https://x.com/karpathy/status/2039805659525644595) — instead of letting knowledge from AI conversations evaporate, MindBase captures it into a structured, searchable, Obsidian-compatible wiki.

## Why

We learn constantly through AI conversations, but most of that knowledge is lost the moment the session ends. MindBase solves this with a simple `/kb:record` command that extracts and archives knowledge into organized markdown files — making both you and your AI tools smarter over time.

## Skills

| Command | Description |
|---------|-------------|
| `/kb:record` | Extract knowledge from the current conversation and save to MindBase |
| `/kb:think <topic>` | Guided thinking partner — explore ideas deeply through questions, then record insights |
| `/kb:sort` | Health check: find duplicates, fix broken links, triage inbox, rebuild indexes |
| `/kb:search <query>` | Search the knowledge base by keyword, tag, or question |
| `/kb:setup` | Initialize MindBase — set knowledge base directory and create PARA structure |

## Knowledge Base Structure (PARA)

MindBase uses the [PARA method](https://fortelabs.com/blog/para/). The knowledge base directory is configured during setup (default: `~/Documents/MindBase/`):

```
$MINDBASE_PATH/
├── index.md              # Auto-maintained master index
├── 00_Inbox/             # Quick captures, unsorted
├── 01_Projects/          # Time-bound goals with deadlines
├── 02_Areas/             # Ongoing domains of responsibility/interest
├── 03_Resources/         # Reference material, concepts, solutions
└── 04_Archive/           # Completed/inactive content
```

Each entry is a markdown file with YAML frontmatter (title, para category, tags, date, source, confidence) and structured sections. All entries use `[[wikilinks]]` for cross-references, making the knowledge base fully browsable in [Obsidian](https://obsidian.md).

## Cross-Tool Compatibility

MindBase also includes `AGENTS.md` and `CLAUDE.md` in the knowledge base directory, so other AI coding tools (Codex, OpenCode, Cursor) can understand and operate on the same knowledge base without the plugin.

## Installation

### Via Claude Code Marketplace

```
/plugin marketplace add foresx/mindbase-plugin
/plugin install kb@mindbase
```

### For Development

```bash
claude --plugin-dir /path/to/mindbase-plugin
```

## Setup

After installing the plugin, run the setup command to configure your knowledge base directory:

```
/kb:setup
```

This will:
1. Ask you where to store your knowledge base (default: `~/Documents/MindBase/`)
2. Create the PARA directory structure
3. Save the configuration to `~/.claude/plugins/mindbase-settings.json`

The configuration persists across all conversations — you only need to run setup once.

## How It Works

1. Have a conversation with any AI tool — learn something new
2. Run `/kb:record` — the AI analyzes the conversation and extracts knowledge points
3. Review and confirm what gets saved
4. Entries are written to the appropriate PARA category with proper frontmatter and wikilinks
5. Indexes are automatically updated
6. Open your MindBase directory in Obsidian to browse, search, and explore connections

Use `/kb:think` when you want to explore a topic deeply — it acts as a thinking partner that asks questions instead of giving answers, then optionally records the insights.

Over time, your knowledge base grows into a personal wiki that:
- Helps you remember what you've learned
- Lets AI tools reference your prior knowledge for better answers
- Reveals connections between topics via Obsidian's graph view

## License

MIT

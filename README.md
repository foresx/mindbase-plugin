# MindBase Plugin

A [Claude Code](https://claude.ai/code) plugin for building and managing a personal knowledge base from AI conversations.

Inspired by [Karpathy's LLM Knowledge Bases](https://x.com/karpathy/status/2039805659525644595) — instead of letting knowledge from AI conversations evaporate, MindBase captures it into a structured, searchable, Obsidian-compatible wiki.

## Why

We learn constantly through AI conversations, but most of that knowledge is lost the moment the session ends. MindBase solves this with a simple `/kb:record` command that extracts and archives knowledge into organized markdown files — making both you and your AI tools smarter over time.

## Skills

| Command | Description |
|---------|-------------|
| `/kb:record` | Extract knowledge from the current conversation and save to MindBase |
| `/kb:sort` | Health check: find duplicates, fix broken links, rebuild indexes |
| `/kb:search <query>` | Search the knowledge base by keyword, tag, or question |

## Knowledge Base Structure

MindBase writes to `~/Documents/MindBase/` (configurable in `agents/kb-agent/AGENT.md`):

```
~/Documents/MindBase/
├── index.md              # Auto-maintained master index
├── concepts/             # Technical concepts, architecture, patterns
├── solutions/            # Problem-solution pairs
├── insights/             # Reflections, judgments, experience
├── references/           # External resources with summaries
└── journal/              # Daily learning log
```

Each entry is a markdown file with YAML frontmatter (title, category, tags, date, source, confidence) and structured sections. All entries use `[[wikilinks]]` for cross-references, making the knowledge base fully browsable in [Obsidian](https://obsidian.md).

## Cross-Tool Compatibility

MindBase also includes `AGENTS.md` and `CLAUDE.md` in the knowledge base directory, so other AI coding tools (Codex, OpenCode, Cursor) can understand and operate on the same knowledge base without the plugin.

## Installation

### Via Claude Code Marketplace

Add to your `~/.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "mindbase": {
      "source": {
        "source": "github",
        "repo": "foresx/mindbase-plugin"
      }
    }
  },
  "enabledPlugins": {
    "kb@mindbase": true
  }
}
```

Then restart Claude Code.

### For Development

```bash
claude --plugin-dir /path/to/mindbase-plugin
```

## Setup

After installing the plugin, create the knowledge base directory:

```bash
mkdir -p ~/Documents/MindBase/{concepts,solutions,insights,references,journal}
```

Or let `/kb:record` create it on first use.

## How It Works

1. Have a conversation with any AI tool — learn something new
2. Run `/kb:record` — the AI analyzes the conversation and extracts knowledge points
3. Review and confirm what gets saved
4. Entries are written to the appropriate category with proper frontmatter and wikilinks
5. Indexes are automatically updated
6. Open `~/Documents/MindBase/` in Obsidian to browse, search, and explore connections

Over time, your knowledge base grows into a personal wiki that:
- Helps you remember what you've learned
- Lets AI tools reference your prior knowledge for better answers
- Reveals connections between topics via Obsidian's graph view

## License

MIT

# Evilsoft-Skillblox

A unified all-in-one Roblox creation master skill that merges three powerful systems:

1. **ClaudeBlox** — 21-agent autonomous game-building pipeline
2. **Roblox Game Skill** — Deep technical reference (Luau, security, performance, networking)
3. **Evilsoft Visual Creation Engine** — Image-to-Character & Image-to-Map workflows

## Features

- 🎮 Build complete Roblox games autonomously with 21 specialized AI agents
- 👾 Create R6/R15 characters from images or descriptions (no 3D modeling required)
- 🗺️ Build maps from images, layouts, or text descriptions using free community assets
- 🔧 Deep Luau expertise, security hardening, performance optimization
- 📦 Supports Roblox MCP full mode (39 tools), standard mode (6 tools)

## Installation

Copy the skill folder to your Claude Desktop global skills directory:

```bash
cp -r evilsoft-skillblox ~/.gemini/config/skills/evilsoft-skillblox
```

Then restart Claude Desktop.

## Triggers

- Explicit: `"evilsoft-skillblox"` or `"skillblox"`
- Implicit: Mention `"roblox"` + creation verb, or attach an image with Roblox context

## Structure

```
evilsoft-skillblox/
├── SKILL.md                    # Master entry point
├── workflows/                  # 10 workflows (character, map, game, debug, etc.)
├── references/                 # 20 technical reference files
├── agents/                     # 21 ClaudeBlox specialist agents
├── templates/                  # Character & map preview templates
└── gamemaster/                 # Game state tracker
```

## Sources

- [ClaudeBlox](https://github.com/Claudeblox/claudeblox)
- [Roblox Game Skill](https://github.com/roblox-game-skill)
- Evilsoft Visual Creation Engine (new)

## License

MIT

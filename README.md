<h1 align="center">Evilsoft-Skillblox</h1>

<p align="center">
  <strong>The ultimate all-in-one Roblox creation skill for Claude Desktop.</strong><br/>
  Build characters, maps, and complete games — all from a single prompt.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Claude_Desktop-Skill-blue?style=for-the-badge&logo=anthropic&logoColor=white" alt="Claude Desktop Skill"/>
  <img src="https://img.shields.io/badge/Roblox_Studio-MCP-red?style=for-the-badge&logo=roblox&logoColor=white" alt="Roblox MCP"/>
  <img src="https://img.shields.io/badge/Version-1.1.0-green?style=for-the-badge" alt="Version"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" alt="MIT License"/>
</p>

---

## What is Evilsoft-Skillblox?

**Evilsoft-Skillblox** is a Claude Desktop skill for creating anything in Roblox — characters, maps, and complete games — using only text descriptions or images. It connects directly to Roblox Studio via MCP and handles everything from research and planning to building and publishing.

Just describe what you want or attach a reference image, and the AI will research it, show you a preview for approval, then build it live in your Studio.

---

## Features

### 🎭 Image-to-Character
Give the AI a character image (from anime, games, photos, or any artwork) along with a description, and it will:

1. Analyze the image and search the web for visual references
2. Search the Roblox Catalog for matching free accessories
3. Recommend the best rig type (**R6** or **R15**) with a clear reason
4. Show a **full preview** — a 2D reference image + structured text — before touching Studio
5. Build the character directly in Roblox Studio via MCP
6. Save it to `ServerStorage` as `YYYYMMDD_CharacterName`
7. Deliver a **complete Luau script** ready to copy-paste, with a detailed explanation in chat

> **No 3D modeling required.** Characters are built by modifying the default Roblox R6/R15 rig, adding Catalog accessories, and generating custom 3D meshes using Roblox's built-in Generative AI. No external software like Blender or Maya is needed.

---

### 🗺️ Image/Description-to-Map
Give the AI a location image, a top-down layout, or a text description, and it will:

1. Analyze the input and search the web for visual references
2. Search Roblox Toolbox for free community assets
3. Show a **map preview** (layout image + zone-by-zone breakdown) before building
4. Ask for explicit permission **before** clearing the Workspace
5. Build the map at maximum scale using:
   - Free community assets from Toolbox
   - AI Generated 3D meshes when assets aren't available
   - Full interior detail (chairs, tables, counters, shelves, products, cashiers, etc.)
6. Set up lighting and atmosphere to match the map's theme

---

### 🎮 Combined Mode
Request a character **and** a map in a single prompt. The AI will:
- Analyze both simultaneously
- Show **one unified preview** for a single approval step
- Build the character first → save to ServerStorage → then build the map
- Offer to place the character inside the map automatically

---

### 🤖 21 Specialized AI Agents
For building complete games, the skill uses 21 specialist agents working in a structured pipeline:

```
roblox-architect
      │
      ├── luau-scripter ──────────────────────────────────┐
      │                                                   │
      └── world-builder                                   │
              │                                           │
        interior-designer (×N rooms)                     │
              │                                           │
        ┌─────┴──────┐                                   │
        ▼            ▼                                    │
  detail-architect  set-dresser (×N rooms)                │
        │            │                                    │
        └─────┬──────┘                                   │
              ▼                                           │
        sound-designer                                    │
              │                                           │
         vfx-designer                                     │
              │                                           │
       lighting-director                                  │
              │                                           │
         art-director                                     │
              │                                           │
        enemy-designer                                    │
              │                                           │
         story-teller                                     │
              │                                           │
              └──────────────────────────────────────────┘
                            │
                      luau-reviewer
                            │
                       ui-designer
                            │
                   roblox-playtester
                            │
                    computer-player
                            │
               ┌────────────┴────────────┐
               ▼                         ▼
          Bugs found?               All clear?
               │                         │
          Fix & retry             roblox-publisher
                                         │
                                   Game is live! 🎮
```

| Category | Agents |
|---|---|
| **Architecture & Planning** | `roblox-architect`, `ai-developer`, `story-teller` |
| **Code & Scripts** | `luau-scripter`, `luau-reviewer`, `general-purpose-luau-notes` |
| **World Building** | `world-builder`, `interior-designer`, `detail-architect`, `set-dresser`, `enemy-designer` |
| **Visual & Audio** | `lighting-director`, `art-director`, `ui-designer`, `vfx-designer`, `sound-designer`, `showcase-photographer` |
| **Testing & Publishing** | `roblox-playtester`, `computer-player`, `analytics`, `roblox-publisher` |

---

### 📚 Deep Technical Reference Library
20 reference files covering every aspect of professional Roblox game development:

| File | Contents |
|---|---|
| `luau-mastery.md` | Luau typing, patterns, idioms, module design |
| `security-hardening.md` | Anti-cheat, server validation, exploit prevention |
| `datastore-persistence.md` | ProfileService, session locking, data migration |
| `combat-systems.md` | Hitbox, damage calculation, abilities |
| `multiplayer-networking.md` | RemoteEvents, state sync, lag compensation |
| `performance-optimization.md` | LOD, streaming, memory management |
| `gui-systems.md` | UIGradient, TweenService, responsive layouts |
| `monetization-systems.md` | GamePass, DevProduct, ProcessReceipt |
| `animation-vfx.md` | AnimationController, ParticleEmitter, Beam |
| `inventory-systems.md` | Item data, equip logic, hotbar |
| `architecture-patterns.md` | Service patterns, OOP in Luau, module design |
| `character-customization.md` | R6/R15 modification techniques |
| `asset-sourcing.md` | Finding and inserting free community assets |
| `generative-3d-modeling.md` | AI generating custom 3D meshes and PBR materials |
| `mcp-requirements.md` | MCP connection verification and error handling |
| `sharp-edges.md` | 12 critical Roblox gotchas with severity ratings |
| `mcp-orchestration.md` | MCP tool usage patterns |
| `testing-patterns.md` | Unit and integration testing in Roblox |
| `tooling-ecosystem.md` | Rojo, Wally, selene, stylua |
| `game-design-roblox.md` | Core loop design, retention, progression |

---

## Requirements

| Requirement | Details |
|---|---|
| **Claude Desktop** | Latest version with Skills support |
| **Roblox Studio** | Installed with a published place open |
| **Roblox MCP Server** | Connected in Claude Desktop settings |
| **Roblox Account** | Required for Toolbox access and publishing |

### Supported MCP Modes

| Mode | Tools | Capability |
|---|---|---|
| **Full** | 39 tools | All features: asset search, Luau execution, file browser, instance inspection |
| **Standard** | ~6 tools | Core builds: execute Luau, insert asset, console output |
| **Offline** | 0 tools | ❌ Skill halts — prompts user to reconnect MCP |

---

## Installation

### 1. Clone This Repository

```bash
git clone https://github.com/bagusmibr/evilsoft-blox.git
```

### 2. Copy to Claude Desktop Skills Directory

**macOS:**
```bash
cp -r evilsoft-blox ~/.gemini/config/skills/evilsoft-skillblox
```

**Windows:**
```powershell
xcopy /E /I evilsoft-blox %USERPROFILE%\.gemini\config\skills\evilsoft-skillblox
```

### 3. Restart Claude Desktop

Close and reopen Claude Desktop. The `evilsoft-skillblox` skill will be detected automatically.

### 4. Verify MCP Connection

In Claude Desktop → Settings → Developer → MCP Servers, confirm the Roblox Studio MCP shows **Connected**.

---

## Usage

### Triggering the Skill

The skill activates automatically when:

**Explicit:**
```
use evilsoft-skillblox to ...
skillblox, create a character ...
```

**Implicit:**
```
create a roblox character from this image [attach image]
build a roblox map that looks like a japanese dojo
make a tycoon game in roblox
```

---

### Example 1 — Creating a Character from an Image

```
[Attach a character image]

Create this character in Roblox. She is a fire mage with red and orange
robes, long silver hair, and glowing amber eyes. She should feel powerful
and mystical.
```

**What happens:**
1. AI analyzes the image and description
2. Searches web for references + Roblox Catalog for free accessories
3. Recommends R15 rig (due to outfit complexity) with reasoning
4. Shows a preview: colors per body part, accessories with Asset IDs, special effects
5. You approve → AI builds in Studio → saved to `ServerStorage/20260702_FireMage`
6. Full Luau script delivered in chat

---

### Example 2 — Building a Map from a Description

```
Build a Japanese convenience store map. It has an entrance, product shelves,
a cashier counter at the front, a drinks refrigerator section at the back,
and a restroom in the corner. Medium size, bright daytime lighting.
```

**What happens:**
1. AI searches for Japanese convenience store references online
2. Finds free shelves, refrigerators, and furniture assets on Roblox Toolbox
3. Shows a zone-by-zone preview with asset IDs and hand-crafted props listed
4. Asks: "May I clear the Workspace before building?"
5. You confirm → AI builds the entire map with full interior detail

---

### Example 3 — Character + Map Together

```
[Attach a samurai character image]

Create this samurai character and build a matching ancient Japanese temple
map for him to train in. Late afternoon atmosphere, slightly mysterious.
```

**What happens:**
1. AI analyzes the character and plans the temple simultaneously
2. One combined preview shown — one approval step for both
3. Samurai built → saved to ServerStorage → temple built
4. AI offers to place the samurai inside the temple

---

### Example 4 — Full Game Build

```
Build a horror escape game. 3 underground floors. The player starts in a
laboratory and needs keycards to unlock doors. There's a monster that
patrols and chases if it sees the player. Dark atmosphere, flickering lights.
```

**What happens:**
1. `roblox-architect` designs the full game blueprint
2. `luau-scripter` writes all scripts (checkpoint system, monster AI, keycard logic)
3. `world-builder` constructs 3 floors
4. `interior-designer` plans each room individually
5. `set-dresser` & `detail-architect` fill in all the details
6. `lighting-director` sets up horror lighting with flickering effects
7. `enemy-designer` creates the monster with pathfinding AI
8. `roblox-playtester` & `computer-player` test the game automatically
9. Bugs found → auto-fixed → retested
10. `roblox-publisher` publishes to Roblox

---

## Behavior Rules

| Condition | Behavior |
|---|---|
| MCP not detected | **HALT** — prompt user to reconnect, no workaround scripts generated |
| Character or map request | Always show a **preview first**, wait for approval before building |
| Workspace has existing content | **Ask permission** before removing anything |
| Asset not found in Toolbox | Generate using AI tools (mesh/material), notify user what was AI-generated |
| Minor revision (color change, reposition) | Apply in-place, no full rebuild |
| Major revision (rig swap, theme change) | Rebuild from scratch after confirmation |
| Ambiguous request | Ask **1 clarifying question**, then proceed |
| Character + map in one prompt | Handle both via combined workflow |
| Content type | No restrictions — all themes, genres, and character archetypes supported |

---

## File Structure

```
evilsoft-skillblox/
│
├── SKILL.md                              ← Master skill entry point
│
├── workflows/
│   ├── character-creation.md             ← Image-to-character workflow
│   ├── map-creation.md                   ← Image/description-to-map workflow
│   ├── combined-creation.md              ← Character + map in one session
│   ├── new-game.md                       ← Full game build workflow
│   ├── debug-loop.md                     ← Bug fixing and debug workflow
│   ├── code-review.md                    ← Luau code quality review
│   ├── performance-audit.md              ← Performance audit and optimization
│   ├── security-audit.md                 ← Security review workflow
│   ├── publish-checklist.md              ← Pre-publish checklist
│   └── monetization-audit.md             ← Monetization system review
│
├── references/                           ← 20 technical reference files
│
├── agents/                               ← 21 specialist AI agents
│
├── templates/
│   ├── character-preview.md              ← Character preview output template
│   └── map-preview.md                    ← Map preview output template
│
├── gamemaster/
│   ├── state.json                        ← Build progress tracker
│   ├── architecture.md                   ← Game design document
│   └── buglist.md                        ← Active bug list
│
├── README.md
└── .gitignore
```

---

## Troubleshooting

**Skill not detected in Claude Desktop**
- Confirm the folder is copied to `~/.gemini/config/skills/evilsoft-skillblox/`
- Restart Claude Desktop after copying
- Verify `SKILL.md` exists at the root of the skill folder

**MCP not connecting**
- Open Roblox Studio with a published place
- Enable HTTP Requests: **File → Game Settings → Security → Allow HTTP Requests = On**
- Check Studio Output window for: `"The MCP Studio plugin is ready for prompts."`
- In Claude Desktop → Settings → Developer → verify MCP shows "Connected"

**Character not saved to ServerStorage**
- Check Studio Output for Luau execution errors
- Ensure the place is published (MCP requires a published place to function)

**Toolbox asset insertion fails**
- The AI will automatically switch to generating the prop using AI (`generate_mesh`)
- The final report will list which assets were replaced and how

---

## License

MIT License — free to use, modify, and distribute.

---

<p align="center">
  <strong>Built by Evilsoft</strong>
</p>

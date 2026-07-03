# Character Creation Workflow

This workflow handles all requests to create a Roblox character from an image, description,
or both. Follow every step in order. Do not skip steps.

---

## Phase 1 — Input Collection

Accept any combination of:
- An image (photo, drawing, screenshot, reference art)
- A text description of the character
- Both together (preferred — gives best results)

If only an image is provided with no description, proceed — analyze the image directly.
If only a description with no image, proceed — use the description as the sole reference.

---

## Phase 2 — Research & Analysis

### 2a. Analyze Input
From the image and/or description, extract:
- Overall style (anime, realistic, cartoon, western, fantasy, sci-fi, etc.)
- Color palette (primary colors for head, torso, arms, legs)
- Key visual features (hair color/style, outfit type, accessories, markings)
- Character personality/archetype (hero, villain, mage, warrior, etc.)

### 2b. Internet Research
Search the web for:
- Visual references of the character (if it's from an existing IP/game/anime)
- Color hex codes or BrickColor equivalents for accurate color matching
- Roblox Catalog free accessories that match (search: `site:roblox.com/catalog [character trait] free`)

### 2c. Roblox Catalog Search & 3D Generation Planning
Search Roblox Catalog/Toolbox for free assets:
- Hair accessories matching the character's hairstyle
- Hat/headwear if applicable
- Shirts/pants (classic clothing) if available for free

**Face Decals:** 
Do NOT use default Roblox faces. Search for custom face decals using `search_asset` with `assetType="Image"` (e.g. `search_asset(query="anime face", assetType="Image")`).

**3D Mesh Generation (No Primitives):**
If an accessory (like a mask, glasses, sword, backpack) is not found in the Catalog, DO NOT build it from primitives. Instead, plan to use the `generate_mesh` MCP tool to create a custom 3D mesh for it.

For each found asset, record:
- Asset Name
- Asset ID
- Creator name
- Verified free (no Robux cost)

### 2d. Rig Selection
Analyze complexity and recommend rig type:

| Character Trait | Recommendation |
|---|---|
| Simple shape, minimal detail | R6 |
| Needs detailed arm/leg proportions | R15 |
| Has complex outfit layering | R15 |
| Anime-style with specific proportions | R15 |
| Blocky/classic Roblox style | R6 |
| Requires custom animations | R15 |

Always explain your recommendation to the user.

---

## Phase 3 — Preview (MANDATORY — Do Not Skip)

Generate the preview before doing ANYTHING in Studio.

### 3a. Generate Reference Image
Use image generation to create a 2D visual reference of what the character will look like.
The image should show: front view, the color scheme, accessories, and overall style.
Label it clearly: "Character Preview — [Name] — [R6/R15]"

### 3b. Generate Structured Text Preview

Output the following structured format:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CHARACTER PREVIEW
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Name:        [Character Name or "Custom Character"]
Rig Type:    [R6 / R15] — [Reason]
Timestamp:   [YYYYMMDD] (used for ServerStorage folder name)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BODY COLORS (BrickColor)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Head:             [BrickColor name]
Torso:            [BrickColor name]
Left Arm:         [BrickColor name]
Right Arm:        [BrickColor name]
Left Leg:         [BrickColor name]
Right Leg:        [BrickColor name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MATERIALS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Body Material:    [SmoothPlastic / Fabric / Metal / etc.]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ACCESSORIES (Free from Roblox Catalog)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Slot]       | [Asset Name]               | ID: [AssetID]
[Slot]       | [AI Generated 3D Mesh]     | (via generate_mesh)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ADDITIONAL FEATURES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Face:             [Face AssetID if applicable / Default]
Shirt:            [Shirt AssetID if applicable / None]
Pants:            [Pants AssetID if applicable / None]
Special effects:  [Particles, glow, trail / None]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
STORAGE LOCATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ServerStorage → [YYYYMMDD_CharacterName]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### 3c. Ask for Approval

After showing the preview image and structured text, ask:

```
✅ This is how your character will be built.

Do you approve this design?
  • Type "yes" or "proceed" to start building
  • Type "revise [what to change]" to adjust before building
  • Type "cancel" to abort
```

**Wait for response. Do not touch Studio until user approves.**

---

## Phase 4 — Build in Studio

Only begin after explicit user approval.

### 4a. Spawn Base Character Model

```luau
-- Execute via MCP execute_luau
local Players = game:GetService("Players")
local ServerStorage = game:GetService("ServerStorage")

-- Create character folder in ServerStorage
local timestamp = os.date("%Y%m%d")
local charName = "[YYYYMMDD_CharacterName]"  -- fill from preview
local charFolder = Instance.new("Model")
charFolder.Name = charName
charFolder.Parent = ServerStorage

-- Load default R6 or R15 rig
-- For R15: use StarterPlayer.StarterCharacter as base
-- For R6: use classic rig template
```

### 4b. Apply Body Colors

```luau
-- Apply BrickColor to each body part
local function applyColors(character)
    local colorMap = {
        Head = BrickColor.new("[COLOR]"),
        ["Upper Torso"] = BrickColor.new("[COLOR]"),  -- R15
        Torso = BrickColor.new("[COLOR]"),              -- R6
        ["Left Arm"] = BrickColor.new("[COLOR]"),
        ["Right Arm"] = BrickColor.new("[COLOR]"),
        ["Left Leg"] = BrickColor.new("[COLOR]"),
        ["Right Leg"] = BrickColor.new("[COLOR]"),
    }
    for partName, color in pairs(colorMap) do
        local part = character:FindFirstChild(partName)
        if part then
            part.BrickColor = color
            part.Material = Enum.Material.[MATERIAL]
        end
    end
end
```

### 4c. Insert Accessories from Catalog

Use MCP `insert_asset` for each accessory ID found in research:

```
insert_asset(assetId = [ASSET_ID], location = charFolder)
```

If insert fails or asset wasn't found: DO NOT build from primitives. Instead, use the `generate_mesh` MCP tool to create a 3D model for the accessory and attach it.

### 4d. Apply Face, Shirt, Pants

Apply the Image ID found via `search_asset(assetType="Image")` to the character's Head `Decal` (Texture). Do not leave the default face. Insert clothing via asset IDs. Apply via Humanoid.

### 4e. Add Special Effects (if any)

Add ParticleEmitters, SpecialMesh modifications, or Beams as needed.

### 4f. Save to ServerStorage

Move completed model to `ServerStorage/[YYYYMMDD_CharacterName]`.

---

## Phase 5 — Delivery Report

After build is complete, output in chat:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ CHARACTER BUILD COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Name:         [Character Name]
Rig:          [R6 / R15]
Location:     ServerStorage → [YYYYMMDD_CharacterName]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WHAT WAS BUILT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✓ Body colors applied to all [6/15] limbs
✓ Accessories inserted: [list]
✓ [X] accessories AI-generated (3D Mesh): [list]
✓ Custom Face applied (Image ID): [yes/no]
✓ Clothing applied: [yes/no]
✓ Special effects: [list or none]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
HOW TO USE IN YOUR GAME
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Find the model in ServerStorage → [YYYYMMDD_CharacterName]
2. To use as player character:
   - Move model to StarterPlayer.StarterCharacter
3. To spawn as NPC:
   - Clone from ServerStorage and parent to Workspace
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FULL LUAU SCRIPT (Copy-Paste Ready)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Full script used during build, formatted for copy-paste into Studio]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Revision Handling

**Minor revisions** (adjust without rebuilding):
- Change a color → re-apply BrickColor to that part only
- Swap one accessory → remove old, insert new
- Adjust size/scale → modify part Size property

**Major revisions** (rebuild from scratch):
- Change rig type (R6 ↔ R15)
- Complete color scheme overhaul
- Fundamental style change

For major revisions: confirm with user, then rebuild using same workflow from Phase 3.

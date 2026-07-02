# Map Creation Workflow

This workflow handles all requests to build a Roblox map from an image, a top-down layout,
a reference photo, or a text description. Follow every step in order.

---

## Phase 1 — Input Collection

Accept any combination of:
- A top-down image/screenshot of a map layout
- A reference photo of a real-world or fictional location
- A text description of the map (zones, rooms, atmosphere, theme)
- A hand-drawn layout diagram

If only an image: analyze the layout, identify zones, deduce style and theme.
If only a description: generate a mental map, ask one clarifying question if needed.

---

## Phase 2 — Research & Analysis

### 2a. Analyze the Map

Extract from input:
- **Theme** (horror, fantasy, modern city, school, forest, sci-fi, Japanese, etc.)
- **Zone list** (lobby, main hall, shop, outdoor area, dungeon, rooftop, etc.)
- **Key props** needed per zone (chairs, tables, counters, shelves, signs, trees, etc.)
- **Atmosphere** (lighting mood, time of day, weather)
- **Scale estimate** (small arena, medium map, large open world)

### 2b. Internet Research

Search the web for:
- Reference images of the location type (e.g., "Japanese convenience store interior")
- Color palettes and material references for the theme
- Roblox community builds of similar maps for inspiration (DevForum, YouTube)

### 2c. Roblox Toolbox Asset Search

For each major prop category:
1. Search Roblox Toolbox/Catalog for free community assets
2. Filter by: Free, relevant name, reasonable poly count
3. Prefer assets from Verified Creators when available
4. Record: Asset Name, Asset ID, Creator, what it represents

Asset categories to check:
- Structural: walls, floors, roofs, pillars, stairs, doors, windows
- Furniture: chairs, tables, desks, beds, shelves, counters, sofas
- Nature: trees, rocks, bushes, grass patches, flowers
- Urban: streetlights, benches, trash cans, fences, road markings
- Decorative: signs, posters, paintings, rugs, plants, lamps

### 2d. Gap Analysis

For any prop where no suitable free asset exists:
- Mark it as "BUILD FROM SCRATCH"
- Plan how to construct it from Roblox primitives (Parts, WedgeParts, Cylinders, Spheres)
- Document the construction plan (e.g., "counter = 3 Parts: base slab + side panels")

---

## Phase 3 — Preview (MANDATORY — Do Not Skip)

### 3a. Generate Reference Image

Use image generation to create a bird's-eye/isometric view of the planned map layout.
Show zone boundaries, major landmarks, and color scheme.
Label it: "Map Preview — [Map Name] — [Theme]"

### 3b. Generate Structured Text Preview

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MAP PREVIEW
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Name:         [Map Name or "Custom Map"]
Theme:        [Theme]
Estimated Size: [XxZ studs, maximized to fit content]
Zones:        [Number] zones
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ZONE BREAKDOWN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Zone 1 Name]
  Purpose:   [What happens here]
  Key Props: [List of props]
  Assets:    [Toolbox IDs or "Built from scratch"]

[Zone 2 Name]
  Purpose:   [What happens here]
  Key Props: [List of props]
  Assets:    [Toolbox IDs or "Built from scratch"]
  ...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COMMUNITY ASSETS TO INSERT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Asset Name]     | ID: [AssetID]  | Used for: [purpose]
[Asset Name]     | ID: [AssetID]  | Used for: [purpose]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
HAND-CRAFTED PROPS (Built from Roblox Primitives)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Prop Name]   → [Construction plan, e.g., "3 Parts: base + 2 side panels"]
[Prop Name]   → [Construction plan]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
LIGHTING PLAN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Ambient:      [ColorCorrectionEffect values]
Mood:         [Bright / Dark / Moody / Horror / etc.]
Special:      [Fog, SunRays, Bloom, etc.]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### 3c. Workspace Clearance Confirmation

Before building, ALWAYS ask:

```
⚠️  WORKSPACE CHECK

Your current Workspace contains existing content.
To build this map cleanly, I may need to clear some or all of it.

Options:
  • Type "clear all" — I will remove everything in Workspace and start fresh
  • Type "clear terrain only" — I will only remove Terrain, keep existing models
  • Type "keep everything" — I will build alongside existing content (may cause conflicts)
  • Type "cancel" — Abort the map build
```

**Wait for response before touching Workspace.**

### 3d. Final Approval

After showing preview image, text preview, and workspace confirmation:

```
✅ This is the map I will build.

Do you approve?
  • Type "yes" or "proceed" to start building
  • Type "revise [what to change]" to adjust the plan
  • Type "cancel" to abort
```

**Wait for approval. Do not build until confirmed.**

---

## Phase 4 — Build in Studio

Only begin after explicit user approval AND workspace clearance confirmed.

### 4a. Handle Workspace

Execute user's chosen clearance option via MCP execute_luau.

```luau
-- Clear all (if "clear all" chosen)
for _, obj in ipairs(workspace:GetChildren()) do
    if obj.Name ~= "Camera" and obj.Name ~= "Terrain" then
        obj:Destroy()
    end
end
workspace.Terrain:Clear()
```

### 4b. Build Base Structure

1. Create terrain/baseplate scaled to planned dimensions
2. Build outer walls, floor, ceiling for enclosed spaces
3. Create zone dividers (walls, paths, elevation changes)

**Scale principle:** Maximize the map size to properly fit all zones. 
Use 1 stud = ~0.3m as a human scale reference. Standard room height: 10-12 studs.

### 4c. Insert Community Assets

For each Toolbox asset in the plan:

```
insert_asset(assetId = [ASSET_ID])
```

Position each asset according to the zone layout.
If insert fails: switch to hand-crafted version, note it in the report.

### 4d. Build Hand-Crafted Props

For all "BUILD FROM SCRATCH" items, construct from primitives.

Always include interior details for indoor spaces:
- Shops: counters, product shelves, product displays, cashier station, price tags
- Offices: desks, computers (block form), chairs, filing cabinets, whiteboards
- Restaurants: tables, chairs, kitchen counter, menu boards
- Classrooms: student desks, teacher desk, blackboard, shelves
- Dungeons: pillars, torches (PointLight + Part), breakable debris

Use grouping (Model instances) to keep Workspace organized.

### 4e. Apply Lighting

Configure Lighting service:
- Set Ambient, OutdoorAmbient based on theme
- Add post-processing effects (Bloom, ColorCorrection, Atmosphere)
- Place local PointLights/SpotLights inside rooms as needed
- Apply fog if horror/dark theme

### 4f. Final Organization

Organize Workspace with clear Model/Folder hierarchy:
```
Workspace
├── Map_[Name]
│   ├── Zone_[Name1]
│   │   ├── Structure (walls, floor, ceiling)
│   │   └── Props
│   ├── Zone_[Name2]
│   └── ...
└── Lighting (local lights go here as children of parts)
```

---

## Phase 5 — Delivery Report

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ MAP BUILD COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Map Name:     [Name]
Theme:        [Theme]
Size:         [XxZ studs]
Zones Built:  [N]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ASSET SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Community assets inserted: [N]
Hand-crafted from primitives: [N]
Failed inserts (switched to primitives): [N]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WORKSPACE STRUCTURE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Workspace hierarchy tree]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WHAT WAS HAND-CRAFTED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[List of all props built from scratch and how]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
NEXT STEPS (Optional)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• "Add NPCs to [Zone]" — invoke enemy-designer agent
• "Add sound to [Zone]" — invoke sound-designer agent
• "Polish lighting" — invoke lighting-director agent
• "Publish this map" — invoke workflows/publish-checklist.md
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Revision Handling

**Minor** (adjust in-place):
- Move a prop → reposition in Studio
- Change a color → re-apply BrickColor
- Add/remove one item → targeted insertion or deletion

**Major** (rebuild needed):
- Complete theme change
- Layout restructure (zones swapped, map size change)
- Full replacement of major structure

For major: confirm with user, then re-run from Phase 3.

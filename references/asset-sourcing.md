# Asset Sourcing Reference

Guide for finding, evaluating, and inserting free Roblox community assets,
and supplementary internet research strategies for visual references.

---

## Source Priority Order

When looking for assets, follow this priority order:

1. **Roblox Toolbox (Free filter)** — official platform, safest
2. **Roblox Catalog (Free accessories)** — for character accessories
3. **Roblox DevForum asset threads** — community-shared free packs
4. **Internet search for asset IDs** — roblox.com/library searches
5. **AI 3D Generation** — use `generate_mesh` or `generate_procedural_model` when no asset is found

---

## Roblox Toolbox Search (via MCP)

### search_asset Tool
```
search_asset(query = "[search term]", assetType = "Model")
```

Effective search strategies:
- Use simple, specific terms: "wooden table", "brick wall", "street lamp"
- Try theme-specific: "japanese lantern", "sci-fi panel", "horror door"
- Append quality keywords: **"PBR", "Realistic", "High Quality"** (Crucial for eliminating basic/primitive asset bias)
- For Materials: Try searching `assetType="Image"` or `assetType="MeshPart"`.

### Asset Evaluation Criteria

Before using any community asset, check:

| Criteria | How to Verify |
|---|---|
| Free (0 Robux) | Check asset page |
| Reasonable part count | Inspect model — avoid 500+ part assets |
| Correct scale | Insert and check size vs. 5-stud player height |
| No malicious scripts | Inspect all scripts inside — delete if suspicious |
| No broken textures | Preview in Studio |

### Trusted Asset Types

**Always safe (no scripts):**
- Pure Part-based models
- Union-based models
- MeshPart models with no scripts

**Check carefully (may have scripts):**
- Interactive props (doors, buttons, vehicles)
- Game systems (shop frames, leaderboards)

**Rule:** If a free decorative prop has a Script inside it, delete the script before using.

---

## Roblox Catalog Search (Accessories for Characters)

### Web Search Strategy
```
Search query: site:roblox.com/catalog [accessory type] free
Examples:
  - site:roblox.com/catalog anime hair free
  - site:roblox.com/catalog ninja mask free
  - site:roblox.com/catalog wizard hat free
```

### Catalog URL Patterns
- Accessory: `https://www.roblox.com/catalog/[ASSET_ID]/[name]`
- Asset detail: shows price (0 = free), creator, type

### Catalog Asset Categories

| Category | Best for |
|---|---|
| Hair | Character hairstyle |
| Hat | Headgear |
| Face | Masks, glasses, face accessories |
| Neck | Scarves, collars, necklaces |
| Back | Wings, capes, backpacks |
| Front | Chest accessories |
| Shoulder | Pauldrons, shoulder pads |
| Waist | Belts, holsters |

---

## Internet Research Strategies

### For Character References
```
Search queries:
  "[character name] reference sheet" — front/side/back views
  "[character name] color palette" — exact colors used
  "[anime/game] character design" — style reference
  "[character name] roblox fanart" — see how others interpreted it in Roblox style
```

### For Map References
```
Search queries:
  "[location type] interior design" — layout and prop ideas
  "[location type] floor plan" — top-down layout reference
  "[location type] Roblox build" — see existing Roblox builds for scale reference
  "[theme] color palette" — atmospheric color reference
  "Japanese convenience store interior" (example of specific query)
```

### Useful Reference Sites
- **Pinterest** — mood boards, color palettes, interior references
- **ArtStation** — game environment art references
- **DeviantArt** — character reference sheets
- **Roblox DevForum** — community tutorials, asset packs
- **Google Images** — general visual research

---

## Asset Insertion via MCP

### insert_asset
```
insert_asset(assetId = 12345678)
```
Inserts asset into Workspace. Then reposition as needed.

### Batch insertion pattern
```luau
-- Insert multiple assets in one script
local InsertService = game:GetService("InsertService")

local assetIds = {
    12345678,  -- wooden table
    23456789,  -- chair
    34567890,  -- shelf
}

for _, id in ipairs(assetIds) do
    local model = InsertService:LoadAsset(id)
    if model then
        model.Parent = workspace
        print("Inserted asset: " .. id)
    else
        print("Failed to insert: " .. id .. " — will build from scratch")
    end
end
```

---

## Fallback: AI 3D Generative Modeling

When no suitable asset is found, DO NOT build it from Roblox primitives. Instead, rely on generative AI tools to create high-fidelity assets.

### 1. Generating Props/Accessories (`generate_mesh`)
If you need a static prop (e.g., a sword, a mask, a trash can, a rock), use the `generate_mesh` tool.

```luau
-- AI Thought Process:
-- "I need a realistic wooden chair. I didn't find a good PBR one in the Toolbox. I will use generate_mesh."
-- Tool Call: generate_mesh(textPrompt="a highly detailed realistic wooden chair with PBR textures")
```

### 2. Generating Customizable Structures (`generate_procedural_model`)
If you need a more complex object that the user might want to edit later (e.g., a car, a table with adjustable legs), use `generate_procedural_model`.

```luau
-- AI Thought Process:
-- "I need a shop counter. I will use generate_procedural_model."
-- Tool Call: generate_procedural_model(prompt="a modern shop counter with adjustable length and color")
```

### 3. Generating Realistic Materials (`generate_material`)
If you are coloring walls, floors, or terrain, never use the default `Enum.Material` for realistic builds. Use `generate_material`.

```luau
-- AI Thought Process:
-- "I need realistic grass for the floor."
-- Tool Call: generate_material(prompt="high resolution realistic lush green grass, PBR")
```

---

## Asset Documentation Template

When documenting assets used in a build, use this format:

```
ASSET LOG — [Build Name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Asset Name]       | ID: [ID]    | Zone: [Zone] | Type: Toolbox Model
[Asset Name]       | ID: [ID]    | Zone: [Zone] | Type: Catalog Accessory
[Prop Name]        | AI GEN      | Zone: [Zone] | Type: AI Generated 3D Mesh
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total Toolbox:    [N]
Total Catalog:    [N]
Total AI Meshes:  [N]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

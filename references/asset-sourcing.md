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
5. **Build from scratch** — when nothing suitable is found

---

## Roblox Toolbox Search (via MCP)

### search_asset Tool
```
search_asset(query = "[search term]", assetType = "Model")
```

Effective search strategies:
- Use simple, specific terms: "wooden table", "brick wall", "street lamp"
- Try theme-specific: "japanese lantern", "sci-fi panel", "horror door"
- Try material-specific: "metal crate", "stone pillar", "wooden shelf"
- Try function-specific: "shop counter", "classroom desk", "hospital bed"

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

## Fallback: Build from Scratch

When no suitable asset is found, build from Roblox primitives.

### Common Props Construction Guide

#### Shop Counter
```luau
-- Counter = wide flat slab + kickboard
local counter = Instance.new("Model")
counter.Name = "ShopCounter"

local top = Instance.new("Part")
top.Size = Vector3.new(8, 0.4, 3)
top.BrickColor = BrickColor.new("White")
top.Material = Enum.Material.SmoothPlastic
top.CFrame = CFrame.new(0, 3, 0)
top.Parent = counter

local base = Instance.new("Part")
base.Size = Vector3.new(8, 2.5, 3)
base.BrickColor = BrickColor.new("Light grey")
base.Material = Enum.Material.SmoothPlastic
base.CFrame = CFrame.new(0, 1.45, 0)
base.Parent = counter
```

#### Simple Chair
```luau
local chair = Instance.new("Model")
chair.Name = "Chair"

local seat = Instance.new("Part")
seat.Size = Vector3.new(2, 0.2, 2)
seat.BrickColor = BrickColor.new("Brown")
seat.CFrame = CFrame.new(0, 1.5, 0)
seat.Parent = chair

local backrest = Instance.new("Part")
backrest.Size = Vector3.new(2, 2, 0.2)
backrest.BrickColor = BrickColor.new("Brown")
backrest.CFrame = CFrame.new(0, 2.5, -1)
backrest.Parent = chair

-- 4 legs
for i, pos in ipairs({
    Vector3.new(0.8, 0.75, 0.8),
    Vector3.new(-0.8, 0.75, 0.8),
    Vector3.new(0.8, 0.75, -0.8),
    Vector3.new(-0.8, 0.75, -0.8),
}) do
    local leg = Instance.new("Part")
    leg.Size = Vector3.new(0.2, 1.5, 0.2)
    leg.BrickColor = BrickColor.new("Brown")
    leg.CFrame = CFrame.new(pos)
    leg.Parent = chair
end
```

#### Product on Shelf
```luau
-- Simple can/bottle product
local product = Instance.new("Part")
product.Shape = Enum.PartType.Cylinder
product.Size = Vector3.new(1, 0.6, 0.6)
product.BrickColor = BrickColor.new("Bright red")
product.Material = Enum.Material.SmoothPlastic
product.CFrame = CFrame.new(0, 0, 0)
```

#### Cashier Station (POS Terminal)
```luau
local pos = Instance.new("Model")
pos.Name = "CashierTerminal"

local screen = Instance.new("Part")
screen.Size = Vector3.new(1.5, 1.2, 0.1)
screen.BrickColor = BrickColor.new("Black")
screen.Material = Enum.Material.Neon
screen.CFrame = CFrame.new(0, 0.6, 0)
screen.Parent = pos

local base = Instance.new("Part")
base.Size = Vector3.new(1.5, 0.1, 1)
base.BrickColor = BrickColor.new("Dark grey")
base.CFrame = CFrame.new(0, 0, 0)
base.Parent = pos
```

#### Wall Shelf
```luau
local shelf = Instance.new("Model")
shelf.Name = "WallShelf"

local board = Instance.new("Part")
board.Size = Vector3.new(6, 0.2, 1)
board.BrickColor = BrickColor.new("Reddish brown")
board.Material = Enum.Material.Wood
board.CFrame = CFrame.new(0, 0, 0)
board.Parent = shelf

-- Brackets
for _, x in ipairs({-2.5, 2.5}) do
    local bracket = Instance.new("WedgePart")
    bracket.Size = Vector3.new(0.2, 0.8, 1)
    bracket.BrickColor = BrickColor.new("Dark grey")
    bracket.CFrame = CFrame.new(x, -0.5, 0) * CFrame.Angles(0, 0, math.rad(x > 0 and 90 or -90))
    bracket.Parent = shelf
end
```

---

## Asset Documentation Template

When documenting assets used in a build, use this format:

```
ASSET LOG — [Build Name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Asset Name]       | ID: [ID]    | Zone: [Zone] | Type: Toolbox Model
[Asset Name]       | ID: [ID]    | Zone: [Zone] | Type: Catalog Accessory
[Prop Name]        | NO ID       | Zone: [Zone] | Type: Built from Primitives
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total Toolbox:    [N]
Total Catalog:    [N]
Total Scratch:    [N]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

# Map Building from Scratch Reference

Complete guide for constructing Roblox map environments entirely from primitives
when community assets are unavailable or insufficient.

---

## Core Principles

1. **Readability first** — Players should immediately understand what a space is for
2. **Scale accuracy** — Human scale = ~5 studs tall. Rooms = 10-12 studs ceiling
3. **Detail layering** — Structure → Large props → Medium props → Small details
4. **Material storytelling** — Use materials to communicate surface type
5. **Interior always furnished** — An empty room is a failed room

---

## Scale Reference

| Real object | Roblox studs |
|---|---|
| Adult human | 5 studs tall |
| Door height | 8 studs |
| Standard room ceiling | 10-12 studs |
| Standard door width | 4 studs |
| Table height | 3 studs |
| Chair height (seat) | 1.5 studs |
| Standard floor slab | 1 stud thick |
| Standard wall | 1-2 studs thick |
| Staircase step | 1 stud rise, 2 studs run |

---

## Structure Building

### Floor Slab
```luau
local floor = Instance.new("Part")
floor.Name = "Floor"
floor.Anchored = true
floor.Size = Vector3.new(50, 1, 50)  -- 50x50 stud room
floor.BrickColor = BrickColor.new("Light grey")
floor.Material = Enum.Material.SmoothPlastic
floor.CFrame = CFrame.new(0, -0.5, 0)
floor.Parent = workspace
```

### Wall
```luau
local function makeWall(width, height, thickness, position, rotation, color, material)
    local wall = Instance.new("Part")
    wall.Name = "Wall"
    wall.Anchored = true
    wall.Size = Vector3.new(width, height, thickness)
    wall.BrickColor = BrickColor.new(color or "White")
    wall.Material = material or Enum.Material.SmoothPlastic
    wall.CFrame = CFrame.new(position) * CFrame.Angles(0, rotation or 0, 0)
    wall.Parent = workspace
    return wall
end
```

### Room Generator
```luau
local function buildRoom(cx, cz, width, depth, height, wallColor, floorColor)
    local room = Instance.new("Model")
    room.Name = "Room"

    -- Floor
    local floor = Instance.new("Part")
    floor.Name = "Floor"
    floor.Anchored = true
    floor.Size = Vector3.new(width, 1, depth)
    floor.BrickColor = BrickColor.new(floorColor or "Light grey")
    floor.CFrame = CFrame.new(cx, -0.5, cz)
    floor.Parent = room

    -- Ceiling
    local ceiling = Instance.new("Part")
    ceiling.Name = "Ceiling"
    ceiling.Anchored = true
    ceiling.Size = Vector3.new(width, 1, depth)
    ceiling.BrickColor = BrickColor.new("White")
    ceiling.CFrame = CFrame.new(cx, height + 0.5, cz)
    ceiling.Parent = room

    -- Walls (N, S, E, W)
    local walls = {
        {Vector3.new(width, height, 1), Vector3.new(cx, height/2, cz - depth/2)},
        {Vector3.new(width, height, 1), Vector3.new(cx, height/2, cz + depth/2)},
        {Vector3.new(1, height, depth), Vector3.new(cx - width/2, height/2, cz)},
        {Vector3.new(1, height, depth), Vector3.new(cx + width/2, height/2, cz)},
    }
    for _, w in ipairs(walls) do
        local wall = Instance.new("Part")
        wall.Name = "Wall"
        wall.Anchored = true
        wall.Size = w[1]
        wall.BrickColor = BrickColor.new(wallColor or "White")
        wall.Material = Enum.Material.SmoothPlastic
        wall.CFrame = CFrame.new(w[2])
        wall.Parent = room
    end

    room.Parent = workspace
    return room
end
```

---

## Interior Details by Location Type

### Convenience Store / Shop
```
Required:
  - Service counter (wide, knee-height slab)
  - Cashier POS terminal (small screen + base)
  - Product shelves (wall-mounted or freestanding)
  - Products on shelves (cylinders for cans, boxes)
  - Refrigerator unit (tall box, slightly transparent door optional)
  - Shopping basket rack
  - Exit/entrance door frame

Optional:
  - Price tag signs (SurfaceGui with TextLabel)
  - Overhead fluorescent lights (white Neon part)
  - Security camera (cylinder + sphere)
```

### Classroom
```
Required:
  - Student desks in rows (small flat surface + legs)
  - Student chairs at each desk
  - Teacher desk (larger, at front)
  - Blackboard/whiteboard (flat dark green or white part on wall)
  - Chalk tray (thin strip under board)
  - Door and window frames

Optional:
  - Bookshelf at back
  - Globe on teacher's desk
  - Papers on student desks (thin flat white parts)
  - Clock on wall (circle SurfaceGui)
```

### Hospital Room
```
Required:
  - Hospital bed (frame + mattress + pillow)
  - Medical IV stand (thin vertical cylinder + horizontal arm)
  - Bedside monitor (box + Neon screen part)
  - Bedside table
  - Privacy curtain track (thin horizontal cylinder near ceiling)

Optional:
  - Medical cabinet on wall
  - Window with blinds
  - Overhead surgical light
```

### Restaurant / Cafe
```
Required:
  - Tables (round or rectangular)
  - Chairs (2-4 per table)
  - Service counter / bar
  - Menu board (vertical part + SurfaceGui text)
  - Kitchen area (visible or implied)

Optional:
  - Pendant lights above tables
  - Flowers on tables
  - Window seating with sill
  - Cash register
```

### Dungeon / Cave
```
Required:
  - Stone floor (Material = Cobblestone or Concrete)
  - Rough stone walls (use SmoothPlastic gray or Concrete)
  - Ceiling supports (pillar arches every 10-15 studs)
  - Torches: PointLight inside orange Neon cylinder/flame shape
  - Iron door or wooden door (Parts arranged as planks)
  - Debris on floor (small irregular Parts, BrickColor = Dark grey)

Optional:
  - Chain hanging from ceiling (thin cylinders linked)
  - Skeleton (assembled from Parts — oval for skull, cylinders for bones)
  - Treasure chest (box + lid arc)
  - Water puddle (flat Neon part, blue, SmoothPlastic)
```

### Forest / Outdoor
```
Required:
  - Ground terrain (use Terrain tool or large flat wedged parts)
  - Trees: trunk (cylinder, brown) + canopy (sphere or union, dark green)
  - Rocks: irregular Parts, Material = Slate or Concrete
  - Grass patches: flat thin Parts, Material = Grass or LeafyGrass color

Optional:
  - Bushes (small green spheres)
  - Path (flat tan/sand colored strip)
  - Fence (vertical posts + horizontal rails)
  - Pond (flat Neon part, water-color blue, low transparency)
```

---

## Lighting for Maps

### Theme Presets

#### Bright/Daytime Indoor
```luau
local Lighting = game:GetService("Lighting")
Lighting.Ambient = Color3.fromRGB(180, 180, 180)
Lighting.OutdoorAmbient = Color3.fromRGB(200, 200, 200)
Lighting.Brightness = 2
Lighting.ClockTime = 14

local cc = Instance.new("ColorCorrectionEffect")
cc.Brightness = 0.02
cc.Contrast = 0.1
cc.Parent = Lighting
```

#### Horror/Dark
```luau
Lighting.Ambient = Color3.fromRGB(30, 20, 20)
Lighting.OutdoorAmbient = Color3.fromRGB(20, 10, 10)
Lighting.Brightness = 0.3
Lighting.FogEnabled = true
Lighting.FogColor = Color3.fromRGB(40, 10, 10)
Lighting.FogStart = 20
Lighting.FogEnd = 80

local bloom = Instance.new("BloomEffect")
bloom.Intensity = 0.5
bloom.Size = 24
bloom.Parent = Lighting
```

#### Sci-Fi
```luau
Lighting.Ambient = Color3.fromRGB(10, 20, 50)
Lighting.OutdoorAmbient = Color3.fromRGB(0, 20, 60)
Lighting.Brightness = 0.5

local cc = Instance.new("ColorCorrectionEffect")
cc.TintColor = Color3.fromRGB(180, 220, 255)
cc.Contrast = 0.2
cc.Parent = Lighting
```

#### Fantasy/Magic
```luau
Lighting.Ambient = Color3.fromRGB(80, 40, 120)
Lighting.OutdoorAmbient = Color3.fromRGB(100, 60, 180)
Lighting.Brightness = 1.5

local bloom = Instance.new("BloomEffect")
bloom.Intensity = 1.2
bloom.Parent = Lighting
```

---

## Organization Pattern

Always organize Workspace with clear hierarchy:

```luau
-- Create main map folder
local mapModel = Instance.new("Model")
mapModel.Name = "Map_" .. mapName
mapModel.Parent = workspace

-- Zone folders
local function createZone(name, parent)
    local zone = Instance.new("Model")
    zone.Name = "Zone_" .. name
    zone.Parent = parent
    
    local structure = Instance.new("Model")
    structure.Name = "Structure"
    structure.Parent = zone
    
    local props = Instance.new("Model")
    props.Name = "Props"
    props.Parent = zone
    
    return zone, structure, props
end
```

---

## Performance Guidelines

- Keep total Workspace parts under 10,000 for good performance
- Use `Anchored = true` on all static parts
- Set `CastShadow = false` on very small detail parts
- Use `CanCollide = false` on decorative props that players won't interact with
- Group related parts into Models with a PrimaryPart set
- Use Unions sparingly — they can have higher render cost than separate parts
- Replace very detailed hand-crafted props with simpler versions in background areas

# Character Customization Reference

Comprehensive technical reference for modifying Roblox R6 and R15 character rigs
without custom 3D modeling. All techniques use Studio-native properties and MCP tools.

---

## Rig Types

### R6 (6-part rig)
Parts: Head, Torso, Left Arm, Right Arm, Left Leg, Right Leg

```
Structure:
Model (Character)
├── HumanoidRootPart
├── Torso
├── Head
├── Left Arm
├── Right Arm
├── Left Leg
└── Right Leg
```

**Best for:** Classic Roblox style, simple characters, lower complexity, retro aesthetic.
**Limitations:** Less articulation, arms/legs are single solid parts.

### R15 (15-part rig)
Parts: HumanoidRootPart, LowerTorso, UpperTorso, Head, LeftUpperArm, LeftLowerArm,
LeftHand, RightUpperArm, RightLowerArm, RightHand, LeftUpperLeg, LeftLowerLeg,
LeftFoot, RightUpperLeg, RightLowerLeg, RightFoot

**Best for:** Detailed characters, anime-style proportions, custom animations,
complex outfit layering.

---

## Color Application

### BrickColor
```luau
part.BrickColor = BrickColor.new("Bright red")
-- Or by number:
part.BrickColor = BrickColor.new(21)
```

### Color3 (more precise)
```luau
part.Color = Color3.fromRGB(255, 100, 50)
-- Or from hex:
part.Color = Color3.fromHex("#FF6432")
```

### Common BrickColors for Characters

| BrickColor Name | Use Case |
|---|---|
| "Reddish brown" | Wood skin, warm tones |
| "Light orange" | Light skin tone |
| "Nougat" | Medium skin tone |
| "Dark orange" | Dark skin tone |
| "Black" | Dark outfit, villain |
| "White" | Light outfit, angel |
| "Bright red" | Bold outfit, hero |
| "Bright blue" | Cool character |
| "Dark green" | Military, nature |
| "Sand green" | Muted, earthy |
| "Bright yellow" | Bright, cheerful |
| "Medium stone grey" | Armor, robot, stone |
| "Pearl gold" | Luxury, royalty |
| "Cyan" | Sci-fi, ice |

---

## Material Application

```luau
part.Material = Enum.Material.SmoothPlastic  -- default, clean
part.Material = Enum.Material.Fabric         -- cloth-like appearance
part.Material = Enum.Material.Metal          -- metallic, reflective
part.Material = Enum.Material.DiamondPlate   -- grated metal
part.Material = Enum.Material.Neon           -- glowing effect
part.Material = Enum.Material.Foil           -- shiny metallic
part.Material = Enum.Material.Wood           -- wooden texture
part.Material = Enum.Material.Concrete       -- rough stone
```

---

## Size & Scale Modifications

### Scaling individual body parts (R6)
```luau
local arm = character:FindFirstChild("Left Arm")
arm.Size = Vector3.new(1, 2, 1)  -- default is 1, 2, 1 for R6
```

### R15 Body Scale (via Humanoid)
```luau
local humanoid = character:FindFirstChildOfClass("Humanoid")
local desc = humanoid:GetAppliedDescription()
desc.HeightScale = 1.0          -- 0.9 = shorter, 1.1 = taller
desc.WidthScale = 1.0           -- body width
desc.HeadScale = 1.0            -- head size
desc.BodyTypeScale = 0.0        -- 0=blocky, 1=slim
desc.ProportionScale = 0.0      -- 0=classic, 1=thin
humanoid:ApplyDescription(desc)
```

---

## Accessory System

### Insert from Roblox Catalog (via MCP)
```
insert_asset(assetId = 12345678)
```
Then parent to character and position.

### Accessory Attachment Points

| Attachment Name | Location |
|---|---|
| HatAttachment | Top of Head |
| HairAttachment | Top of Head |
| FaceFrontAttachment | Front of Head (face accessories) |
| NeckAttachment | Neck area |
| LeftShoulderAttachment | Left shoulder |
| RightShoulderAttachment | Right shoulder |
| BodyFrontAttachment | Front of Torso |
| BodyBackAttachment | Back of Torso |
| WaistFrontAttachment | Front waist |
| WaistBackAttachment | Back waist |
| LeftGripAttachment | Left hand (tools, weapons) |
| RightGripAttachment | Right hand (tools, weapons) |

### Manual Accessory Creation
```luau
local accessory = Instance.new("Accessory")
accessory.Name = "CustomHat"

local handle = Instance.new("Part")
handle.Name = "Handle"
handle.Size = Vector3.new(2, 1, 2)
handle.BrickColor = BrickColor.new("Black")
handle.Parent = accessory

local attachment = Instance.new("Attachment")
attachment.Name = "HatAttachment"
attachment.Position = Vector3.new(0, -0.5, 0)
attachment.Parent = handle

accessory.Parent = character
```

---

## Clothing System

### Classic Clothing (Shirt/Pants)
```luau
local shirt = Instance.new("Shirt")
shirt.ShirtTemplate = "rbxassetid://[SHIRT_ASSET_ID]"
shirt.Parent = character

local pants = Instance.new("Pants")
pants.PantsTemplate = "rbxassetid://[PANTS_ASSET_ID]"
pants.Parent = character
```

### Layered Clothing (R15 only)
Insert WrapLayer assets from Catalog. These conform to body shape automatically.

---

## Face Customization

```luau
local humanoid = character:FindFirstChildOfClass("Humanoid")
local desc = humanoid:GetAppliedDescription()
desc.Face = [FACE_ASSET_ID]  -- from Roblox Catalog
humanoid:ApplyDescription(desc)
```

---

## Special Effects on Characters

### Neon Glow Effect
```luau
part.Material = Enum.Material.Neon
part.Color = Color3.fromRGB(0, 200, 255)  -- cyan glow
```

### Trail Effect
```luau
local trail = Instance.new("Trail")
trail.Attachment0 = attachment1  -- on HumanoidRootPart
trail.Attachment1 = attachment2
trail.Color = ColorSequence.new(Color3.fromRGB(255, 100, 0))
trail.Lifetime = 0.5
trail.Parent = character
```

### Particle Effect (aura around character)
```luau
local emitter = Instance.new("ParticleEmitter")
emitter.Rate = 20
emitter.Lifetime = NumberRange.new(0.5, 1.5)
emitter.Speed = NumberRange.new(2, 5)
emitter.Color = ColorSequence.new(Color3.fromRGB(255, 200, 0))
emitter.Parent = character.HumanoidRootPart
```

### PointLight (glowing character)
```luau
local light = Instance.new("PointLight")
light.Brightness = 5
light.Range = 20
light.Color = Color3.fromRGB(100, 200, 255)
light.Parent = character.HumanoidRootPart
```

---

## ServerStorage Placement Pattern

```luau
local ServerStorage = game:GetService("ServerStorage")
local timestamp = os.date("%Y%m%d")

-- Create named folder
local folder = Instance.new("Folder")
folder.Name = timestamp .. "_" .. characterShortName
folder.Parent = ServerStorage

-- Move character model into folder
character.Parent = folder

print("Character saved: " .. folder.Name)
```

---

## Complete Character Build Script Template

```luau
-- Evilsoft-Skillblox: Character Build Script
-- Generated by evilsoft-skillblox skill
-- Run this in a Script inside ServerScriptService (once)

local ServerStorage = game:GetService("ServerStorage")

local function buildCharacter(name, rigType)
    -- 1. Clone base rig from StarterPlayer
    local StarterPlayer = game:GetService("StarterPlayer")
    local baseChar = StarterPlayer.StarterCharacter
    
    if not baseChar then
        -- Fall back: construct minimal humanoid model
        baseChar = Instance.new("Model")
        baseChar.Name = name
        local humanoid = Instance.new("Humanoid")
        humanoid.Parent = baseChar
        local hrp = Instance.new("Part")
        hrp.Name = "HumanoidRootPart"
        hrp.Parent = baseChar
    end
    
    local char = baseChar:Clone()
    char.Name = name
    
    -- 2. Apply colors (fill in values from preview)
    local colorMap = {
        Head =          BrickColor.new("REPLACE"),
        Torso =         BrickColor.new("REPLACE"),  -- R6
        ["Left Arm"] =  BrickColor.new("REPLACE"),
        ["Right Arm"] = BrickColor.new("REPLACE"),
        ["Left Leg"] =  BrickColor.new("REPLACE"),
        ["Right Leg"] = BrickColor.new("REPLACE"),
    }
    
    for partName, color in pairs(colorMap) do
        local part = char:FindFirstChild(partName)
        if part and part:IsA("BasePart") then
            part.BrickColor = color
            part.Material = Enum.Material.SmoothPlastic
        end
    end
    
    -- 3. Save to ServerStorage
    local timestamp = os.date("%Y%m%d")
    local folder = Instance.new("Folder")
    folder.Name = timestamp .. "_" .. name
    char.Parent = folder
    folder.Parent = ServerStorage
    
    print("[Evilsoft-Skillblox] Character built: " .. folder.Name)
end

buildCharacter("CharacterNameHere", "R6")
```

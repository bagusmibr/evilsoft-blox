# Generative 3D Modeling

When building characters and maps in Roblox, we want to achieve the highest possible visual fidelity. Instead of building items from basic primitives (`Instance.new("Part")`) and applying basic colors, you must utilize Roblox's Generative AI tools via MCP to create actual 3D models and PBR textures.

## 1. `generate_mesh`
Use this tool to generate a textured 3D mesh from a text prompt.

**When to use:**
- Creating character accessories (masks, hats, swords, backpacks) that cannot be found in the Catalog.
- Creating single, solid props for maps (statues, rocks, weapons, specific furniture pieces).
- When you need a high-quality, singular 3D object.

**How to use:**
Call the MCP tool: `generate_mesh(textPrompt="[highly descriptive prompt]")`
- **Prompting Tips:** Be specific about style, material, and colors. E.g., `generate_mesh(textPrompt="a glowing red fantasy sword with a golden hilt, anime style")`.

## 2. `generate_procedural_model`
Use this tool to create 3D objects built from primitives but organized as a scriptable `ProceduralModel` with configurable attributes.

**When to use:**
- Building structures with distinct parts (e.g., a car with wheels, a table with legs).
- Building objects that the user might want to configure later (e.g., "a wooden chair with adjustable leg height").
- Generating complex props where `generate_mesh` might struggle with the topology.

**How to use:**
Call the MCP tool: `generate_procedural_model(prompt="[descriptive prompt with configurable attributes]")`
- **Prompting Tips:** Name the configurable parts. E.g., `generate_procedural_model(prompt="a wooden dining table with adjustable leg height, table width, and wood color")`.

## 3. `generate_material`
Use this tool to generate custom PBR (Physically Based Rendering) materials.

**When to use:**
- Applying textures to floors, walls, and terrain in map builds.
- NEVER use basic `Enum.Material.Grass` or `Enum.Material.Wood` if a realistic theme is requested. Generate a custom PBR material instead.

**How to use:**
Call the MCP tool: `generate_material(prompt="[material description]")`
- **Prompting Tips:** Include keywords like "realistic", "weathered", "seamless", "4k". E.g., `generate_material(prompt="realistic weathered wood planks with deep grooves, PBR")`.

## Workflow Integration
1. **Prioritize the Toolbox/Catalog:** Always try to find a high-quality, free community asset first using `search_asset(assetType="MeshPart", query="...")` or `assetType="Image"` for decals.
2. **Fallback to AI Generation:** If no high-quality asset is found, DO NOT build it manually from Parts. Invoke `generate_mesh` or `generate_procedural_model`.
3. **Materials:** For any surface covering a large area, invoke `generate_material` to give it a realistic texture.

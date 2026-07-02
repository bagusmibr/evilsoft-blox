# Combined Creation Workflow (Character + Map)

This workflow handles requests that include BOTH a character creation AND a map build
in a single prompt. Examples:
- "Create a ninja character and build a dojo map for him"
- "Make this anime girl character and build her bedroom"
- "Build this villain and create a dark castle map"

Run both pipelines together with a single unified preview and approval step.

---

## Phase 1 — Parse Combined Input

Split the user's request into two clear components:

**Character Component:**
- Who is the character? (image, description, or both)
- Rig preference or Claude decides? (default: Claude analyzes)
- Special features? (weapons as accessories, special effects, etc.)

**Map Component:**
- What is the map? (image, layout, description)
- What theme/atmosphere?
- Is the map specifically for this character? (if yes, design map to fit character's style)

If components are unclear, ask one clarifying question:
> "Just to confirm — do you want [Character X] placed IN [Map Y], or are these two separate things?"

---

## Phase 2 — Research Both in Parallel

Run research for character and map simultaneously:

**Character Research:**
- Internet search for visual references
- Roblox Catalog search for free accessories
- Rig analysis (R6 vs R15)

**Map Research:**
- Internet search for location references
- Roblox Toolbox search for structural/prop assets
- Gap analysis (what needs to be built from scratch)

**Thematic Cohesion Check:**
- Do character colors match the map's color palette? (optional recommendation)
- Does the character style fit the map theme? (flag any mismatch)

---

## Phase 3 — Unified Preview

Produce ONE combined preview for a single approval step.

### 3a. Generate Combined Reference Image

Create a single image showing:
- The character design (front view) on the LEFT
- The map layout (bird's-eye or isometric) on the RIGHT
- Label: "Combined Preview — [Character Name] + [Map Name]"

### 3b. Generate Unified Structured Preview

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COMBINED BUILD PREVIEW
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[CHARACTER]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Name:         [Character Name]
Rig:          [R6 / R15] — [Reason]
Storage:      ServerStorage → [YYYYMMDD_CharacterName]
Body Colors:  [Summary: Head=X, Torso=Y, ...]
Accessories:  [List]
Hand-crafted: [List if any]

[MAP]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Name:         [Map Name]
Theme:        [Theme]
Size:         [XxZ studs]
Zones:        [List]
Community assets: [N items, list IDs]
Hand-crafted:     [N props, list]

[THEMATIC NOTE]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Note on how character and map relate visually, or "No conflicts detected"]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### 3c. Workspace Confirmation

Ask workspace clearance question (same as `map-creation.md` Phase 3c).

### 3d. Single Approval

```
✅ Here is the full plan for both the character and the map.

Do you approve? Type:
  • "yes" / "proceed" → build both
  • "revise character [what]" → adjust character plan only
  • "revise map [what]" → adjust map plan only
  • "revise both [what]" → adjust both
  • "cancel" → abort
```

**Do not build anything until user confirms.**

---

## Phase 4 — Build Sequence

Build in this order:

### 4a. Build Character First
Follow all steps from `character-creation.md` Phase 4.
Save to `ServerStorage/[YYYYMMDD_CharacterName]`.

### 4b. Build Map Second
Follow all steps from `map-creation.md` Phase 4.
Organize in Workspace hierarchy.

### 4c. Optional: Place Character in Map (Ask User)

After both are built:

```
Both the character and map are ready.

Would you like me to place the character into the map?
  • Type "yes" → I'll clone the character from ServerStorage and place it at [spawn point]
  • Type "no" → Leave character in ServerStorage for you to place manually
```

If yes: clone character from ServerStorage, parent to Workspace, position at map spawn.

---

## Phase 5 — Combined Delivery Report

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ COMBINED BUILD COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

CHARACTER: [Name]
  ✓ Rig: [R6/R15]
  ✓ Colors: applied to all limbs
  ✓ Accessories: [N] inserted, [N] built from scratch
  ✓ Location: ServerStorage → [YYYYMMDD_CharacterName]

MAP: [Name]
  ✓ Theme: [Theme]
  ✓ Size: [XxZ studs]
  ✓ Zones: [N] built
  ✓ Community assets: [N] inserted
  ✓ Hand-crafted props: [N]
  ✓ Placed in Workspace → Map_[Name]

PLACEMENT: [Character placed in map at [XYZ] / Not placed — in ServerStorage]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FULL LUAU SCRIPTS (Copy-Paste Ready)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Character build script]
[Map build script]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

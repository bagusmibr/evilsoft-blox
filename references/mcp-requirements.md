# MCP Requirements Reference

This reference defines the exact MCP connection requirements for Evilsoft-Skillblox.
All Studio build operations depend on an active, working MCP connection.

---

## Hard Rule

> ⛔ If MCP is not verified as active, ALL build operations must halt immediately.
> Do NOT generate workaround scripts or attempt offline substitutes.
> The skill must inform the user and stop — no exceptions.

---

## MCP Detection Sequence

On every invocation that involves Studio operations, run this detection sequence:

### Step 1: Check for Key Tools

Look for the presence of these tools (any combination indicates MCP is active):

| Tool Name | Mode | Purpose |
|---|---|---|
| `execute_luau` | Full or Standard | Run Luau code in Studio |
| `insert_asset` | Full or Standard | Insert models from Roblox catalog |
| `search_asset` | Full | Search Toolbox |
| `get_console_output` | Full or Standard | Read Studio output window |
| `screen_capture` | Full or Standard | Capture Studio viewport |
| `inspect_instance` | Full | Inspect specific instance |
| `start_stop_play` | Full or Standard | Control play mode |

### Step 2: Determine Mode

**Full Mode (Community MCP — 20+ tools available):**
- Has: `execute_luau`, `search_asset`, `script_search`, `get_file_tree`, `inspect_instance`
- Capabilities: Live execution, Toolbox search, file browsing, instance inspection
- Preferred mode — all features work

**Standard Mode (Official Roblox MCP — ~6 tools):**
- Has: `execute_luau`, `insert_asset`, `get_console_output`
- Missing: `search_asset`, advanced inspection
- Workaround: Use known Asset IDs instead of Toolbox search

**Offline Mode (No MCP tools detected):**
- HALT. Output the stop message. Do not proceed.

---

## Stop Message (Offline Mode)

```
⛔ MCP Roblox Connection Not Found

I cannot build in Roblox Studio because the MCP Roblox server is not connected.

To fix this:
1. Open Claude Desktop Settings
2. Go to Developer → MCP Servers
3. Verify the Roblox Studio MCP server is listed and shows "Connected"
4. If disconnected: restart the rbx-studio-mcp server
5. If not listed: add it using the configuration in SETUP.md

Once MCP is reconnected, send your request again and I will proceed.
```

---

## Connection Verification Test

After detecting tools, optionally run a ping test to confirm Studio is responsive:

```luau
-- Send via execute_luau MCP tool
print("[Evilsoft-Skillblox] MCP connection verified. Studio is ready.")
```

If `get_console_output` returns the print statement → Studio is live and responsive.
If it returns nothing or an error → MCP tools exist but Studio is not open/active.

In the second case, output:

```
⚠️  MCP tools are available but Roblox Studio doesn't seem to be running
or no place is open.

Please:
1. Open Roblox Studio
2. Open or create a place
3. Publish the place (File > Publish to Roblox As) if not yet published
4. Enable HTTP Requests (File > Game Settings > Security > Allow HTTP Requests = On)
5. Check the Studio Output window shows: "The MCP Studio plugin is ready for prompts."

Then try again.
```

---

## MCP Tool Usage Quick Reference

### execute_luau
Runs a Luau script in the context of the Studio session.
```
execute_luau(code = "print('hello')")
```
Returns: console output

### insert_asset
Inserts a model from Roblox by Asset ID.
```
insert_asset(assetId = 12345678)
```
Returns: confirmation or error

### search_asset (Full mode only)
Searches Roblox Toolbox.
```
search_asset(query = "wooden table", assetType = "Model")
```
Returns: list of matching assets with IDs

### get_console_output
Reads recent Studio output window content.
```
get_console_output()
```
Returns: string of recent output lines

### screen_capture
Captures the current Studio viewport.
```
screen_capture()
```
Returns: image of current Studio view

### inspect_instance (Full mode only)
Inspects a specific instance in the DataModel.
```
inspect_instance(path = "workspace.Map_Example.Zone_Shop")
```
Returns: instance properties

---

## Common MCP Error Responses & Fixes

| Error | Cause | Fix |
|---|---|---|
| `execute_luau` times out | Studio is not open | Open Studio with a place |
| `insert_asset` returns 403 | Place not published | File > Publish to Roblox As |
| `search_asset` returns empty | Search term too specific | Use broader terms |
| All tools return errors | MCP server crashed | Restart rbx-studio-mcp process |
| HTTP error in Studio output | HTTP Requests disabled | Enable in Game Settings > Security |

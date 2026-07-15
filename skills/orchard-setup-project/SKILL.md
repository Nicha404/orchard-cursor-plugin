---
name: orchard-setup-project
description: Verify or repair the Orchard connection in Cursor and initialize Orchard project identity without duplicating plugin configuration. Use when the user asks whether Orchard is connected, asks to connect or configure Orchard, needs first-project setup, explicitly requests durable project instructions, or needs a manual fallback because the Marketplace MCP is unavailable.
---

# Connect Orchard in Cursor

Prefer the Marketplace-installed connection. It already provides the MCP server
and Orchard routing rule, so normal installation must not write duplicate
project configuration.

## Marketplace path

1. Verify that `orchard_storage` is available.
2. Call `orchard_storage` with `action: status`.
   - If authentication is required, direct the user to
     `Cursor Settings -> Tools & MCP -> orchard -> Authenticate`.
   - If the call succeeds, report the connected account and stop unless the
     user requested a project-scoped Orchard service.
3. Do not create `.cursor/mcp.json` or `AGENTS.md` just to connect the installed
   plugin.
4. For the first project-scoped Orchard request, when
   `.orchard/project.json` is missing:
   - Call `orchard_storage` with `action: register_project` and
     `project_name` equal to the current folder name.
   - Write the returned `persist.contents` exactly to `persist.path`.
   - Reuse the saved `project_id` for every later Orchard tool call.

## Durable project instructions

Only when the user explicitly requests project-level Orchard instructions,
create or update `AGENTS.md` in the project root.

- Reuse an existing `# Orchard MCP` section instead of adding a duplicate.
- Preserve all unrelated instructions exactly.
- Add the section below when it is missing.

```markdown
# Orchard MCP

Use Orchard MCP for:

- login / sign-in / accounts -> `orchard_auth`
  - Use Google auth through Orchard.
- app data / tables / records -> `orchard_database`
- file storage / uploads / downloads -> `orchard_storage`
- transactional email -> `orchard_email`
- deploy / publish / host the built frontend -> `orchard_deploy`

Reuse the `project_id` saved in `.orchard/project.json`.

For anything outside these services, implement normally.
```

## Manual MCP fallback

Use this only when the Marketplace MCP is unavailable and the user explicitly
asks for manual project configuration.

1. Locate the project root and inspect `.cursor/mcp.json` when it exists.
2. Create or update `.cursor/mcp.json`.
   - Preserve every existing MCP server and unrelated setting.
   - If an `orchard` server already exists, do not add a duplicate. Update only
     its URL when needed.
   - Otherwise, merge Orchard into the existing `mcpServers` object.
   - Ensure the resulting configuration contains:

     ```json
     {
       "mcpServers": {
         "orchard": {
           "url": "https://orchard-mcp.orchardagentic.workers.dev/mcp"
         }
       }
     }
     ```

   - Add only the URL. Never add tokens, API keys, authorization headers,
     provider credentials, or other secrets.
3. Tell the user to reload the current Cursor window so Cursor detects the new
   configuration:
   - Open the Command Palette with `Cmd+Shift+P` on macOS or `Ctrl+Shift+P` on
     Windows and Linux.
   - Run `Developer: Reload Window`.
   - Open `Cursor Settings -> Tools & MCP`, find `orchard`, enable it, and
     complete the connection if prompted.

## Boundaries

- Verify an Orchard tool call before claiming the connection works.
- Merge rather than replace `.cursor/mcp.json` or `AGENTS.md` when either file
  is explicitly requested.
- Respect explicit stop boundaries.
- Do not create cloud-provider accounts or request provider credentials.
- Do not expose Orchard runtime API keys in frontend code or commit them.

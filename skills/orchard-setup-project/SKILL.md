---
name: orchard-setup-project
description: Connect Orchard to the current Cursor Desktop project and add durable Orchard routing instructions. Use when the user asks to connect, install, configure, or set up Orchard; asks for Orchard project instructions; or needs .cursor/mcp.json and AGENTS.md prepared without overwriting existing project configuration.
---

# Set up Orchard for Cursor Desktop

Configure only the Orchard connection and project instructions. Preserve all
existing MCP servers, settings, and unrelated project guidance.

## Workflow

1. Locate the project root and inspect `.cursor/mcp.json` and `AGENTS.md` when
   they exist.
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
3. Create or update `AGENTS.md` in the project root.
   - If a `# Orchard MCP` section already exists, reuse and update that section
     instead of adding another one.
   - Preserve all unrelated instructions exactly.
   - If no Orchard section exists, add the section below.
4. After saving both files, stop. Do not modify application code or unrelated
   project files.
5. Tell the user to reload the current Cursor window so Cursor detects the new
   configuration:
   - Open the Command Palette with `Cmd+Shift+P` on macOS or `Ctrl+Shift+P` on
     Windows and Linux.
   - Run `Developer: Reload Window`.
   - Open `Cursor Settings -> Tools & MCP`, find `orchard`, enable it, and
     complete the connection if prompted.

## AGENTS.md section

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

## Project identity

- On the first project-scoped Orchard operation, use the appropriate Orchard
  tool to register or create the project.
- When the tool response returns a `persist` block, write its contents exactly
  to `.orchard/project.json` immediately.
- Reuse that `project_id` for every later Orchard tool call in the project.
- Verify that an Orchard tool is callable before claiming the connection works.

## Boundaries

- Merge rather than replace `.cursor/mcp.json` or `AGENTS.md`.
- Respect an explicit stop boundary such as "after saving both files, stop."
- Do not create cloud-provider accounts or request provider credentials.
- Do not expose Orchard runtime API keys in frontend code or commit them.

# Orchard for Cursor

Orchard gives Cursor projects managed authentication, a database, file storage,
transactional email, and static-site deployment through one OAuth-enabled MCP
connection.

Install the plugin, approve the Orchard sign-in, and ask Cursor to connect
Orchard to the current project. The included setup skill safely merges the
Orchard MCP URL into `.cursor/mcp.json` and adds durable Orchard routing guidance
to `AGENTS.md` without overwriting unrelated configuration.

Orchard manages the service setup so you do not need to create separate
provider accounts or paste infrastructure credentials into Cursor.

## Included components

- **MCP server:** connects Cursor to Orchard's five managed services.
- **Project setup skill:** creates or updates `.cursor/mcp.json` and `AGENTS.md`,
  preserving existing servers and instructions.
- **Always-on rule:** routes auth, data, storage, email, and deployment requests
  to the matching Orchard tool.

To run project setup, ask Cursor:

`Connect Orchard to this project for Cursor Desktop.`

After the two project files are saved, reload the Cursor window with
`Developer: Reload Window`, then enable `orchard` under
`Cursor Settings -> Tools & MCP` if needed.

## What Cursor can do with Orchard

- Add Google sign-in and user accounts
- Create tables and work with structured application data
- Store and serve uploads, images, and documents
- Send transactional email
- Publish static frontends to a public URL

## MCP connection

The plugin connects Cursor to Orchard's hosted MCP server:

```json
{
  "mcpServers": {
    "orchard": {
      "url": "https://orchard-mcp.orchardagentic.workers.dev/mcp"
    }
  }
}
```

Authentication uses the browser-based OAuth flow. Do not add tokens, API keys,
or provider credentials to this configuration.

## Example requests

- `Add Google login to this app.`
- `Create a table for customer feedback.`
- `Let signed-in users upload profile photos.`
- `Send a welcome email after signup.`
- `Publish this static site.`

## Pricing

The Cursor plugin and MCP connection are free to install. Orchard service plans
and usage charges may apply to the managed backend resources used by a project.
See the [Orchard pricing page](https://orchard-dashboard.pages.dev/pricing.html)
for current details.

## Privacy, terms, and support

- [Privacy Policy](https://orchard-dashboard.pages.dev/privacy.html)
- [Terms of Service](https://orchard-dashboard.pages.dev/terms.html)
- [Orchard dashboard](https://orchard-dashboard.pages.dev)
- [GitHub issues](https://github.com/Nicha404/orchard-cursor-plugin/issues)

## License

The plugin packaging and configuration in this repository are available under
the MIT License. The hosted Orchard service is governed by the Orchard Terms of
Service.

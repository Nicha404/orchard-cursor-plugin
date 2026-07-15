# Orchard for Cursor

Orchard gives Cursor projects managed authentication, a database, file storage,
transactional email, and static-site deployment through one OAuth-enabled MCP
connection.

Install the plugin, approve the Orchard sign-in, and start asking Cursor for the
managed service you need. The plugin supplies the MCP connection and routing
instructions in one installation; no project-level MCP file or API key is
required.

Orchard manages the service setup so you do not need to create separate
provider accounts or paste infrastructure credentials into Cursor.

## Included components

- **MCP server:** connects Cursor to Orchard's five managed services.
- **Always-on rule:** routes auth, data, storage, email, and deployment requests
  to the matching Orchard tool and provides the persistent guidance that would
  otherwise require project-level instructions.

## Install

1. Install Orchard from the Cursor Marketplace.
2. Open `Cursor Settings -> Tools & MCP`, select `orchard`, and approve the
   Google sign-in when prompted.
3. Ask Cursor for authentication, data, storage, email, or deployment.

On the first project-scoped request, Cursor registers the current folder and
saves the returned non-secret project identity in `.orchard/project.json`.
Every later request reuses that `project_id`.

To verify the connection, ask Cursor:

`Check whether Orchard is connected to this project.`

Neither `.cursor/mcp.json` nor `AGENTS.md` is required for a normal Marketplace
installation. The plugin-supplied rule provides the Orchard routing instructions
without modifying the user's project files.

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
- [Orchard dashboard](https://www.orchardagentic.cloud/)
- [GitHub issues](https://github.com/Nicha404/orchard-cursor-plugin/issues)

## License

The plugin packaging and configuration in this repository are available under
the MIT License. The hosted Orchard service is governed by the Orchard Terms of
Service.

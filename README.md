# Adobe Acrobat Sign MCP server

Inspect signature agreements and prepare a DRAFT from existing document references without sending invitations.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `ADOBE_SIGN_ACCESS_TOKEN`
- `ADOBE_SIGN_SHARD`



Credential help: https://helpx.adobe.com/sign/kb/how-to-create-an-integration-key.html

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call adobe_sign_list_agreements '{}'
```

## Use with an MCP client

Launch `node /absolute/path/adobe-acrobat-sign-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| adobe_sign_list_agreements | Read | adobe sign list agreements |
| adobe_sign_get_agreement | Read | adobe sign get agreement |
| adobe_sign_create_draft | Explicit approval required | Create a DRAFT agreement using existing document references; does not send signature invitations. |

## Concrete workflow

Inspect signature agreements and prepare a DRAFT from existing document references without sending invitations.

1. adobe_sign_list_agreements
2. adobe_sign_get_agreement
3. adobe_sign_create_draft

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Import with PipMCP](https://pipmcp.com/github/start?integration=openapi-to-mcp&utm_source=github&utm_campaign=github-adobe-acrobat-sign-mcp&utm_content=readme) when you want the hosted service. This provider is not currently listed as a managed template. Import selected-openapi.json (REST) or the official GraphQL schema linked in provenance, configure authentication, and review the tools before execution. Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/adobe-acrobat-sign/).

## Provenance and maintenance

- https://secure.na1.adobesign.com/restapijson/v6/restapi.json

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.

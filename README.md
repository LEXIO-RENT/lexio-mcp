# Lexio MCP server

Official remote [Model Context Protocol](https://modelcontextprotocol.io) server of **[Lexio](https://lexio.rent/logiciel-location-voiture)**, the vehicle rental management software for rental companies in France.

It lets the owner of a Lexio account ask an AI assistant such as Claude or ChatGPT about their rental agency, in natural language: vehicle availability, rentals, customers, fleet, maintenance, catalog and pricing.

- **Presentation:** https://lexio.rent/mcp
- **Technical documentation:** https://docs.lexio.rent/mcp

This repository only describes the server. The server is hosted and operated by Lexio; its source code is not published here.

## Connect

| | |
|---|---|
| Server URL | `https://api.lexio.rent/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth 2.1: authorization code with PKCE (S256), Client ID Metadata Documents |
| Access | Read-only |

1. In your MCP client, add a custom connector with the server URL above.
2. Sign in to Lexio, choose the organization and review the requested read scopes, then authorize.
3. Ask your question.

Requirements: a Lexio plan that includes the API (Business today). Only the owner of the organization can connect. The product and its data are mainly in French.

### Claude Code

```bash
claude mcp add --transport http lexio https://api.lexio.rent/mcp
```

Or install it as a plugin from this repository (`.claude-plugin/`).

## Tools

43 read-only tools, one per read operation of the [Lexio external API](https://docs.lexio.rent), all annotated `readOnlyHint: true`:

- **Availability and rentals:** availability search, rentals, contracts, amendments, inspections and photos, invoices, payments, events
- **Customers**
- **Fleet:** vehicles, maintenance records and maintenance alerts, vehicle blocks
- **Catalog:** categories, options, deductibles, deposits, mileage packages, locations
- **Pricing:** pricing settings, seasons and season calendar, duration discounts, lead-time tiers
- **Organization** settings

The assistant cannot create, change or delete anything in Lexio.

## Example questions

- *Quels véhicules sont libres ce week-end ?* (Which vehicles are free this weekend?)
- *Quels départs sont prévus demain matin ?* (Which departures are planned tomorrow morning?)
- *Quels entretiens sont en retard sur la Peugeot 208 ?* (Which maintenance items are overdue on the Peugeot 208?)

## Security and privacy

- Each connection gives access to one organization only, chosen on the consent screen, and to the read scopes granted there.
- Permissions are checked again on every request. Access can be revoked at any time in Lexio under *Paramètres › Intégrations › Assistants IA*.
- Access tokens last 10 minutes. The assistant never sees the password.
- Data that is read, including the rental company's customer contact details, is sent to the provider of the assistant.

Privacy policy: https://lexio.rent/politique-de-confidentialite

## Support

contact@lexio.rent · https://lexio.rent/contact

## License

The files in this repository (documentation and configuration) are under the MIT license. The Lexio service is proprietary and subject to its [terms](https://lexio.rent/cgv).

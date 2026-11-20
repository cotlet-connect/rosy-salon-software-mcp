# Rosy Salon Software MCP server for ChatGPT and Claude

Rosy Salon Software has a published API covering reads across appointments, clients, employees, services and tickets, plus selected creation endpoints. The Cotlet.dev page checked 12 November 2026 found no official Rosy MCP server or ChatGPT or Claude connector. Cotlet.dev connects your AI agent to your own signed-in Rosy Salon Software Cloud Browser for appointment schedules, client records, inventory and salon sales. Your account permissions determine access, and tools marked Asks first wait for your approval.

## What you can ask

> Read a stylist's appointments for tomorrow

> Find the client's previous services

> Check the products recorded in inventory

> Review the salon's sales figures

> Prepare a selected appointment change

> Find client records before a follow-up

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev. No API key needed.

### Claude

Settings > Connectors > Add custom connector: `https://cotlet.dev/mcp/v1/connect`. Sign in to Cotlet.dev.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Rosy Salon Software tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"rosy-salon-software":{"command":"uvx","args":["--from","git+https://github.com/cotlet-connect/rosy-salon-software-mcp","rosy-salon-software-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t rosy-salon-software-mcp .
docker run -i --rm -e COTLET_API_KEY rosy-salon-software-mcp
```

Tools: `rosy_salon_software_guide`, `rosy_salon_software_status`, `rosy_salon_software_open`, `rosy_salon_software_read`, `rosy_salon_software_click`, `rosy_salon_software_type`, `rosy_salon_software_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From this repository:

```bash
pip install git+https://github.com/cotlet-connect/rosy-salon-software-mcp
rosy-salon-software-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 rosy_salon_software_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 rosy_salon_software_agent.py status    # is Rosy Salon Software ready in your Cotlet.dev account
python3 rosy_salon_software_agent.py guide     # Rosy Salon Software screens and sign-in link
python3 rosy_salon_software_agent.py read      # open Rosy Salon Software, read the page, close the browser
python3 rosy_salon_software_agent.py tools     # list Cotlet.dev tools
python3 rosy_salon_software_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Rosy Salon Software users

**Does Rosy Salon Software have an API or MCP server?**

Rosy's published API covers reads across appointments, clients, employees, services and tickets, plus selected creation endpoints. It does not document the complete salon screen edit and checkout workflow. The Cotlet.dev page checked 12 November 2026 found no official Rosy MCP server or ChatGPT or Claude connector.

**How do I connect Rosy Salon Software to ChatGPT?**

Sign up at https://cotlet.dev/signup?app=rosy-salon-software, open Rosy Salon Software in your Cotlet.dev Cloud Browser and sign in at app.salonrunner.com/manager/login.htm. Enable it for agents, add https://cotlet.dev/mcp/v1/connect in ChatGPT and authenticate with OAuth.

**How do I connect Rosy Salon Software to Claude?**

Add https://cotlet.dev/mcp/v1/connect as a custom connector in Claude and sign in to Cotlet.dev. Enable Rosy Salon Software in your console and refresh the connector.

**What happens when I edit a recurring appointment?**

The page states that editing a standing series changes only the selected occurrence. Check the client, service and stylist before approving the proposed change.

**Is this an official Rosy Salon Software server?**

No. Cotlet.dev is independent and is not affiliated with Rosy Salon Software. Access follows your signed-in role and enabled Rosy features.

## Live integration page

https://cotlet.dev/integrations/rosy-salon-software-api-mcp-server

---

More: https://cotlet.dev/integrations/rosy-salon-software-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=rosy-salon-software

Start free: https://cotlet.dev/signup?app=rosy-salon-software&utm_source=github&utm_medium=readme&utm_campaign=rosy-salon-software

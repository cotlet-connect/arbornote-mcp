# ArborNote MCP server for ChatGPT and Claude

Connect ChatGPT, Claude and any AI agent to your ArborNote account through Cotlet.dev. The hosted integration offers 28 operations for tree inventories, proposals, estimator visits, crew work orders and invoices.

## What can I ask?

> Show overdue proposal reminders.

> Draft a General Tree Care proposal from the trees I select, and save it after my approval.

> Schedule an approved proposal as a crew work order after I confirm the date and resources.

> Create an invoice from a proposal and save it without emailing it.

## Connect ChatGPT and Claude

1. [Get access](https://cotlet.dev/signup?app=arbornote).
2. Turn on ArborNote in the Cotlet.dev console and sign in to https://app.arbor-note.com/ in your Cloud Browser.
3. Add `https://cotlet.dev/mcp/v1` in your agent and sign in with Cotlet.dev. The live guide has the current client-specific setup.

For Codex, Claude Code and other clients using an API key, create a key in the Cotlet.dev console and use this configuration:

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

## Hosted operations

The live page documents these operations through `arbornote_read` and `arbornote_write`:

- `manage_projects`
- `clone_project`
- `archive_projects`
- `share_project`
- `map_trees`
- `manage_tree_groups`
- `move_trees`
- `restore_trees`
- `export_inventory`
- `import_inventory_ai`
- `manage_landscape_inventory`
- `get_map_link`
- `set_tree_treatments`
- `manage_treatment_catalog`
- `manage_multi_year_plans`
- `manage_gtc_proposals`
- `manage_phc_proposals`
- `manage_proposal_reminders`
- `ask_sales`
- `view_sales_dashboard`
- `run_project_reports`
- `schedule_estimator_appointment`
- `schedule_work_order`
- `manage_job_requirements`
- `manage_extra_work`
- `manage_crew_hours`
- `manage_clients`
- `create_invoice`

Read operations run without confirmation. Write operations ask for confirmation by default; this can be changed per tool. Sending a proposal or emailing an invoice reaches your client, so review the action first.

## Run the local stdio bridge

This repository contains a Python bridge that forwards calls to Cotlet.dev. Python 3.10 or newer is required. It uses the standard library.

```bash
export COTLET_API_KEY="your-key"
python3 arbornote_agent.py serve
```

The local bridge lists seven browser helper tools: `arbornote_guide`, `arbornote_status`, `arbornote_open`, `arbornote_read`, `arbornote_click`, `arbornote_type` and `arbornote_close`. Use the hosted connector for the application operations documented above. The local helper list and the hosted operation list serve different purposes.

```bash
docker build -t arbornote-mcp .
docker run -i --rm -e COTLET_API_KEY arbornote-mcp
```

Without `COTLET_API_KEY`, a tool call returns instructions for obtaining a key. Keep your key out of source control.

## Does ArborNote have an API?

The live guide, checked 16 November 2026, describes the Enterprise-only ArborNote Open API. It reads clients, projects, proposals, work orders, appointments and crew hours, and supports selected client, project and proposal updates. It does not create proposals, schedule work, map trees or create invoices. If the official API covers your task, use it first.

## Is this affiliated with ArborNote?

Cotlet.dev is independent and is not affiliated with, endorsed by or sponsored by ArborNote. ArborNote is a trademark of its owner. You use your own ArborNote account, and your user permissions and plan apply.

[Full ArborNote guide](https://cotlet.dev/integrations/arbornote-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=arbornote)

[Get access](https://cotlet.dev/signup?app=arbornote)

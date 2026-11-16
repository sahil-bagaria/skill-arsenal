---
name: n8n-workflows
description: Find, adapt, and assemble n8n automation workflows from a local library of 2,061 real workflow templates covering 365+ integrations. Use when the user wants to automate something with n8n, asks for an n8n workflow, template, or example, mentions connecting two services with n8n, wants to see how an n8n node is wired up, or needs a starting point for an automation involving webhooks, schedules, or app triggers. Also use when the user asks what n8n can integrate with. Do NOT use for non-n8n automation (Zapier, Make, Airflow) unless the user wants an n8n equivalent.
---

# n8n Workflow Library

A local collection of **2,061 production n8n workflows** across **188 node/integration folders**. Search it before writing any n8n workflow from scratch — a close match almost always exists and adapting one is faster and more reliable than authoring blind.

**Library root:** `~/.claude/skill-repos/n8n-workflows/workflows/`

## How the library is organised

```
workflows/<Folder>/<id>_<Service1>_<Service2>_<Purpose>_<Trigger>.json
```

Example: `workflows/Airtable/1120_Airtable_Mindee_Automate_Webhook.json`

Two things about folder names that will trip you up if you assume otherwise:

- Folders are named after the **primary node type**, not always the app. That is why the largest folders are `Manual` (391), `Splitout` (194), `Code` (183), `Http` (176) — these are structural nodes, not integrations. App folders like `Telegram` (119) and `Googlesheets` (26) also exist.
- Because of that, **never rely on the folder alone**. Always search filenames across all folders.

Trigger suffixes tell you how a workflow starts: `Webhook` (997), `Triggered` (735), `Scheduled` (275), plus a few `Automate`, `Create`, `Send`, `Process`.

## Search strategy — cheapest first

**1. Filename search across everything.** Fastest and usually enough. Case-insensitive, matches service names.

```bash
cd ~/.claude/skill-repos/n8n-workflows/workflows
ls */*.json | grep -i slack
ls */*.json | grep -i -e telegram -e openai     # either service
ls */*.json | grep -i slack | grep -i sheets    # both services
ls */*.json | grep -i "_Scheduled\.json$"       # by trigger type
```

**2. Node-type search when the filename does not say enough.** Workflow names do not always list every node, so grep the JSON for the actual node type.

```bash
grep -rl "n8n-nodes-base.slack" . | head -20
grep -rl "n8n-nodes-base.openAi" . | head -20     # AI workflows (32 files)
```

**3. Content search for a concept** — an API host, a field name, a specific operation.

```bash
grep -rli "hubspot" . | head -20
```

This collection largely predates n8n's LangChain node namespace — only 6 files use `n8n-nodes-langchain`. AI workflows here are built on `n8n-nodes-base.openAi`. If the user wants a modern AI Agent workflow, expect to build it rather than find it.

Report how many matches you found before narrowing. If a search returns nothing, say so plainly and offer to build the workflow from scratch rather than forcing a poor match.

## Reading a workflow

Files are standard n8n exports: `name`, `nodes`, `connections`, `settings`, `tags`.

Do not dump a whole JSON into the conversation — some run to thousands of lines. Summarise the shape first:

```bash
python3 -c "
import json
d = json.load(open('WORKFLOW.json'))
print(d['name'], '—', len(d['nodes']), 'nodes')
for n in d['nodes']:
    print(' ', n['type'].replace('n8n-nodes-base.',''), '·', n['name'])
"
```

Then read only the nodes that matter for the user's question.

## Delivering a workflow

Give the user the complete JSON as a file they can import, not pasted into chat unless it is small. Then tell them: **n8n → Workflows → Import from File**.

Always state, without being asked:

- **Credentials do not transfer.** Nodes reference credential IDs from the original author's instance. The user must re-select their own credentials on every node that touches an external service.
- **These are community-contributed.** Read what a workflow does before running it, especially anything with `httpRequest` nodes hitting unfamiliar hosts, or `Code` nodes.
- Any webhook URLs, spreadsheet IDs, channel names, or hardcoded IDs are the original author's and need replacing.

When you adapt a workflow, say exactly what you changed from the original.

## Combining and building

For a request no single workflow covers, it is usually right to take the trigger section from one workflow and the action section from another. Say which files you drew from so the user can check your sources.

Keep node `name` values unique inside a workflow — `connections` is keyed by node name, so duplicates silently break the graph.

## Updating the library

```bash
git -C ~/.claude/skill-repos/n8n-workflows pull
```

This skill lives outside that clone, so pulling never overwrites it.

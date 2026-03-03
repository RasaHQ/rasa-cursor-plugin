# Rasa Cursor Plugin

A [Cursor](https://cursor.com) plugin that adds [Rasa CALM](https://rasa.com/docs/) agent skills so the AI can help you build flows, configure assistants, write custom actions, manage slots, and more—following Rasa’s conventions and docs.

## Installing the plugin

- **From the Cursor Marketplace** (when published): Open **Settings** (e.g. **Cmd+Shift+J**), go to **Rules**, and install the **Rasa Cursor Plugin** from the marketplace.
- **From this repo**: Install the plugin from this GitHub repo (Cursor can install from a Git repository). You can also clone the repo and add the folder as a local plugin source in Cursor.

After installation, the plugin’s skills show up under Cursor’s **Rules** settings.

## Using the skills in Cursor

- **Agent Decides**: By default, skills are in the **Agent Decides** group. Cursor will use them when your request matches the skill’s description (e.g. “add a flow for booking” → building flows, “write a custom action to call our API” → custom actions).
- **Invoke manually**: In chat you can run a skill by name, e.g. `/rasa-building-flows` or `/rasa-writing-custom-actions`. Use **Tab** to see skill names after typing `/`.

**Example prompts:**

- *“Create a flow for booking an appointment”*
- *“Add a custom action to fetch order status from our API”*
- *“Set up enterprise search with Qdrant”*
- *“Write E2E tests for the transfer money flow”*

## Skills included

Skills are synced from [rasa-agent-skills](https://github.com/RasaHQ/rasa-agent-skills). They currently cover:

- **rasa-building-flows** — Conversation flows in YAML  
- **rasa-configuring-assistant** — `config.yml`, `endpoints.yml`, pipeline, policies  
- **rasa-configuring-model-groups** — LLM and embedding providers, routing, failover  
- **rasa-managing-slots** — Slot types, mappings, validation  
- **rasa-rephrasing-responses** — Contextual Response Rephraser  
- **rasa-setting-up-enterprise-search** — RAG, vector stores, `EnterpriseSearchPolicy`  
- **rasa-writing-custom-actions** — Python actions with the Rasa SDK  
- **rasa-writing-e2e-tests** — E2E test cases and assertions  
- **rasa-writing-responses** — Response templates, variations, rich responses  

## For maintainers: how skills are updated

Skills are maintained in [rasa-agent-skills](https://github.com/RasaHQ/rasa-agent-skills). This plugin repo stays in sync via CI:

- **Sync workflow** (this repo): [Sync skills from agent-skills](.github/workflows/sync-skills.yml) runs on `repository_dispatch` or manually (**Actions → Sync skills from agent-skills → Run workflow**). It copies `skills/` from rasa-agent-skills and opens a **PR to main**; merge that PR to publish updates.
- **Trigger** (rasa-agent-skills): Pushes to `main` that change `skills/**` can send `repository_dispatch` to this repo. To enable that, add secret **CURSOR_PLUGIN_DISPATCH_TOKEN** in rasa-agent-skills (PAT with access to this repo: classic **repo** or **public_repo**, or fine-grained **Contents** + **Metadata** on this repository).

## License

Apache-2.0

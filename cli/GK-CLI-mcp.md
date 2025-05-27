---

title: MCP
description: Use your MCP connectors with GitKraken CLI. 
taxonomy:
    category: cli

---


### Use MCP (Model Context Protocol) to connect your AI agent to GitKraken CLI 

MCP (Model Context Protocol) allows you to connect your GitKraken CLI to your LLM (Large Language Model) program. With this enabled you can manage your PRs, Issues, Work Items and more directly from your AI Desktop Agent. 

### MCP Setup

GitKraken CLI will connect locally with most LLMs by setting an MCP arguement. Please see the string below:

```json
{
  "mcpServers": {
    "gitkraken": {
      "command": "gk",
      "args": ["mcp"]
    }
  }
}

```
***

### Example Integrations

#### Claude

* Navigate to **Settings** by using the sidebar or keyboard shortcuts
* On the pop out window select the **Developer** tab
* Select **Edit Config** and open the *claude_desktop_config* json file
* Add the following string to the JSON file
```json

{
  "mcpServers": {
    "gitkraken": {
      "command": "gk",
      "args": ["mcp"]
    }
  }
}

```

#### Windsurf
* Locate the `mcp_config.json` file, usually located at `~/.codeium/windsurf/mcp_config.json`
* Add GitKraken CLI to the JSON with the following string: 

```json
{
  "mcpServers": {
    "gitkraken": {
      "command": "gk",
      "args": ["mcp"]
    }
  }
}

```

#### GitHub Copilot

* Click the Copilot Icon
* On the new menu, select `Edit Preferences`
* In the left panel, expand `Copilot Chat` and click `MCP`
* In the Json file add the following string

```json
{
    "servers": {
        "gitkraken": {
            "type": "stdio",
            "command": "gk",
            "args": ["mcp"]
        }
    }
}

```




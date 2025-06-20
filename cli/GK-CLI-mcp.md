---
title: MCP (Model Context Protocol)
description: Learn how to connect GitKraken CLI with AI agents using MCP.
taxonomy:
    category: cli
---
<kbd>Last updated: June 2025</kbd>

### Use MCP (Model Context Protocol) to connect your AI agent to GitKraken CLI

**Model Context Protocol (MCP)** allows you to connect your GitKraken CLI to your **Large Language Model (LLM)** program. With this enabled, you can manage your PRs, Issues, Work Items, and more directly from your AI Desktop Agent.

###  Pre Installation Checklist 

1.  Download the [GitKraken CLI](https://www.gitkraken.com/cli)
2.  Follow the GitKraken CLI [Installation Guide](https://help.gitkraken.com/cli/cli-home/)
3.  Authenticate to your [GitKraken Account](https://help.gitkraken.com/cli/cli-home/#get-started-with-gitkraken-cli)
4.  Synchronize your [GitKraken Integrations](https://help.gitkraken.com/cli/cli-home/#synchronize-your-integrations) with the CLI 

Please see our [MCP blog post](https://www.gitkraken.com/blog/introducing-gitkraken-mcp) with example workflows that can be enabled with this powerful tool. 

---

### MCP Setup

GitKraken CLI will connect locally with most LLMs by setting an MCP arguement. Please see the string below:


```
{
  "mcpServers": {
    "gitkraken": {
      "command": "gk",
      "args": ["mcp"]
    }
  }
}
```

---

### Example Integrations

#### Claude

1. Open **Settings** from the sidebar or use keyboard shortcuts.
2. Select the **Developer** tab in the pop-up window.
3. Click **Edit Config** to open the `claude_desktop_config` JSON file.
4. Add the following MCP configuration:

```
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

1. Locate the `mcp_config.json` file. The default path is `~/.codeium/windsurf/mcp_config.json`.
2. Add the GitKraken CLI entry:

```
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

1. Click the Copilot icon.
2. Select **Edit Preferences** from the menu.
3. In the left panel, expand **Copilot Chat** and click **MCP**.
4. Add the following to the JSON configuration file:

```
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



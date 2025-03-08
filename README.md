# MCP Ripgrep Server

An MCP server that provides ripgrep (rg) search capabilities to any MCP client such as Claude.

## Overview

This server provides a Model Context Protocol (MCP) interface for the powerful [ripgrep](https://github.com/BurntSushi/ripgrep) search tool. It enables Claude AI and other MCP-compatible clients to perform high-performance text searches across files on your system.

## Prerequisites

- Node.js (v18 or higher)
- ripgrep (`rg`) command installed and available in your PATH. Install it with `brew install ripgrep` on macOS.

## Usage with Claude for Desktop

To use this MCP server with Claude for Desktop:

1. Edit your Claude for Desktop configuration file:
   - macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - Windows: `%APPDATA%\Claude\claude_desktop_config.json`

2. Add the following to your configuration:
   ```json
   {
     "mcpServers": {
       "ripgrep": {
         "command": "npx",
         "args": ["-y", "mcp-ripgrep@latest"]
       }
     }
   }
   ```
   
   Replace `/path/to/mcp-ripgrep` with the absolute path to where you cloned this repository.

3. Restart Claude for Desktop.

## Available Tools

### search

Basic search with ripgrep:

```
Pattern: error
Path: ./src
```

### advanced-search

More advanced search with additional options:

```
Pattern: function
Path: ./src
FixedStrings: true
FileType: ts
IncludeHidden: false
```

### count-matches

Count occurrences of a pattern:

```
Pattern: TODO
Path: ./src
CountLines: true
```

### list-files

List files that would be searched without actually searching them:

```
Path: ./src
FileType: js
```

### list-file-types

List all supported file types in ripgrep.

## Security Considerations

This MCP server executes shell commands using the ripgrep tool. While efforts have been made to safely escape arguments, use caution when providing input as it runs commands on your machine.

## License

MIT

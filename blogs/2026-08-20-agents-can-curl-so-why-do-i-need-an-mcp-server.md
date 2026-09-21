---
title: "Agents Can Curl, So Why Do I Need an MCP Server?"
url: "http://apievangelist.com/2026/08/20/agents-can-curl-why-do-i-need-an-mcp-server/"
date: "2026-08-20"
feed_url: "https://apievangelist.com/atom.xml"
---
Here is a question I get asked more than any other right now, usually by an engineer who is a little annoyed and entirely correct to be asking it: if the agent can already read my OpenAPI and just make the HTTP call itself, why do I need to stand up an MCP server at all? Agents can curl. A modern model, handed a decent API description, can figure out the endpoint, assemble the request, send it, and read the response back without any of the ceremony of a Model Context Protocol server sitting in the middle.

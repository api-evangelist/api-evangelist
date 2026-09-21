---
title: "The MCP Authentication and Authorization Gap"
url: "http://apievangelist.com/2026/09/03/the-mcp-authentication-and-authorization-gap/"
date: "2026-09-03"
feed_url: "https://apievangelist.com/atom.xml"
---
The part of the MCP story that keeps me up at night is not the tools, the prompts, or the discovery. It is authentication and authorization, because that is the part where the gap between how it should be done and how it is actually being done right now is widest, and the consequences of getting it wrong are the most severe. We are wiring language models into production systems at a speed that would have been reckless even for human-driven integrations, and a large share of the MCP servers going live are handling identity and access in ways that range from naive to genuinely dangerous.

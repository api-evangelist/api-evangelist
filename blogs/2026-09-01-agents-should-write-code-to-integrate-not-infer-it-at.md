---
title: "Agents Should Write Code to Integrate, Not Infer It at Runtime"
url: "http://apievangelist.com/2026/09/01/agents-should-write-code-to-integrate-not-infer/"
date: "2026-09-01"
feed_url: "https://apievangelist.com/atom.xml"
---
Here is the strongest opinion I hold about agents and APIs right now, and I know it cuts against the mood of the moment: for most real integrations, you do not want the agent inferring what an API said at runtime through MCP. You want the agent to write deterministic code that integrates with the API, once, that you can read, test, and run a thousand times with identical behavior. The agent as a runtime interpreter of your APIs is a seductive idea and, for a lot of production work, a bad one.

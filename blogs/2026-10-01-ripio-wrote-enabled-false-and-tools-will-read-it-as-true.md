---
title: "Ripio Wrote enabled false And Tools Will Read It As True"
url: "http://apievangelist.com/2026/10/01/ripio-wrote-enabled-false-and-tools-will-read-it-as-true/"
date: "2026-10-01"
feed_url: "https://apievangelist.com/atom.xml"
---
This is the last post in a series about OpenAPI vendor extensions, and I saved it for the end because it is the one that turns an argument about tidiness into an argument about a bug. Ripio, a Latin American cryptocurrency exchange, uses x-mcp on their operations: x-mcp: enabled: false An object, with a single field, set to false. Ripio is marking this operation as not exposed to agents.

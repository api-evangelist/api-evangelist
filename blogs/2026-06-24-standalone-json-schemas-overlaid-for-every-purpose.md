---
title: "Standalone JSON Schemas, Overlaid for Every Purpose"
url: "https://apievangelist.com/2026/06/24/standalone-json-schemas-overlaid-for-every-purpose/"
date: "2026-06-24"
author: "Kin Lane"
feed_url: "https://apievangelist.com/atom.xml"
---
Yesterday I wrote about localizing the Products API with OpenAPI overlays , treating the whole API description as one document to be translated four ways. Today I want to go down a level, because the more interesting structural decision in that little Products API template isn’t the OpenAPI at all — it’s that the data models don’t actually live inside the OpenAPI. They live next to it, as standalone JSON Schema files, and that single choice is what makes everything else flexible.

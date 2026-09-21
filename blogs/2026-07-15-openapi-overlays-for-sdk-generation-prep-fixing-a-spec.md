---
title: "OpenAPI Overlays for SDK Generation Prep: Fixing a Spec Before Codegen"
url: "http://apievangelist.com/2026/07/15/openapi-overlays-for-sdk-generation-prep/"
date: "2026-07-15"
feed_url: "https://apievangelist.com/atom.xml"
---
Every time I run a code generator against a real OpenAPI document, the output tells me something ugly about how the spec was written. I get a method called get_products hanging off a client with no namespace, a status field typed as a loose string so the SDK hands me a stringly-typed free-for-all, and operations scattered flat across the client because nobody tagged them. That is not the generator’s fault.

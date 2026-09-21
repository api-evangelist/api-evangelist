---
title: "OpenAPI Overlays for Deprecation and Migration Choreography"
url: "http://apievangelist.com/2026/08/14/openapi-overlays-for-deprecation-and-migration-choreography/"
date: "2026-08-14"
feed_url: "https://apievangelist.com/atom.xml"
---
Deprecation is where most API programs quietly fall apart. Not because teams don’t know how to sunset an operation, but because they do it by hand, one operation at a time, across a dozen specs, on whatever day someone finally gets to it. Somebody sets deprecated: true in one place, forgets the Sunset header in another, writes “please migrate soon” in a description here and “this endpoint is going away” there, and six weeks later nobody can tell you which version of the truth is actually live.

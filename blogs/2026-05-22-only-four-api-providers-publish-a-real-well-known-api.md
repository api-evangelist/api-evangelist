---
title: "Only Four API Providers Publish a Real .well-known/api-catalog Right Now"
url: "http://apievangelist.com/blog/2026/05/22/four-providers-publishing-well-known-api-catalog/"
date: "2026-05-22"
feed_url: "https://apievangelist.com/atom.xml"
---
RFC 9727 has been a published IETF standard for over a year. It defines /.well-known/api-catalog as the machine entrypoint for discovering an organization’s APIs — a small, boring, eminently useful primitive. An agent (or a developer, or a tool) does a GET against that path, gets back an application/linkset+json document, and finds the URLs of every OpenAPI, AsyncAPI, or other spec the provider publishes.

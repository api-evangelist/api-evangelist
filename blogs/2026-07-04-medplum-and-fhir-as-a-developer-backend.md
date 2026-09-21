---
title: "Medplum and FHIR as a Developer Backend"
url: "http://apievangelist.com/2026/07/04/medplum-and-fhir-as-a-developer-backend/"
date: "2026-07-04"
feed_url: "https://apievangelist.com/atom.xml"
---
Medplum treats FHIR R4 as a developer backend, exposing the RESTful API as a generic create, read, update, search, and history surface parameterized by resource type. That generality is powerful, but it also means the meaningful workflows are entirely about how you sequence those generic operations—and that is precisely the kind of thing worth writing down as Arazzo so it does not stay locked in tribal knowledge. There were already several Medplum workflows in my catalog from an earlier pass—upserting a patient, registering a patient with an observation, scheduling an encounter, finalizing an 

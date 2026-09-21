---
title: "RFC 10008 Left A Slot Open And Somebody Is Standing In It"
url: "http://apievangelist.com/2026/09/03/rfc-10008-left-a-slot-open-and-somebody-is-standing-in-it/"
date: "2026-09-03"
feed_url: "https://apievangelist.com/atom.xml"
---
Every API I have ever catalogued eventually grows a search endpoint, and every one of them has had to lie to get it. You cannot put a real filter in a URL — you hit length limits, you leak your parameters into access logs and referrer headers, and you cannot express nesting at all. So you do what everyone does and reach for POST /resource/search.

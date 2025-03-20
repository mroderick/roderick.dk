---
date: '2010-02-26T00:00:00+0000'
title: 'IE8 Getting EcmaScript 262 rev. 5 Compliant Native JSON'
tags: ['JavaScript']
aliases: /2010/02/26/ie8-getting-ecmascript-262-rev5-compliant-native-json/
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: false
# description: "Desc Text."
# canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: false
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
# cover:
#     image: "<image path/url>" # image path/url
#     alt: "<alt text>" # alt text
#     caption: "<text>" # display caption under cover
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
---

Earlier this week, Microsoft posted an article with details on udpates to the native JSON implementation in IE8.

> Because of the new ECMAScript specification changes, some customers have reported issues. These issues are caused by deviations between the native JSON feature in Internet Explorer 8 and the final specification. An update is now available to address these customer issues and improve JSON interoperability of Internet Explorer 8. This update enables JSON interoperability of Internet Explorer 8 to keep in conformance with the new "ECMAScript, fifth edition" standard specification.

According to the [Microsoft Knowledgebase article](http://support.microsoft.com/kb/976662), these updates are already being pushed via Windows Update to Windows versions with IE8 support.

Getting standards compliant native JSON support in what is soon to become the most popular browser on the planet, will certainly make lives easier for everyone working with JSON in browsers, and will help keep our JavaScript frameworks lean and fast.

## Why should I care?

This update might seem like small potatoes at first sight, but this update hints at something much, much bigger.

To my knowledge, this is the first time that Microsoft have fixed non-compliant implementations in published versions of Internet Explorer. It also means that IE8 wont' be bug-for-bug compatible between builds, which is perfectly acceptable to me. Developers deal with browser inconsistencies every day, but it's not every day we get news as significant as this.

This shift in strategy, could actually mean that Microsoft plan on continually updating the current Internet Explorer with smaller enhancements, and leave the previous strategy of only improving standards support with a new generation of IE.

Who knows, they might even be planning a v8.1 of Internet Explorer, with even more significant upgrades to standards support?

---
date: '2008-11-20T00:00:00+0000'
title: 'How to create un-indexable content for missing javascript warnings'
tags: ['Web', 'Work']
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

At Gazebo we love to use unobtrusive enhancement to make our solutions available to the biggest possible audience, and greatly improve the experience for users with sophisticated user-agents.

This usually means:

* Create semantic, valid markup, which can be read by any browser, including phones
* Add styling via CSS, to make it look nice in modern, sophisticated browsers
* Sprinkle a little javascript, to make it all *behave* nicely for supported user-agents


To control decoration, when javascript IS available, I usually add `js-enabled` or something similar to the classname of the `<body>` element. This allows me differentiate the styling of widgets for when javascript is available, and allows a controlled fallback decoration, for when it is not.


This is all nice and dandy, but sometimes javascript IS a fundamental requirement of your application, and then it's a whole different mess of issues. This post will give you the details on how to deal with one of these issues.

## Avoiding getting your warnings indexed by search engines

One project we're currently working on, is entirely depending on javascript to allow the user interaction with the application. Because of this requirement, we wanted to play nice, and tell users without javascript, that it is a requirement to use the web app.

But, and here's the kicker, I didn't want every page on the site indexed by Google to have a big fat warning, telling users to go elsewhere.

So, how does one go about providing users with nice friendly warnings, without spamming the search engine indexes with useless warnings, that say absolutely nothing about your site?

So far, the only solution I have been able to come up with is this:

* Add a &lt;noscript&gt; element to the page to contain the warning(s). This takes care of the visiblity problems, as it is only visible to users without javascript. But unfortunately, search engines will still index it as regular content.
* To prevent indexing, place the content in a separate file, and load that file using an iframe inside the noscript tag, thus: `<noscript><iframe src="fancy-javascript-required-warning.html" /></noscript>`
* Lastly, don't forget to modify your robots.txt to make sure search engines will know to exclude the warning message from the index

And that's it ... you can now create nice, user-friendly warnings about javascript being a requirements for your application, without ruining your SEO efforts :-)

This a repost from the Gazebo blog, as it is no longer maintained, and I didn't want my posts from that blog to disappear.

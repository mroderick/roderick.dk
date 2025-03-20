---
date: '2010-02-26T00:00:00+0000'
title: 'Juicer 1.0.0 Released'
tags: ['Ruby', 'Web', 'Work']
aliases: /2010/02/26/juicer-1-0-0-released/
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

Earlier today [Christian Johansen](http://cjohansen.no/en/) pushed the button and [published Juicer v1.0.0 as a gem](http://groups.google.com/group/juicer-dev/browse_thread/thread/1ce8b35ab2ccccae).

For those unfamiliar with [Juicer](http://github.com/cjohansen/juicer), it's an open source Ruby based tool that allows you to merge and minify your JavaScript and CSS files. Internally, Juicer uses [JSLint](http://www.jslint.com/) to keep your JavaScript in good shape and supports both YUI Compressor and Google Closure Compiler to make your CSS and JavaScript files as small as possible.

I have written about [speeding up your Webby site with Juicer](/2009/11/04/speeding-up-your-webby-site-with-juicer/) previously, and with the new version there are even more features to like. These are the new features that exites me the most

* Support for [Google Closure Compiler](http://code.google.com/closure/compiler/)
* Support for embedding images into stylesheets using data-uri's (my contribution)
* Ruby 1.9 support

Christian has done a lot of work tidying up the codebase, making it very flexible and easy to work with. So if Juicer also exites you, I suggest you get involved in making it even better.

* [Juicer on Github](http://github.com/cjohansen/juicer) - includes all the details you need to get started with Juicer
* [Juicer Google Group](http://groups.google.com/group/juicer-dev) - where you go to discuss all things Juicer

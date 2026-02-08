---
date: "2020-07-28T12:03:00+0200"
title: "Using HTTPie with mkcert"
tags: ["Work"]
aliases: /2020/07/28/using-httpie-with-mkcert/
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

In order to get the development environment on `localhost` closer to the production environment, I'm using HTTPS on `localhost`. This helps me with discovering bugs much earlier, which saves a lot of time.

I use the [excellent tool `mkcert`](https://blog.filippo.io/mkcert-valid-https-certificates-for-localhost/) for managing the certificates locally. `mkcert` is built exactly for this purpose and removes most of the friction.

I regularly use [`httpie`](https://httpie.org) to interact with HTTP servers.

However, `httpie` doesn't know about about the certificate authority installed locally by `mkcert`, so we'll have to help it a bit.

```sh
http --verify="$(mkcert --CAROOT)/rootCA.pem" https://localhost.myapp.org:8443/some/path
```

Since I don't want to type that on every invocation, I've added it as an alias in `.bash_profile`.

```sh
alias http="http --verify=\"$(mkcert --CAROOT)/rootCA.pem\""
```

And then I can use `httpie` as normal

```sh
http https://localhost.myapp.org:8443/some/path
```

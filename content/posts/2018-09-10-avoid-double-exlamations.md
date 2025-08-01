---
date: '2018-09-10T00:00:00+00:00'
title: 'Avoid double exclamations in JavaScript'
tags: ['JavaScript', 'Work']
aliases: /2018/09/10/avoid-double-exlamations/
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

There is a common misuse of JavaScript's type coercion that I see in code reviews. It's the terse use of two exclamation marks to convert a [truthy][truthy] value to a `Boolean` value.

Here's an example:

```js
const someValue = "I like apple pie";
const userLikesPie = !!someValue;
// userLikesPie is now `true`
```

I think this is a misuse for two reasons:

1. it obscures intent for people that are not fully aware of JavaScript coercion
1. it is easy to introduce a mistake that can be difficult to detect

As for the first point, you could argue that it is the reader's responsibility to educate themself in order to fully understand the code. However, there isn't much value in winning that argument if the reader misunderstands the code and introduces new bugs.

Even seasoned writers of the JavaScript will be able to casually introduce subtle and difficult to find regressions, when playing around with the code in order to understand how it behaves. These changes can hide in a large diff and sneak past even the most diligent code reviews.


Let's illustrate with an example:

```js
// as in the example above:
// the first exclamation mark coerces and negates a truthy expression to `false`
// second exclamation mark negates `false` to `true`
if (!!someValue && someOtherValue) {
    // some action
}

// will anyone detect the mistake of removing one exclamation mark?
if (!someValue && someOtherValue) {
    // some action
}

// or detect the mistake of adding third exclamation mark?
if (!!!someValue && someOtherValue) {
    // some action
}
```

Instead of using double exclamation marks, which opens the door for these regressions, I recommend using the [`Boolean`][boolean] function to coerce values to booleans. Using this pattern makes it difficult for these mistakes to hide.


```js
if (Boolean(someValue) && Boolean(someOtherValue)) {
    // some action
}
```

Since we're already working in this area of the codebase, we can improve it further by introducing a constant to label the condition that we're examining. This will make the both the context and the author's intent clearer, which in turn makes it less likely that future developer will introduce regressions.

```js
const someConditionIsMet = Boolean(someValue) && Boolean(someOtherValue);
if (someConditionIsMet) {
    // some action
}
```

### Bonus: use `Boolean` in iteration

You can also use `Boolean` in iteration, which would be a lot less elegant with `!!`.

```js
const values = [1, 0, {}, undefined, [], null, 'apple pie', '',  false, true, ];
const truthyValues = values.filter(Boolean);
// [1, {}, [], "apple pie", true]
```

[boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean
[truthy]: https://developer.mozilla.org/en-US/docs/Glossary/Truthy

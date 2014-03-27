---
layout: post
title: "Numeric Input on Mobile"
description: "How to add cross-browser numeric input to mobile, for a better user experience."
category: articles
modified: 2014-03-27
---

Let's say we we want a field for numeric quantity (e.g. the user specifies a number of items to order during checkout). We want it to look like this:

![Numeric input keypad, on iOS](/images/numeric.png =320x480)

The correct, semantic approach for bringing up the numeric keypad looks like this:

{% highlight html %}
  <input type="number" pattern="[0-9]*" inputmode="numeric">
{% endhighlight %}

... resulting in this (try it on your favorite mobile browser):

<input type="number" pattern="[0-9]*" inputmode="numeric">

Why not just use `<input type="text">`, like we used to? Here's why we need each of the attributes above:

**Type**: Technically, you *could* use `type="tel"`. It's an ugly hack, but it does reliably pull up a phone-style input on just about any mobile browser. That said, there are better and more semantic ways to get where we want to be. You want this to be `type="number"`, because it reflects the true purpose of the field.

**Pattern**: Most of the common iPhone browsers will infer the correct keypad type from `pattern`, a regular expression to tell the browser which inputs should be treated as valid. In this case, we're using `pattern="[0-9]*"` to say "allow the user to give us anything starting with a digit, zero through nine."

**Inputmode**: The HTML5 `inputmode` attribute is fully supported on newer Android browsers, including the latest versions of Chrome. We can use `inputmode="numeric"` to force the number pad to appear. Not every browser recognizes `inputmode`, but it's the best way to explicitly ask for a numeric keyboard.

---
layout: post
title: How to Access Array of Array in Ember.js
---

For example we have array like this:

{% highlight javascript %}

[[1, "Orange"], [2, "Grape"], [3, "Strawberry"]]

{% endhighlight %}

The simplest and straightforward way to access the individual elements from handlebars template is like this:

{% highlight javascript %}

{{#each fruitArrays as |fruitArray|}}
   <option value={{fruitArray.[0]}}>{{fruitArray.[1]}}</option>
{{/each}}

{% endhighlight %}
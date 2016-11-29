---
layout: post
title: How to Access Array of Array in Ember.js
---

For example you have array like this:

```javascript
[[1, "Orange"], [2, "Grape"], [3, "Fruit"]]
```

The simplest and straightforward way to access the individual elements from handlebars template is like this:

<pre>
{{#each fruitArrays as |fruitArray|}}
   <option value={{fruitArray.[0]}}>{{fruitArray.[1]}}</option>
{{/each}}
</pre>
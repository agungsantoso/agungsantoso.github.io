---
layout: post
title: Circular Dependencies Support in Babel.js
---

Circular dependency is a relation between two or more modules which either directly or indirectly depend on each other to function properly. 

The simplest example of a circular dependency is when file A imports file B and file B imports A. Unfortunately, what makes this issue hard to detect sometimes is that the circle can be arbitrarily large, spanning over a huge amount of files.

Circular dependencies are supported in ES6 and they can be used when one is careful enough. However, circular dependencies are very often a sign of bad design decisions.

There are some information in [ES 2017 spec](https://tc39.github.io/ecma262/#sec-resolveexport) regarding this. So don't be surprised to find that in Babel.js, you could have two modules import each other without any issues.
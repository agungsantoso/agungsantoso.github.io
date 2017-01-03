---
layout: post
title: Simple guideline to use react js web code on react native
---

* Consider a good architecture and code structure in order to share as much code (and application logic) as possible. Try to separate the UI presentation components (which will be different for each platform).
* Take a look at the JavaScript Environment specifics in the React Native docs. When using React Native, you’re going to be running your JavaScript code in two environments:
    * On iOS simulators and devices, Android emulators and devices. React Native uses JavaScriptCore which is the JavaScript engine that powers Safari. On iOS JSC doesn’t use JIT due to the absence of writable executable memory in iOS apps.
    * When using Chrome debugging, it runs all the JavaScript code within Chrome itself and communicates with native code via WebSocket. So you are using V8.
    While both environments are very similar, you may end up hitting some inconsistencies.
* Consider the different strategies for sharing the code. In order to accesses shared code, the apps you’re building doesn’t have to all live in the same codebase or git repository.

More realistically, you would have two or more projects hosted separately, so an npm package is one of the easiest ways to share code between them.

This is easy as making a new package and setting it as a dependency inside each of your projects. For the path to the shared project, you can use a git repository rather than pointing to a public package on npm.

Even though you’re building only the web app now, you could spend some time thinking about how you could generalize some of the shared code, so it is easier to re-use it in future.
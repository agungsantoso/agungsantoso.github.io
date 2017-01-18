---
layout: post
title: Difference between Dagger and ButterKnife Android
---

ButterKnife is targeted to inject views only. Non-activity injection just means that you can provide your own view root to inject views from (like with manually inflated views, etc.). Dagger is a bit more complicated. It can inject anything you want as long as you specified `Module` - class which satisfies those dependencies (alternatively you can use constructor injection).

As a bottom line — I would say ButterKnife helps you to avoid all that boilerplate code for creating views (aka `(TextView)findViewById(R.id.some_text_view);`. Nothing more. Under the hood it still does all that boring code. So it is not really an injection..

Also it worth mentioning that Jake Wharton is one of the developers for both those cool libs :)

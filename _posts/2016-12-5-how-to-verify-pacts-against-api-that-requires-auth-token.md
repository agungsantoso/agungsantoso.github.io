---
layout: post
title: How to Verify Pacts Against API that Requires Auth Token
---

You know how to generate an API token for your user, but you don't know where to place the token in the Pact workflow? The answer is you actually don't have to use a real token for each pact interaction unless you really need to.

For that kind of stuff, You just need to create a regex to be used on the header to validate certain rules while keeping it 'open'. In my node project (which uses the Ruby binary in the back), I created these 2 utilities functions to create objects with a pattern and another for a object minimum equal:

```javascript
function term(matcher, generate) {
    if ((typeof matcher === 'undefined') || (typeof generate === 'undefined')) {
      throw 'Matcher and Generate arguments must be specified to use Term';
    }
    return {
      "json_class": "Pact::Term",
      "data": {
        "generate": generate,
        "matcher": {
          "json_class": "Regexp",
          "o": 0,
          "s": matcher
        }
      }
    };
}

function somethingLike(value) {
    return {
      "json_class": "Pact::SomethingLike",
      "contents": value
    };
}
```
  
You can then use it in your DSL definition like so:

```ruby
mockService
  .given('a form')
  .uponReceiving('a GET request with a valid auth')
  .withRequest('get', '/', term('^Bearer (?!null$).+$', 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ'))
  .willRespondWith({
    status: 200,
    headers: {'Content-Type': 'application/json;charset=utf-8'},
    body: {worked:true}
  });
```

The 'term' utility has a regex as the first parameter and then an example (that should match the first) of what to use during the test.

I know that this needs to be expanded better within Pact itself to make it simpler to use. I hope this helps.
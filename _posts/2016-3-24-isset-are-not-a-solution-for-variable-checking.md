---
layout: post
title: isset() Are Not a Solution for Variable Checking
---

Despite its name, `isset()` not only returns false if an item does not exist, but also returns `false` for `null` values.

This behavior is more problematic than it might appear at first and is a common source of problems.

Consider the following:

```php
$value = functionName($bar, $foo);
if (!isset($value['keyName']) {
    // do something here if 'keyName' is not set
}
```

The author of this code presumably wanted to check if `keyName` was set in `$value`. But, as discussed, `isset($value['keyName']` will also return false if `isset($value['keyName']` was set, but was set to `null`. So the above logic is flawed.

Here’s another example:

```php
if ($_POST['keyName']) {
    $postValue = functionName($_POST);
}

// ...

if (!isset($postValue)) {
    echo 'key not found';
}
```

The above code assumes that if `$_POST['keyName']` returns `true`, then `postValue` will necessarily be set, and therefore `isset($postValue)` will return `true`. So conversely, the above code assumes that the only way that `isset($postValue)` will return false is if `$_POST['keyName']` returned false as well.

Not.

As explained, `$_POST['keyName']` will also return false if `$postValue` was set to `null`. It therefore is possible for `isset($postValue)` to return false even if `$_POST['keyName']` returned true. So again, the above logic is flawed.

And by the way, as a side point, if the intent in the above code really was to again check if `$_POST['keyName']` returned true, relying on `isset()` for this was a poor coding decision in any case. Instead, it would have been better to just recheck `$_POST['keyName']`; i.e.:

```php
if ($_POST['keyName']) {
    $postValue = functionName($_POST);
}

// ...

if ($_POST['keyName']) {
    echo 'keyName not found';
}
```

For cases, though, where it is important to check if a variable was really set (i.e., to distinguish between a variable that wasn’t set and a variable that was set to null), the `array_key_exists()` method is a much more robust solution.

For example, we could rewrite the first of the above two examples as follows:

```php
$value = functionName($foo, $bar);
if (! array_key_exists('keyName', $value)) {
    // do this if 'keyName' isn't set
}
```

Moreover, by combining `array_key_exists()` with `get_defined_vars()`, we can reliably check whether a variable within the current scope has been set or not:

```php
if (array_key_exists('keyName', get_defined_vars())) {
    // variable $keyName exists in current scope
}
```

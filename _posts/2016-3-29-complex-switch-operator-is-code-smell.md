---
layout: post
title: Complex Switch Operator Is a Code Smell 
---

Do you have a complex switch operator or sequence of if statements? I would strongly recommend avoiding them. I believe switch operator or if statements that is too complex is a code smell. Why? Because often code for a single switch can be scattered in different places in the program. And when a new condition is added, you have to find all the switch code and modify it. It is an obvious code smell.


As a rule of thumb, when you see switch you should think of polymorphism. Look at this PHP class:

```php
class Bird {
  ...
  function getSpeed() {
    switch ($this->type) {
      case EUROPEAN:
        return $this->getBaseSpeed();
      case AFRICAN:
        return $this->getBaseSpeed() - $this->getLoadFactor() * $this->numberOfCoconuts;
      case NORWEGIAN_BLUE:
        return ($this->isNailed) ? 0 : $this->getBaseSpeed($this->voltage);
    }
    throw new Exception("Should be unreachable");
  }
  ...
}
```

Why does it have a conditional that performs various actions depending on object type or properties? Isn't it almost identical conditional? I would create subclasses matching the branches of the conditional.

![Smell](http://cf.jare.io/?u=http://www.agungsantoso.com/images/smell.jpg "Smell")

Here is how I would refactor the class:

```php
abstract class Bird {
  ...
  abstract function getSpeed();
  ...
}

class European extends Bird {
  function getSpeed() {
    return $this->getBaseSpeed();
  }
}
class African extends Bird {
  function getSpeed() {
    return $this->getBaseSpeed() - $this->getLoadFactor() * $this->numberOfCoconuts;
  }
}
class NorvegianBlue extends Bird {
  function getSpeed() {
    return ($this->isNailed) ? 0 : $this->getBaseSpeed($this->voltage);
  }
}

// Somewhere in Client code.
$speed = $bird->getSpeed();
```

In them, I create a shared method and move code from the corresponding branch of the conditional to it. Then I replace the conditional with the relevant method call. The result is that the proper implementation will be attained via polymorphism depending on the object class.

Now the code looks more organized.

This technique adheres to the Tell-Don't-Ask principle: instead of asking an object about its state and then performing actions based on this, it is much easier to simply tell the object what it needs to do and let it decide for itself how to do that. If you need to add a new execution variant, all you need to do is add a new subclass without touching the existing code (Open/Closed Principle) :)
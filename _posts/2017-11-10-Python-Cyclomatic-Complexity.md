---
title: "Python Cyclomatic Complexity"
categories:
  - technical
tags:
  - python
  - coding
  - OOP design
  - clean code
toc: true
---

This post presents several scenarios with high CC and the ways to decrease 
it in Python.


Here's a short introduction about how the cyclomatic complexity (CC) in computed: [Introduction to Code Metrics](http://radon.readthedocs.io/en/latest/intro.html)

Keeping low CC is important for other developers to understand and maintain your code. Generally, we try to write short functions with single responsibility to avoid high CC. The following scenarios describe functions with high CC and the ways to decrease the complexity.


## Homogeneous `if ... elif ... else`

### `switch`
As there's no `switch ... case ...` in Python as in other languages, you might want to implement similar code by using many `if ... else ...` statements. This can make the code heavy. Here is an example
```python
if value == "a":
    action_a()
elif value == "b":
    action_b()
elif value == "c":
    action_c()
else:
    action_default()
```

### Dictionary Mapping
A clean way for this situation is to create a mapping dictionary. In Python, functions are also object. So the code above can be written as this
```python
action_map = {"a": action_a, "b": action_b, "c": action_c}
action = action_map.get(value, action_default)
action()
```
Of course, when the *action* of each case is more complex, like when the function 
grows too long, the inner logic becomes more and more complicated, or each action 
requires some specific configuration.
In this case, you should consider polymorphism to refactor it into class.

### Factory Pattern
A [factory](https://sourcemaking.com/design_patterns/abstract_factory) pattern here
can be a good idea, like this

```python
class Action(object):

    @classmethod
    def from_value(cls, value):
        for sub_cls in cls.__subclasses__():
            if "action" + value == sub_cls.__name__.lower():
                return sub_cls()
        return cls()

    def __call__(self):
        action_default()


class ActionA(Action):
    def __call__(self):
        action_a()


class ActionB(Action):
    def __call__(self):
        action_b()


class ActionC(Action):
    def __call__(self):
        action_c()
        
        
# main
action = Action.from_value(value)
action()
```
The above code is equivalent with the two previous ones. There's a variation I 
implemented some time ago in 
[abstract_factory.py](https://github.com/faif/python-patterns/blob/master/creational/abstract_factory.py).
It can be cleaner by setting `__call__` as abstract, which makes the intention 
of the parent class more clear for other developers.

Although I think the third option may look fancy, I would prefer to start the development
with the first implementation for a simple case. Then we advance to the second one when there
are too many `if`. Finally when it is needed, we can refactor the code into the third pattern.

## Inhomogeneous conditional logic and loop

Consider the following piece of code
```python
if value_a == "a":
   action_a()
   if value_b != "c":
      action_a()
if value_b == "b" and value_c == "d":
    action_b()
if value_c != "c":
    action_c()
```
This is really bad. The work flow is hard to follow. It is difficult to figure out which case will land where. You'd better refactor the code with [single responsibility principle](http://www.oodesign.com/single-responsibility-principle.html). Be nice and thoughtful to people who will read and maintain your code later. 

Imagine one day you are asked to add a feature to this code. Will you enjoy working on it ?
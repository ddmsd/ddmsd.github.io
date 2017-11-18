---
title: "Tell, don't ask"
categories:
  - technical
tags:
  - coding
  - OOP design
---


> Procedural code gets information then makes decisions. Object-oriented code tells objects to do things.
> — Alec Sharp

I have read an article [Tell, don't ask](https://pragprog.com/articles/tell-dont-ask) recently and found it a very valuable point for object oriented programming.

Take the following Python code as an example,

```python
# main
person_age = 40
if person_age < 70:
    jump_high()
else:
    jump_low()
```

This is a typical *asking* version. The main program takes the responsiblity to decide if a person can jump high or not by checking the variable state, i.e. the age of person here. This does not look like a correct division of responsibility. It also violates the idea of encapsulation as the decision of jump level is made outside the object.

A *tell* version of the same problem is to encapsulate the behavior *jump* and the data *age* into one class, like this

```python
class Person:
    jump_age_threshold = 70
    def __init__(self, age):
        self.age = age

    def jump(self):
        if self.age < self.jump_age_threshold:
            jump_high()
        else:
            jump_low()
# main
person = Person(40)
person.jump()
```
In the *tell* version, we hide the inner logic of jump from the main program. This corresponds more to the idea of OOP.


There is another article of Martin Fowler on the same subject [tell don't ask](https://martinfowler.com/bliki/TellDontAsk.html).
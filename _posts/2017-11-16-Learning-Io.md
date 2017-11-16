---
title: "Try Io"
categories:
  - technical
tags:
  - prototype
  - notes
---

[Io](http://iolanguage.org/) is a low-level prototype-based language.

In a *prototype* language, every object is a clone of an existing object rather than a class. We will just create new objects by cloning existing ones, and the existing object is a *prototype*. To create an object of type `Vehicle`

```io
Io> Vehicle := Object clone
==>  Vehicle_0x1b5c300:
  type             = "Vehicle"
```
Here we send the `clone` message to `Object` then it returns a new object. And we assigned that object to `Vehicle`. An object in Io is like a Python dictionary, you can assign a value to a key that does not exist, but cannot access the value of an unexisting key. The key is called *slot* in Io.
```io
Io> Vehicle description := "cute"
==> cute
Io> Vehicle
==>  Vehicle_0x979b40:
  description      = "cute"
  type             = "Vehicle"

Io> Vehicle slotNames
==> list(type, description)
```

## Object model
A type is an object, not a class. By convention, types in Io begin with uppercase letters.
```io
Io> Car := Vehicle clone
==>  Car_0x89c500:
  type             = "Car"

Io> benz := Car clone
==>  Car_0x994080:

Io> benz description
==> cute
```
In Io, objects are just containers of slots. Get a slot by sending its name to an object. If the slot isn’t there, Io calls the parent.

## Singleton

It is very interesting to create a singleton in Io. For this, you only need to redefine the *clone* method.
```io
Io> Snowman := Object clone
==>  Snowman_0xc8c750:
  type             = "Snowman"

Io> Snowman clone := Snowman
==>  Snowman_0xc8c750:
  clone            = Snowman_0xc8c750
  type             = "Snowman"
```
Now let's create some copies
```io
Io> snowman_in_france := Snowman clone
==>  Snowman_0xc8c750:
  clone            = Snowman_0xc8c750
  type             = "Snowman"

Io> snowman_in_china := Snowman clone
==>  Snowman_0xc8c750:
  clone            = Snowman_0xc8c750
  type             = "Snowman"

Io> snowman_in_china == snowman_in_france
==> true
```
It is always the same snowman !



---
This note is from the book [Seven Languages in Seven Weeks](https://www.amazon.com/Seven-Languages-Weeks-Programming-Programmers/dp/193435659X) I'm reading recently.


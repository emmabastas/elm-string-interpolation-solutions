# Approaches to string concatenation/interpolation in Elm

[![Build Status](https://travis-ci.org/emmabastas/elm-string-interpolation-solutions.svg?branch=master)](https://travis-ci.org/emmabastas/elm-string-interpolation-solutions)

This text is intended to be some sort of shared knowledge about different approaches for doing string concatenation/interpolation in Elm, and list their pros and cons.

This text is likely to opinionated and narrow, if you have any thoughts then please share them! I think the Elm slack is the most appropriate, my handle there is `@emmabastas`.

## Introduction

A common programming task is to compose a string of many substrings and expressions. Say that I want to tell the users of my weather app what the temperature outside is in a nice personalized way. For instance: If the users name is `"Mark"` and the temperature outside in °C is `21`, then I'd like the final string to be `"Hey Mark, It's 21 °C outside."`. How do we accomplish that? There's many competing ways to do this in Elm, which is not desirable. In this text we look at the previous art, list what qualities we're looking for in an Elm solution and then evaluate the current approaches/solutions against this list.

## Previous art

There's so incredibly much previous art, it would be impossible to cover it all. The goal of this section is mostly to establish the core concepts and language when it comes to string concatenation/interpolation. If you're already familiar with C-style `printf`, positional and named placeholders and Rust's `format` macro then you can probably skip this section.

### String concatenation

__TODO__

### String interpolation with a format string

The most common form of this is C-style `printf` et al. which appears in a lot of languages today. It looks like this
```c
printf("Hey %s. It's %d °C outside.", "Mark", 21);
// Hey Mark. It's 21 °C outside.
```

A _format string_ is passed to `printf`. The `%s` is a _format specifier_ and means "put a string here" and `%d` is the same but for a number. You can do even more fancy stuff with format specifiers, but that outside the scope of this text.

Another example is Pythons `.format`. It can have _positional placeholders_
```python
'Hey {}, It\'s {} °C outside.'.format("Mark", 21)
# 'Hey Mark, It's 21 °C outside.'
```
Or _named placeholders_
```python
'Hey {name}, It\'s {temperature} °C outside.'.format(name = 'Mark', temperature = 21)
# 'Hey Mark, It's 21 °C outside.'
```

The biggest problem with this type of interpolation in the context of Elm is that it's not type safe. If I forget an argument or have a typo in a key the programs will either crash or produce garbled output. This python crashes:
```python
'Hi {name}!'.format(naem = 'Mark')
#         typo here ^^^^
```

### String interpolation with built in syntax

__TODO__

### Rusts `format` macro - Statically analyzed format string

In Rust you do string interpolation like this:
```rust
format!("Hey {name}, It's {temperature} °C outside.", name = "Mark", temperature = 21);
// "Hey Mark, It's 21 °C outside."
```
This looks a lot like string interpolation with a format string. But it's actually evaluated statically and is type safe. If I have a typo in a placeholder I get a compilation error!

## Important qualities / what to optimize for

Defining what to optimize for is incredibly important. It's through that lens we view and judge all the approaches.

Rust optimizes for type safety and zero cost abstractions, which led to the `format` macro to become the preferred way. Python optimizes for other things, leading to another solution that wouldn't make sense in rust, and vice-versa.

In Elm, the solution should optimize for:
* __Type safety.__ If something compiles it should work. But more generally the API/behavior should be designed in a way that minimizes the potential bugs, and gives a pleasant user experience.
* __Simplicity__. Ideally there would be one approach which is _the_ approach. That approach should be easy to use and have no major flaws. If someone asks about string concatenation/interpolation, the response should be "use __x__", not "if __a__ then use __x__, else if __b__ then use __y__ ...". I think that approaches utilizing already existing functions in `elm/core` have this going for them.
* __Readability.__ Looking at the code should give us a feel for what the concatenated/interpolated string will look like. Looking at something like `"Hello ${firstName} ${lastName}!"` makes it clear that the final string could look something like `"Hello Laurie Anderson!"` or `"Hello Alvin Lucier!"`.

We do __not__ optimize for:
* __Performance.__ String interpolation/concatenation has never been a bottleneck for me nor have i heard of that being the case for others. We shouldn't solve problems that folks aren't having! That said, if you have a use case where performance is a concern that would be very valuable to hear about.

__NOTE:__ If you don't agree with this, or have some thoughts the please share them! It's important to get this right. Any and all feedback appreciated :heart:

## Approaches evaluated

### Stick to `++`

Pros:
* __Type safe.__
* __Simple.__ `++` is arguably the most obvious way to do concatenation, it's in `elm/core` and is one of the first things Elm developers learn about.

Cons:
* __Readability.__ `++` is considered to be less readable than other alternatives.

There are however some techniques to make `++` more readable:
* Bind expressions to variables and use the variables instead.<br/>
__TODO__

* Use multiline strings for multiline content.<br/>
__TODO__

### `String.join`
__TODO__

### `String.replace`
__TODO__

### [elm-string-format](https://package.elm-lang.org/packages/jorgengranseth/elm-string-format/latest/)
__TODO__

### [elm-template](https://package.elm-lang.org/packages/lukewestby/elm-template/latest/)
__TODO__

### [elm-string-interpolate](https://package.elm-lang.org/packages/lukewestby/elm-string-interpolate/latest/)
__TODO__

### [elm-string-template](https://github.com/emmabastas/elm-string-template/blob/master/README.md)
__TODO__

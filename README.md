# Approaches to string concatenation/interpolation [![Build Status](https://travis-ci.org/emmabastas/elm-string-interpolation-solutions.svg?branch=master)](https://travis-ci.org/emmabastas/elm-string-interpolation-solutions)

This text is intended to be some sort of shared knowledge about different approaches for doing string concatenation/interpolation in Elm, and list their pros and cons.

The text is divided into three parts:
1. __Introduction__ explains string concatenation and interpolation
2. __Factors to consider__ lists the factors that we care about when doing string concatenation/interpolation
3. __Approaches enumerated__ enumerates all the approaches and their pros/cons

This text is likely to opinionated and narrow, if you have any thoughts then please share them! I think the Elm slack is the most appropriate, my handle there is `@emmabastas`.

## Introduction

A common programming task is to compose a string of many strings and expressions. Say that I want to tell the users of my weather app what the temperature outside is in a nice personalized way. For instance: If the users name is `"Måns"` and the temperature outside in °C is `25`, then I'd like the final string to be `"Hey Måns, It's 25 °C outside."`. How to accomplish that?

1. __String concatenation__
```elm
userName : String
userName = "Måns"

temperature : Int
temperature = 25

"Hey " ++ userName ++ ", It's " ++ (String.fromInt temperature) ++ " °C outside."
--> "Hey Måns, It's 25 °C outside."
```

2. __String interpolation__. There isn't a built in way to do string interpolation in Elm. In JavaScript string interpolation would look like this:
```js
`Hey ${userName}, It's ${temperature.toString()} °C outside.`
// "Hey Måns, It's 25 °C outside."
```

String interpolation is often considered more readable than string concatenation and is therefore often preferred. This becomes even more apparent with larger strings spanning multiple lines.

## Factors to consider

Before we can evaluate the pros and cons of different approaches we need to know which factors are important to us.

We care about:
* __Readability.__ Looking at the code should give us a feel for what the concatenated/interpolated string will look like. Looking at something like `"Hello ${firstName} ${lastName}!"` makes it clear that the final string could look something like `"Hello Laurie Anderson!"` or `"Hello Alvin Lucier!"`.
* __Type safety.__ If something compiles it should work. But more generally the API/behavior should be designed in a way that minimizes the potential bugs, and gives a pleasant user experience.
* __"Standardization"__. Ideally there would be one approach which is _the_ approach. That approach should be easy to use and have no major flaws. I think that approaches utilizing already existing functions in `elm/core` have this going for them.

We do __not__ care about:
* __Performance.__ String interpolation/concatenation has never been a bottleneck for me nor have i heard of that being the case for others. We shouldn't solve problems that folks aren't having! That said, if you have a use case where performance is a concern that would be very valuable to hear about.

## Approaches enumerated

### Stick to `++`

Pros:
* __"Standardized".__ `++` is arguably the most obvious way to do concatenation, it's in `elm/core` and is one of the first things Elm developers learn about.
* __Type safe.__

Cons:
* __Readability.__ `++` is considered to be less readable than other alternatives. See __Introduction__ for examples.

There are some techniques to make `++` more readable:
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

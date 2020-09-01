# Aproaches to string concatenation/interpolation [![Build Status](https://travis-ci.org/emmabastas/elm-string-interpolation-solutions.svg?branch=master)](https://travis-ci.org/emmabastas/elm-string-interpolation-solutions)

This text is intended to be some sort of shared knowlegde about different approaches for doing string concatenation/interpolation in Elm, and list their pros and cons.

The text is devided into three parts:
1. __Introduction__ explains string concatenation and interpolation
2. __Factors to consider__ lists the factors that we care about when doing string concatenation/interpolation
3. __Aproaches enumerated__ enumerates all the aproaches and their pros/cons

This text is likley to opinionated and narrow, if you have any thoughts then please share them! I think the Elm slack is the most appropriate, my handle there is `@emmabastas`.

## Introduction

A common programming task is to compose a string of many strings and expressions. Say that I want to tell the users of my weather app what the temperature outside is in a nice personalised way. For instace: If the users name is `"Måns"` and the temperature outside in °C is `25`, then I'd like the final string to be `"Hey Måns, It's 25 °C outside."`. How to acomplish that?

1. __String concatenation__
```elm
userName : String
userName = "Måns"

temperature : Int
temperature = 25

"Hey " ++ userName ++ ", It's " ++ (String.fromInt temperature) ++ " °C outside."
--> "Hey Måns, It's 25 °C outside."
```

2. __String interpolation__. There isn't a built in way to do string interpolation in Elm. In javascript string interpolation would look like this:
```js
`Hey ${userName}, It's ${temperature.toString()} °C outside.`
// "Hey Måns, It's 25 °C outside."
```

String interpolation is often considered more readable than string concatenation and is therefore often prefered. This becommes even more apparent with larger strings spanning multiple lines.

## Factors to consider

Before we can evaluate the pros and cons of different approaches we need to know which factors are important to us.

We care about:
* __Readabillity.__ Looking at the code should give us a feel for what the concatenated/interpolated string will look like. Looking at something like `"Hello ${firstName} ${lastName}!"` makes it clear that the final string could look something like `"Hello Laurie Anderson!"` or `"Hello Alvin Lucier!"`.
* __Type safety.__ If something compiles it should work. But more generally the api/behaviour should be designed in a way that minimises the potential bugs, and gives a pleasant user experience.
* __"Standardization"__. Idealy there would be one aproach which is _the_ approach. That approach should be easy to use and have no major flaws. I think that aproaches utilizing already existing functions in `elm/core` have this going for them.

We do __not__ care about:
* __Performance.__ String interpolation/concatenation has never been a bottleneck for me nor have i heard of that being the case for others. We shouldn't solve problems that folks arent having! That said, if you have a usecase where performance is a concern that would be very valuable to hear about.

## Approaches enumerated

#### Stick to concatenation

#### `String.concat`

#### `String.replace`

#### [elm-string-format](https://package.elm-lang.org/packages/jorgengranseth/elm-string-format/latest/)

#### [elm-template](https://package.elm-lang.org/packages/lukewestby/elm-template/latest/)

#### [elm-string-interpolate](https://package.elm-lang.org/packages/lukewestby/elm-string-interpolate/latest/)

#### [elm-string-template](https://github.com/emmabastas/elm-string-template/blob/master/README.md)

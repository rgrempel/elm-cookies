# elm-cookies

This is a Cookies API for the Elm programming language.

## Getting Cookies

You can get the cookies with the `get` task.

```elm
get : Task x (Dict String String) 
```

`get` results in a `Dict` of key -> value pairs which represent the key / value
pairs parsed from Javascript's `document.cookie`. Both keys and values are
uriDecoded for you.

## Setting Cookies

If you don't need to provide special options, then you can just create
a `set` task by supplying the key and value.

```elm
set : String -> String -> Task x ()
```

Both the key and the value will be uriEncoded for you.

If you need to provide options in addition to the key and value, use `setWithOptions`.

```elm
setWithOptions : Options -> String -> String -> Task x ()
```

The options are a record type with the possible options:

```elm
type alias Options =
    { path : Maybe String
    , domain : Maybe String
    , maxAge : Maybe Time
    , expires : Maybe Date 
    , secure : Maybe Bool
    }
```

You can use `defaultOptions` as a starting point, in which all options are set to `Nothing`.

```elm
defaultOptions : Options
```

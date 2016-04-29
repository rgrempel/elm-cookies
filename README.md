# Deprecation Notice

As previously noted below (under Installation), this package was, from the beginning, outside
the mainstream Elm ecosystem, since it could not be installed via the Elm package manager
(due to the native package block).

Now that more information is available about Elm 0.17, the following things seem clear:

* As expected, a variety of changes would be required for this package to work with Elm 0.17.

* The policy of @elm-lang will be that @elm-lang should own all packages which access Web APIs.
  For this reason, it will continue to be impossible to install this package via Elm's package manager.

* @elm-lang will provide as much access to Web APIs as @elm-lang considers should be available in Elm,
  via packages owned by @elm-lang.

Reflecting on this, I find that my preference is not to continue work on this package. If anyone else
should want to do something with this code, be my guest.

# elm-cookies

This is a Cookies API for the Elm programming language.

Since creating elm-cookies, I have started a larger elm-web-api project
which deals with various Javascript APIs. There is a module there for
dealing with cookies that is better maintained and tested than this
module is:

https://github.com/rgrempel/elm-web-api#webapicookie

However, if you'd prefer a smaller module, this one remains available.

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
a `set` task by supplying the key (first parameter) and value (second parameter).

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

## Installation

Because elm-cookies uses a 'native' module, it cannot be included in the
[Elm package repository](http://package.elm-lang.org/packages). Thus, you cannot
install it using `elm-package`.

In the meantime, you can install it and use it via the following steps:

*   Download this respository in one way or another. For instance, you might use:

        git clone https://github.com/rgrempel/elm-cookies.git

    Or, you might use git submodules, if you're adept at that. (I wouldn't suggest
    trying it if you've never heard of them before).

*   Modify your `elm-package.json` to refer to the `src` folder.

    You can choose where you want to put the downloaded code, but wherever that
    is, simply modify your `elm-package.json` file so that it can find the
    `src` folder.  So, the "source-directories" entry in your
    `elm-package.json` file might end up looking like this:

        "source-directories": [
            "src",
            "elm-cookies/src"
        ],

    But, of course, that depends on where you've actually put it.

*   Modify your `elm-package.json` to add elm-http as a dependency, if it's not
    already there. E.g.

        "dependencies": {
            "elm-lang/core": "2.0.0 <= v < 3.0.0",
            "evancz/elm-http": "1.0.0 <= v < 2.0.0",
            ... your other dependencies
        },

*   Modify your `elm-package.json` to indicate that you're using 'native' modules.
    To do this, add the following entry to `elm-package.json`:

        "native-modules": true,

Now, doing this would have several implications which you should be aware of.

*   You would, essentially, be trusting me (or looking to verify for yourself)
    that the code in [Cookies.js](src/Native/Cookies.js) is appropriate code for
    a 'native' module -- that is, that it will not cause run-time crashes or
    otherwise interfere with the usual guarantees provided by Elm.

*   It is predictable that this module will need some changes when a new
    version of Elm is released. Therefore, you would need to remember to check
    here for such changes when that happens.

*   It has been said that Elm 0.17 will include additional support for bindings
    to Javascript platform APIs. This may make this module redundant, or it may
    make it easier or harder to implement or install.

*   If you're using this as part of a module you'd like to publish yourself,
    then you will also be unable to publish your module in the package repository.

So, you may or may not really want to do this. But I thought it would be nice to
let you know how.

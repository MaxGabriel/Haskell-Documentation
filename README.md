# Haskell-Documentation
Issue tracker for Haskell documentation projects for Bay Area haskell group meetup.

## Documenting Haskell Libraries

1. Pick a project or module that you'd like to work on documenting. I recommend working on a library that you've already used, but you can also look for something in the [Issue Tracker](https://github.com/MaxGabriel/Haskell-Documentation/issues). If you'd like to work on a tutorial instead, check out requests for tutorials [at this repo](https://github.com/parsonsmatt/hasktuts).
	* Please comment on the issue tracker what you're working on, and if you'd like other people to join you.
2. Find the library on Github and fork it.
3. Clone your copy of the library.
4. Write documentation.
5. Test that it looks correct (see below)
6. Push to your own repo, then submit a pull request to the original library.

## Haddock Syntax overview:

Most Haddock syntax involves a comment followed by some sort of "control character" based on what kind of documentation you're writing. Here's a brief overview of some basic concepts ([full guide available here](https://www.haskell.org/haddock/doc/html/index.html)).

### Top level declarations

Top-level declarations like functions and `data` declarations can be documented by putting `-- |` on the line before declaration:

```haskell
-- | Opens the cave where the treasure is.
openSesame :: IO ()
openSesame = ...
```

This syntax (`-- |`) also works for `data` declarations, `newtype`, `type`,

### Referencing other functions

If you reference another function or data type, wrap it in single quotes to have Haddock hyperlink to it:

```haskell
-- | This function calls 'openSesame' and does some other things
openSesame2 :: IO ()
openSesame2 = ...
```

### Writing example code

See [the Haddock Guide for a concise explanation](https://www.haskell.org/haddock/doc/html/ch03s08.html#idm140354810780208).

As the guide explains, you can use bird tracks (>) before each line, or surround the code block with `@` symbols. Bird tracks are simpler, because you don't need to escape Haddock markup:

```
-- | This function reverses a string
--
-- > let x = reverse "abc"
-- > x == "cba" -- True
```

Writing examples using `@` signs is more powerful, because you can do things like link to other functions from the code block. You'll need to escape Haddock markup, though. You can see this approach [being used here](https://github.com/snoyberg/mono-traversable/blob/d71530430bb7b2e1559ca30779d885ad0ece761a/src/Data/MinLen.hs#L356-L360)


### Writing high-level overviews

Sometimes you'll have a group of functions that you'd like to give a broader explanation for. You can create a block of Haddock documentation with an identifier:

```
-- $example
-- Here I give a high level overview of these functions, and provide some example code.
```

and then reference it in the export list:

```haskell
module Yesod.Form.Bootstrap3
  ( -- * Example: Rendering a basic form
    -- $example

    -- * Rendering forms
    renderBootstrap3
```

You can see an example of this being done in [this module](https://github.com/yesodweb/yesod/blob/ae0d0b12c4e17705a01f3bdd78a2a3743b17bdf7/yesod-form/Yesod/Form/Bootstrap3.hs#L267-L286).

Again, the [full Haddock guide is available here](https://www.haskell.org/haddock/doc/html/index.html).

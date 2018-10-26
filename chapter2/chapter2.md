# Chapter 2! The world of Haskell!

## Useful GHCi commands
These are part of GHCi, not part of haskell!

- `:q` quit
    quits out of GHCi!
- `:i something` information
    gives some information about funcs, types, etc. E.g.
    ```GHCi
    Prelude> :i +
    class Num a where
      (+) :: a -> a -> a
      ...
            -- Defined in ‘GHC.Num’
    infixl 6 +
    ```
- `:l module_name.hs` load a haskell file into scope
- `:m` unload a haskell file

_expressions_ evaluate to _result_

_declaration_: top-level bindings

_normal form_: irreducable (everything that _can_ be done, has been done). E.g. `9` is in normal form but `3 * 3` is not.

_redex_: reducable expressions

reducing AKA executing, normalizing or evaluating

## Functions
They map input or set of input to an output

In GHCi, we use `let`:
```ghci
Prelude > let triple x = x * 3
```

in a source file, no let! (unless we're in a func)

_parameters_ are the variable names used in the body of a function

## Evaluation
By default, haskell evaluates to "Weak Head Normal Form" not normal form.

### QUESTION!: is WHNF equivalent to "being lazy"

### Exercises:
1.
```ghci
let half x = x/2
let square x = x * x
```

2.
```haskell
areaCircle :: Fractional a => a -> a -- type taken from ghci with :i areaCircl
areaCircle radius = 3.14 * (radius * radius)
```

3.
```haskell
areaCircle :: Fractional a => a -> a -- type taken from ghci with :i areaCircl
areaCircle radius = pi * (radius * radius)
```

## infix vs prefix
default: prefix . E.g. `id 1`

some operators: infix . E.g. `1 + 2`

infix -> infix with backtics.
```haskell
10 `div` 4
```

prefix -> prefix with parens
```haskell
(+) 1 2
```


### NOTE: THIS WAS AN AHAH MOMENT FOR ME:
case function name of
  alphanumeric? -> prefix by default
  symbol -> infix by default

"not all prefix funcs can be infix"
- I think this is because infix requires two args (maybe I'm wrong!)

### precedence
find it with `:i` in ghci

higher number -> happens "faster" / higher precedence. 0-9


### associativity
infixl: left associative, e.g. 1-2-3 equivalent to (1-2)-3 not 1-(2-3)
infixr: right associative, e.g. 4^3^2 equivalent to 4^(3^2) not (4^3)^2

### Exercises
1. changes, + has lower precedence than *
2. same, * already has higher precedence than +
3. changes, + has lower precedence than /

## Declarating values
can bundle multiple values under let, but whitespace is meaningful

can use `let` with `in`
e.g.

```haskell
foo x =
  let y = x*2
      z = x^2
  in 2*y*z
```

### aside: we use hlint to help with whitespace stuff. Hlint also is way faster than compiler, so we get faster feedback about mistakes on larger projects. Similar to elm-format.

### exercises

1. There's a redundant space between 3. and 14
2. b isn't a param to double
3. extra space before y


## Arithmetic functions
notable: special funcs for Integral division: div, mod, quot, rem

### mod is like a clock
always has the same sign as the second argument

### negative nums
often need to use parens or the negate function to clarify that you're not using the infix function, `-`

### parenthisization
can use it for precedence. Can also use `$`, equivalent to `<|` in elm. Simple infixl operator with lowest precedence

### parenthizing infix
can also parenthise infix operators with an argument, e.g. `(1-)` to subtract FROM 1 or `(/2)` to halve.

Can't do that with `(-1)` because that's ambiguous with negate. There, you can use `subtract`, the prefix version of `-`

## Let & Where

we can use `let`/ `in` or we can follow an expression with `where`

```haskell
printInc n = print plusTwo
  where plusTwo = n+2

-- or with let
printIncWithLet n =
  let plusTwo = n+2
  in print plusTwo
```


### Exercises
guess the result
1. 5
2. 25
3. 30
4. 6

rewrite with where
1.
```haskell
a = x*3+y where x = 3; y = 1000
```

2.
```haskell
x*5 where y = 10; x = 10*5+y
```

3.
```haskell
z / x + y
where
  x = 7
  y = negate x
  z = y * 10

```

## Chapter Exercises
parens
1. 2 + (2 * 3) - 1
2. ((^) 10) $ (1 + 1)
3. ((2 ^ 2) * (4 ^ 5)) + 1

equivalent expressions
1. same
2. same
3. different as args are wrong
4. different types (frac vs integral)
5. different, changing precedence

funcs
1. 

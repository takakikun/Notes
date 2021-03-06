### Item51 : Beware the performance of string concatenation

----------

The string concatenation operator(+) is a convenient way to combine a few strings into one. It is fine for generating a single line of output or for constructing the string representation of a small, fixed-size object, but it does not scale. **Using the string concatenation operator repeatedly to concatenate *n* strings requires time quadratic in *n***. It is an unfortunate consequence of the fact that strings are *immutable*. When two strings are concatenated, the contents of both are copied.

So don't use the string concatenation operator to combine more than a few strings unless performance is irrelevant. Use `StringBuilder`'s `append` method instead. Alternatively, use a character array, or process the strings one at a time instead of combining them.
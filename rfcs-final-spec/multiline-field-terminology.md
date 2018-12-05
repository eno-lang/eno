# RFC: Multiline field terminology

This RFC proposes a *non-functional* change of terminology, renaming eno's `Block` element as `Multiline Field` instead.

Presently in eno there are `Field` and `Block` elements:

```eno
my field: my value

-- my block
my value
...
...
-- my block
```

`Block`s were named as such because of its brevity, but in hindsight I'm reconsidering this because the term is very generic (e.g. coming freshly to eno, `Block` offers little differentiation from `Section`, although vastly different things). `Multiline Field` is considerably longer but does spell out its meaning right to the point, as well as solving the inconsistency that in all eno libraries both `Field` and `Block` are referred to as fields in the API, which would be consistent again if the latter were a `Multiline Field`.

This change also has some positive overlap with another, yet unwritten RFC to be linked here then.

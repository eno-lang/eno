# RFC: Key terminology

This RFC proposes a *non-functional* change of terminology, changing eno's `Name` terminology to `Key` instead.

Presently in eno, `Name` is used to refer to keys:

```eno
> 'my section' is referred to as the *name* of the section
# my section

> 'my field' is referred to as the *name* of the empty element
my field:

> 'my block' is referred to as the *name* of the block
-- my block
...
-- my block
```

In the future, all these should be referred to as `Key`.

Furthermore `:`, when used as an operator, is presently labelled the `Name Operator` but shall in the future be labelled the `Element Operator` (because it specifies an element of sometimes known, sometimes ambiguous identity, e.g. it might start a list, a field, a fieldset, etc.)

Originally the `Name` terminology was chosen because it likely is a more graspable term for non-technical users to understand (and eno strives to be very accessible to people with different backgrounds), however given that there soon will be official eno API support to use type loaders on names as well, and that generally names might just as well encode any type of data, not just names in the semantic sense, key really is a more apt term, asides being the go-to term in computing for this.

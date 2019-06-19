# Language specification details

This is a work in progress draft for providing eno's specification details in a
textual form.

## Ordering

All data structures in eno respect and retain their ordering, regardless of
whether they conceptually represent key-value structures or key-less lists.

## Types

In eno there is no type differentiation on the language level, there are only
textual representations ("strings"), which are always referred to as *values*.

## Application types

Libraries implementing the parsing of eno documents should provide first class
APIs that facilitate validation and conversion of eno's ambiguous *values* into
arbitrary types that can both be offered out of the box by the library, by
add-on packages, or be defined by the developer themself in a functional manner. The
paradigms as explored and demonstrated by the offical eno libraries (enojs,
enopy, enorb at the time of writing) can serve as inspiration for this, but
innovation is just as welcome as replication of the existing paradigms, which is
also why the eno specification itself does not constrain the defintion of a
valid eno parser implementation in that regard.

## Line continuation

A line continuation only contributes to a field if it contains a value itself,
or in other words, a line continuation without a value is a noop:

```eno
> null
my_field:
\

> "my_value"
my_field: my_value
\

> "my_value continued"
> (only one space, contributed by the second line continuation)
my_field: my_value
\
\ continued
```

## Newline continuation

Empty newline continuations only contribute to a field if they are both  preceded and
followed by non-empty continuations respectively an initial field value at some point (they do not need to be directly preceded or followed for this to apply):

```eno
> null
my_field:
|

> "my_value"
my_field: my_value
|

> "my_value"
my_field:
| my_value

> "my_value"
my_field:
|
| my_value

> "my_value\n\ncontinued"
> (two newlines, both continuations contribute here)
my_field: my_value
|
| continued

> "my_value\n\ncontinued"
> (two newlines, both continuations contribute here)
my_field:
| my_value
|
|
| continued
```

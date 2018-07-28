# Terminology

A complete glossary of terms employed by the eno language and its implementations.  
All terms are listed alphabetically and in their singular form.

## Block

```eno
-- my_name
my multiline value ...
-- my_name
```

A `Block` has a `Name` and a `Value`.

## Block Operator

Two or more consecutive `-` characters when they appear as first non-whitespace characters on a line and followed by a `Name`, indicating the begin or end of a `Block`.

## Comment

```eno
> my comment
```

A `Comment` is indicated by the `Comment Operator` and followed by arbitrary text.

## Comment Operator

The `>` character, when it occurs as the first non-whitespace character on a line, thereby indicating a `Comment`.

## Copy Operator

A `<` character when it appears between a `Name` and a `Template`, indicating a copy operation.


## Deep Copy Operator

The `<<` character sequence when it appears between a `Name` and a `Template`, indicating a deep copy operation.

## Document

```eno
```

The top level structure that contains everything in an `.eno` file.
Technically equivalent to a `Section`, but implicitly always there and without a
name.

## Empty Element

```eno
my_name:
```

A name that might refer to either a `Value`, `List` or `Fieldset`. Given
that the actual nature of the element is therefore ambiguous outside the
context on an actual application, it is called simply an `Empty Element`.

## Element

All meaningful data nodes in a `Document`, that is a `Block`, `Field`, `Fieldset`, `Fieldset Entry`, `List`, `List Item` or `Section`.

## Escaped Name

```eno
`my_escaped_name`:
```

A `Name` contained between `Escape Operators`.

## Escape Operator

Any number of connected ``` characters when they appear as the first non-whitespace characters in a line, indicating an `Escaped Name`. It must be followed by exactly the same `Escape Operator` later in the same line, terminating the `Escaped Name`.

## Field

```eno
my_name: my value
```

A `Field` has a `Name` and a `Value`.

## Fieldset

```eno
my_name:
my_entry_a = my value
my_entry_b = my value
```
A `Name` followed by any number of `Fieldset Entries`.

## Fieldset Entry

```eno
my_entry = my value
```

A `Fieldset Entry` can have a `Value` or be empty.

## Fieldset Entry Operator

The `=` character when it appears after a `Name`, optionally followed by a `Value`.

## Line Continuation

```eno
\ my value
```

A `Line Continuation` can contain a `Value` or be empty.

## Line Continuation Operator

The `\` character when it appears as the first non-whitespace character on a line, indicating a `Line Continuation`.

## List

```eno
my_name:
- my value
- my value
```

A `Name` followed by any number of `List Items`.

## List Item

```eno
- my value
```

A `List Item` can have a `Value` or be empty.

## List Item Operator

A `-` character, when it appears as the first non-whitespace character in a line, indicating a `List Item`.

## Name

```eno
my_name:
```

The thing that is referred to as either *key*, *identifier* or *variable name* in other languages is always designated as `Name` in eno. A `Name` can be given to
a `Block`, `Field`, `Fieldset Entry`, `Section`, or appear as a reference in form of a `Template`.

## Name Operator

The `:` character when it appears after a `Name`, optionally followed by a `Value`.

## Newline Continuation

```eno
| my value
```

A `Newline Continuation` can contain a `Value` or be empty.

## Newline Continuation Operator

The `|` character when it appears as the first non-whitespace character on a line, indicating a `Newline Continuation`.

## Operator

Any of `>`, `<`, `<<`, `:`, `=`, `-`, `--`, `#`, `|`, `\`, ``` when they appear outside of a `Name` or `Value`.

## Section

```eno
# my_name
```

A `Section` has a `Name` and a `Depth` or `Level`, determined by the number of hashes that make up the `Section Operator`. It contains `Elements`. 

## Section Operator

Any number of connected `#` characters when they appear as the first non-whitespace characters on a line, indicating a `Section`.

## Template

```eno
my_name < my_template
```

A `Template` is a `Name` referencing an `Element` to be copied.

## Value

```eno
my_name: my_value
```

A `Value` might be associated with a `Block`, `Field`, `Fieldset Entry` or `List Item`.
`Values` can only include leading or trailing whitespace when they come from a `Block`.

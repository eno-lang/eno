# Terminology

**WORK IN PROGRESS / NOT YET COMPLETE**

A complete glossary of terms employed by the eno language and its implementations.  
All terms are listed in their singular form.

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



All meaningful data nodes in a `Document`, that is a `Field`, `Fieldset`, `Fieldset Entry`, `List`, `List Item` or `Section`.

## Field

```eno
my_name: my_value
```

A `Field` has a `Name` and a `Value`.


## Line Continuation

## List Item

```eno
- my_value
```

A `List Item` can have a `Value` or be empty.

## List Item Operator

A `-` character, when it appears as the first non-whitespace character in a line, indicating a `List Item`.


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

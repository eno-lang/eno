# RFC: Explicit Empty

This RFC proposes adding the possibility to omit the `Element Operator` after a key, thereby explicitly specifying an `Empty`, an element with a key but no value.

```eno
> An empty field/fieldset/list
element:

> An empty
element
```

The `Empty` is useful for representing a switch/flag in a section or document, or e.g. for representing a spacer or placeholder for other content in a sequential, document-oriented eno DSL.

This comes with the additional positive side effect that during writing a line containing a field, fieldset or list, the document stays valid throughout, e.g.:

```eno
m█
my█
my_incompl█
my_incomplete_k█
my_incomplete_key:█
```

At each step but the last there is an `Empty` instead of an invalid line, thereby the document can be fully parsed and a lookup performed on the cursor location, for instance to provide autocomplete suggestions for a key.

## Details on type strictness

In order to enforce documents that communicate their intent as well as possible it is also proposed to strictly differentiate between an `Empty` and an empty `Field`, i.e. if the user provided this document ...

```eno
name
tags
```

... and the application expects and validates a `Field` for 'name' and a `List` for 'tags', neither of the two above would satisfy that requirement. Neither if the document were ...

```eno
heading: My blog post
spacer:
-- post_body
...
-- post_body
```

... and the application were to expect only `Empty` elements with the key 'spacer', would this satisfy the validation conditions.

# RFC: Unifying Field, Fieldset and List

This RFC proposes a change that **does not affect existing (nor future) Eno documents**, but slightly alters Eno's conceptual hierarchic model by removing the differentiation between `Field`, `Fieldset` and `List` elements, merging them into `Field` and in turn allowing that `Field` to contain either a `Value`, `Attributes` or `Items`. Although this shift mandates a substantial one-time change in the documentation and the API model of existing Eno parsers, it shall be demonstrated below that this is ultimately worth the effort in the long-term perspective.

## Merging `Field`, `Fieldset` and `List`

Presently in Eno this is a `Field` (because it contains just a `Value`):

```eno
Name: Jane
```

This is a `Fieldset` (because it contains `Fieldset Entries`):

```eno
Name:
First = Jane
Last = Smith
```

This is a `List` (because it contains `List Items`):

```eno
Names:
- Alice
- Bob
```

Given that either of the three element types above is allowed to be empty, an ambiguity presents itself - how do we call this?

```eno
Name:
```

Ironically not even as the designer of Eno I have an official answer! This only goes to show that the current conceptual model and terminology needs a correction here, so this is what the RFC proposes:

This is a `Field` and it has a `Value`:


```eno
Name: Jane
```

This too is a `Field` and it has `Attributes`:

```eno
Name:
First = Jane
Last = Smith
```

This as well is a `Field` and it has `Items`:

```eno
Names:
- Alice
- Bob
```

And finally, now without any ambiguity, this is an empty `Field`:

```eno
Name:
```

As we can see, nothing changes about our documents, just the way we conceptualize and label the elements has changed, reducing the amount of terminology required to describe what we see, and removing an ambiguity that only had drawbacks without giving us anything in return.

## Renaming the `Multiline Field`

An example for what's currently called a `Multiline Field`:

```eno
-- my_json
{
  "example_factor": 1.0
}
-- my_json
```

By changing what a `Field` is in Eno (now allowing it to hold associative attributes and list items in addition to just text) the sibling term `Multiline
Field` becomes somewhat unclear. Originally it used to be called `Block` but
that term was abandoned because as a metaphor it did not differentiate itself
from `Section` well enough.

Working with the metaphor that this element really offers a way to have a "document within a document", it is proposed to rename this element to `Embed` or `Heredoc`. (Feel free to open an issue to leave your comment/preference on this!)

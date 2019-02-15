# RFC: Restrict fields to a single line

This RFC seeks to establish that regular `Field` elements can never contain line breaks (`\n`) by repurposing the current newline continuation operator for new functionality.

## The two changes

### 1. `|`, the current *newline continuation operator*, becomes the *direct line continuation operator*

Currently the *newline continuation operator* exists and works like this:

```eno
> my_field contains a value of "First line\nSecond line"

my_field: First line
|         Second line
```

According to this proposal `|` becomes the *direct lined continuation operator* and works like this:

```eno
> my_field contains a value of "my-token-continued-wihout-gap"

my_field: my-token-
|         continued-wihout-gap
```

### 2. `\` retains its current functionality but adopts a new name: the *spaced line continuation operator*

The functionality remains unchanged:

```eno
> my_field contains a value of "my value continued with gap"

my_field: my value
\         continued with gap
```

## Design considerations

**Considerations around conveying meaning through document structure**

An integral part of the reasoning behind this RFC is to establish a predictable dichotomy of single line data versus multi line data, a concept that is firmly established and known to the likely widest technological user base there can be: people who use a browser (in the form of the single line text `input` and the multi line `textarea`). By guaranteeing that fields only ever contain a single line the nature of data to be supplied becomes much more intuitively clear to users, and although a savvy user might still try to change a field into a block then, the barrier to such misuse and potential ensuing errors is considerably higher.

**Cultural bias considerations**

This RFC also exists because the initial specification (which only offers one way to continue a line - separated by a space) neglects that in some cultures a line continuation that does not introduce an extra space might be customary instead.

(Thanks to Tomoki Aonuma for pointing this out - see https://github.com/eno-lang/eno/issues/3)

**Relation to Multiline Field Terminology RFC**

This RFC relates to the changes proposed in `multiline-field-terminology.md`.
If a `Field` only ever contains a single line, the therein proposed `Multline Field`
terminology complements that behavior on the descriptive side as well. (On the functional side the existing `Block` element already complements the herein described single-line only field).

**What is (not) lost, what is gained**

In early eno language drafts there were only *line continuations*, mostly to allow this:

```eno
my_command: foo -u alice
\               -p 1234567890
```

Additional *newline continuations* were introduced to allow this:

```eno
my_command:
| foo -u alice
\     -p 1234567890
| foo -u bob
\     -p abcdefghijklmnopqrstuvwxyz
```

But this can be stored (even more semantically I would argue) as a list too:

```eno
my_command:
- foo -u alice
\     -p 1234567890
- foo -u bob
\     -p abcdefghijklmnopqrstuvwxyz
```

And based on this RFC we actually gain new possibilities:

```eno
my_request: https://mydomain.com/api/foo/request/?id=aw45ojhi9aw4
|                                                &options=compact,files
|                                                &page=3
|                                                &lang=fr

my_key:
| tQpVvLtVrOAQKJusuehMorHqvNOVmTrLPvVVEfMGeiSdfXQWdDgpGMhfQwc
| WprgefVgAgRhaOivsTvLDOwxIndAtpspeEmmsbkfrlsKIGVgrMegbCGtSWC
| jtLbcQFULKUtmpYCbRAwSEVqZuzoXdWCaTfDUXhPInlsHliQAOkTvcGkVvr
| xtHYYVBMfYsKdhyBAdyyiwdttoyLBUzwZLSNYnwPhkSYdaVUPldOwzeygiA
```

## Continuation behavior details

There are some not so obvious scenarios and edge cases to consider here - the 4 following examples should completely cover these ambiguities. If you spot an oversight or something is yet unclear you're very welcome to open an issue to bring it up - thank you!

**1. There is no leading/trailing spacing**

```eno
field:
\
\ value
\

> results in 'value' (leading/trailing spacing is discarded)
```

**2. The spacing produced by spaced line continuations does not accumulate**

```eno
field:
\ value
\
\
\ continued

> results in 'value continued' (*one* separating space only)
```

**3. Empty spaced line continuations between direct line continuations are taken into account**

```eno
field:
| value
\
| continued

> results in 'value continued'
```

**4. Multiple empty spaced line continuation between direct line continuations do not accumulate**

```eno
field:
| value
\
\
| continued

> results in 'value continued' (*one* separating space only)
```

## Revision history

**rev1:** Added a section to clarify continuation behavior details and edge case scenarios

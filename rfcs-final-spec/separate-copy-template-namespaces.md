# RFC: Separate copy template namespaces for non-section and section elements

This RFC proposes to establish that non-section and section elements both only reference templates for copying in their own separate namespaces.

Consider the following eno document:

```eno
copy < template

template: value

# template
```

In the initial eno specification and implementations this triggers an error because `template` is resolved against all elements in the document, and it is therefore not clear which of the two elements named `template` should be copied. The same applies for this scenario:

```eno
template: value

# template

# copy < template
```

However, given that in both documents one of the two amiguous options does not make sense anyway because a section can not be copied into a non-section element and vice versa, it makes a lot more sense to let both section and non-section elements reside in their own namespaces. That way both scenarios can unambiguously be resolved without error.

Note: The original, existing behavior described here was never consciously specified, but resulted out of the first library implementation process. During work on prerelease libraries for the final eno specification it now became clear that this was an oversight and unnecessary limitation in the design.

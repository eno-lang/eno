# RFC: Exclude fieldsets from section deep merging

**This RFC proposes to treat fieldsets appearing in deep-copied sections like any other non-section element, excluding it from deep merging and instead doing simple element replacement when a fieldset with an identical key appears both in a section and the template section it is being copied from.**

Most everyone is probably unaware of this feature, but up to now, in the initial eno implementations it is possible to merge two fieldsets with the same key indirectly by putting them within deep-copied sections. During work on the new prerelease libraries it became apparent that this feature can exhibit somewhat confusing element type-instability in certain scenarios, which, given its obscurity and complexity in the first place led to this RFC. The matter is rather complex so here's an example to illustrate what's problematic about the existing behavior:

## Issue example - Step 1

```eno
# default
## grouping
configuration:
setting 1 = parameters
setting 2 = parameters

# specific << default
## grouping
configuration:
- setting 1
- setting 2
```
In the example above the user overrides the default fieldset-style `configuration` with a list-style `configuration`, which resolves to this after deep merging:

```eno
# specific
## grouping
configuration:
- setting 1
- setting 2
```

## Issue example - Step 2

The user now removes 2 items from his list-style `configuration`, still with the intent of overriding the default fieldset-style `configuration`, only this time with an empty list:

```eno
# default
## grouping
configuration:
setting 1 = parameters
setting 2 = parameters


# specific << default
## grouping
configuration:
```
What actually happens though is that during deep merging `configuration` now appears as an ambiguous empty element (either field, fieldset or list), and as a potential merge target for the default `configuration` fieldset it now takes on that type and ends up being a verbatim copied fieldset instead of an empty list (which was the user's intention):
```eno
# specific
## grouping
configuration:
- setting 1
- setting 2
```

Bottom line of this: The user is confused because removing items from a list resulted in the element type changing. Following this RFC the thing that the user expected would have happened instead - `configuration` just would have been overridden with whatever the user expliclity specified (an empty list here in step 2).

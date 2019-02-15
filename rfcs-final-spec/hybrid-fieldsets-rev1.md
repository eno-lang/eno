# RFC: Hybrid fieldsets

This RFC proposes adopting the hybrid usage concept found in sections for fieldsets, allowing them to be used both as simple key-value stores (think attributes of an XML tag, this is already the current fieldset specification) and additionally also as an ordered document structure (think XML tags, consecutive elements whose names can reappear, to store e.g. chronological key-value data).

Right now fieldsets only allow this kind of usage:

```eno
generic_configuration:
debug = no
errors = yes
info = no
warnings = yes

specific_configuration < generic_configuration
debug = yes

image:
src = my_image.png
title = My image
```

Following this RFC they would also be able to represent this:

```eno
init_procedure:
ruby-2.5.3 = clean.rb
ruby-2.5.3 = seed.rb
ruby-2.5.3 = tests.rb
npm = compile
shell = ls -ah > files_snapshot.txt

dialogue_lines:
Alice = Hi Bob.
Bob = Hey Alice!
Alice = What's up?
Bob = Not much!
```

## Pro

- More consistency - with this change entries in fieldsets behave like fields in sections
- More flexibility through more usage patterns, as outlined above

## Contra

- More complex APIs - the fieldset APIs need adaptations to support the additional new behavior
- More complex merging behavior - consider this:

  ```eno
  settings:
  color = red
  color = green
  foo = bar
  number = one

  settings_2 < settings
  color = blue
  number = two
  number = three
  ```

  `color` and `number` from `settings` are discarded, resulting in this resolved fieldset:

  ```eno
  settings_2:
  color = blue
  foo = bar
  number = two
  number = three
  ```
  (Note that this consideration might be more hypothetical than relevant for actual usecases though)

## Usecases wanted!

Whether to write and publish this RFC was not an easy decision, there seems to be fairly balanced reasoning for both adopting and not adopting it, so seeing plausible usecases that justify its adoption would help greatly in making the final decision. Please open an issue if you've encountered scenarios that would benefit from this change if you'd like to help out, thanks!


## Revision history

**rev1:** Replaced the JSON metaphors explaining the merging behavior with actual eno notation to avoid misunderstandings.

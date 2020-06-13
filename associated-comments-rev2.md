# RFC: Comments associated with immediately following elements (revision 2)

This RFC proposes to give consecutive comment lines *immediately preceding* an element special significance by associating them with the element.

Consider the following eno document:

```eno
> My first comment

My first element: A value

> My second comment
My second element: Another value
```

Following this proposal the second comment would get associated with the second element when the document is parsed, making it available through the parser API for instance in the following way (for javascript in this example):

```js
const comment = document.element('My second element').comment();
  // returns 'My second comment'
```

The first comment on the other hand would get no association to the following element because of the empty line separating both:

```js
const comment = document.element('My first element').comment();
  // returns null
```

Consecutive comment lines would be combined into a single string, following the herein described whitespace rules:

```eno
>
> Leading and trailing empty lines are kept
> Indentation shared by all lines is stripped
>
>   Further indentation on individual lines is kept
>
      > Indentation is calculated relative to the comment operator
      >
      >
> All empty comment lines appearing inbetween non-empty lines are kept
> Whitespace on empty lines and trailing whitespace on all lines is removed
>
My element: A value
```

```js
const comment = document.element('My element').comment();
  // returns a string equivalent to result below

const result =
  '\n' +
  'Leading and trailing empty lines are kept\n' +
  'Indentation shared by all lines is stripped\n' +
  '\n' +
  '  Further indentation on individual lines is kept\n' +
  '\n' +
  'Indentation is calculated relative to the comment operator\n' +
  '\n' +
  '\n' +
  'All empty comment lines appearing inbetween non-empty lines are kept\n' +
  'Whitespace on empty lines and trailing whitespace on all lines is removed\n'
;
```

Note that mixing tabs and spaces unintuitively interfers with indentation stripping. This circumstance was extensively considered in the making of this RFC and found to be an acceptable trade-off: A "clean" behavior without side-effects would only be possible by giving up indentation stripping (too great a sacrifice in functionality) or enforcing consistent indentation on parsing (this would confuse non-professional users who might inadvertently mix tabs and spaces without even being aware of their existence - in fact even without them being aware of associated comments).

This is how the mixed tab/spaces scenario would be handled:

```eno
>·⇥·space-tab-space
>··⇥space-space-tab
>·⇥⇥space-tab-tab
```

would result in

```js
'⇥·space-tab-space\n·⇥space-space-tab\n⇥⇥space-tab-tab'
```

Associated comments would not functionally change anything about the way existing eno documents work, therefore they would be completely harmless to introduce, but at the same time would offer a great deal of added flexibility and facilitate usecases such as documentation generation, or allowing custom metadata notation for domain specific usecases, eg. an inline schema, type annotations. etc.

Another point in favor of this is probably that it adds functionality without making the language more complex for non-technical users - relying on these associated comments for implementing something would be at the discretion of application architects and developers.

On the contra side this will have a small impact on parsing performance, as well as adding some complexity to parser implementation.

In conclusion some more examples for comments associated with other element types:

```eno
> My comment
# My section

> My comment
My list:

> My comment
- My list item

> My comment
My fieldset:

> My comment
My field = My value
```

## Revision history

**rev2:** Revised the indentation processing rules: Stripping shared indentation relative to a general baseline (as rev1 proposed) turns out to be an extremely complex behavior to specify and implement considering the fact that spaces and tabs could be used and mixed both before and after the comment operator, leading to a multitude of strange and for document authors hardly understandable parsing results. Referencing the comment operator as the baseline for indentation stripping greatly simplifies things: The only problematic behavior results of mixing tabs and spaces in the indentation past the operator, this is an accepted edge case and users are expected to provide sane input.

**rev1:** Completely revised the example for multiline associated comments to describe in detail what whitespace behavior is proposed. This includes a change of indentation processing - while the original example somewhat loosely implied stripping all leading and trailing whitespace, the now proposed behavior only removes the baseline indentation shared across all lines and keeps relative indentation differences between lines intact.

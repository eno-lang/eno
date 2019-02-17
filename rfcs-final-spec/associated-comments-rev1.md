# RFC: Comments associated with immediately following elements (revision 1)

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
> Leading and trailing empty lines are removed
> Indentation shared by all lines is stripped
>
>   Further indentation on individual lines is kept
 >  Indentation is calculated relative to the general baseline
  > The comment operator can therefore appear at any indentation
   >
    >
> Empty comment lines are kept when they appear inbetween non-empty lines
> Whitespace on empty lines and trailing whitespace on all lines is removed
>
My element: A value
```

```js
const comment = document.element('My element').comment();
  // returns a string equivalent to result below

const result =
  'Leading and trailing empty lines are stripped\n' +
  'Indentation shared by all lines is stripped\n' +
  '\n' +
  '  Further indentation on individual lines is kept\n' +
  '  Indentation is calculated relative to the general baseline\n' +
  '  The comment operator can therefore appear at any indentation\n' +
  '\n' +
  '\n' +
  'Empty comment lines are kept when they appear inbetween non-empty lines\n' +
  'Whitespace on empty lines and trailing whitespace on all lines is removed'
;
```

This mechanism would not functionally change anything about the way existing eno documents work, therefore it would be completely harmless to introduce, but at the same time would offer a great deal of added flexibility and facilitate usecases such as documentation generation, or allowing custom metadata notation for domain specific usecases, eg. an inline schema, type annotations. etc.

Another point in favor of this is probably that it adds functionality without making the language more complex for non-technical users - relying on these associated comments for implementing something would be at the discretion of application architects and developers.

On the contra side this will introduce a small (although likely negligible) performance impact on parsing, although enabling this behaviour behind an API flag would be a possible option to remedy this, should it be relevant at all.

Lastly this also looks like it could have potential to take on a life of its own, giving birth to unpredictable usage conventions that might establish themselves in the community, possibly including problematic ones, but potentially also leading to fantastic developments :)

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

**rev1:** Completely revised the example for multiline associated comments to describe in detail what whitespace behavior is proposed. This includes a change of indentation processing - while the original example somewhat loosely implied stripping all leading and trailing whitespace, the now proposed behavior only removes the baseline indentation shared across all lines and keeps relative indentation differences between lines intact.

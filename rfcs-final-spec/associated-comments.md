# RFC: Comments associated with immediately following elements

This RFC proposes to give consecutive comment lines *immediately preceding* an element special significance by associating them with the element.

Consider the following eno document:

```eno
> My first comment

My first element: A value

> My second comment
My second element: Another value
```

Following this proposal the second comment would get associated with the second element when the document is parsed, making it available through the parser API for instance in the following way (for enojs in this example):

```js
const comment = document.element('My second element').comment();
  // returns 'My second comment'
```

The first comment on the other hand would get no association to the following element because of the empty line separating both:

```js
const comment = document.element('My first element').comment();
  // returns null
```

Consecutive comment lines would be bundled together as a single string, following eno's whitespace rules:

```eno
> My comment spans
>      two lines
My element: A value
```

```js
const comment = document.element('My element').comment();
  // returns 'My comment spans\ntwo lines'
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

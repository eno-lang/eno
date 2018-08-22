# FAQ

## How can I express a value with leading/trailing or only whitespace?

Use a block - a block's value is retained verbatim, all newlines and whitespace are conserved:

```eno
-- my_block

  my content  

-- my_block
```

In the rare case where a document needs to contain a high number of single-line
values that include leading/trailing or even only whitespace you can also
consider using a custom type syntax and loader to better express this concept in
your application, for instance:

```eno
> In our eno documents we use our own custom type syntax
> for expressing a whitespace-only value (3 spaces)

my_value: >   <
```

```js
// In our application code we define and utilize a
// reusable loader for loading our own custom type

const whitespace = ({ value }) => value.replace(/^>|<$/, '');

const myValue = document.field('my_value', whitespace);
```

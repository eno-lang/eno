# RFC: Disallow use of line continuations on copied fields

This RFC proposes to remove the currently supported mechanism of placing line continuations after a copied field to append to the copied value.

This is currently possible:

```eno
original field: my field value

-- original block
my
block
value
-- original block

> vvv This yields a field "copied field" with the value "my field value extended"

copied field < original field
\ extended

> vvv This yields a field "copied field" with the value "my\nblock\nvalue\nextended"

copied field < original block
| extended
```

While it's of course nice to have possibilities, this mechanism actually came to
be as a side effect in parallel to the specification of extendable list copies,
respectively modifiable fieldset copies, and in the interest of consistency
with those, not for its own sake.

In contrast to extending list-, or modifying fieldset copies, which to me both seem like
great features on the structural document level, continuations on copied fields always felt like an obscure, limited way to do string operations in eno, something that I never had any intention to integrate, but there it happened anyway.

Another consideration that has implications on future eno API library design possibilities is that currently by copying a block and continuing it with a line continuation the identity of that block gets somewhat muddled - it originally was a block, but by appending to it with a line continuation it somewhat turns into a field (that is literally what's happening in eno library implementations right now and I'm not happy about it).

This last paragraph also has relevance on complexity and performance - if a copied block can be altered, it can only be kept as a reference up to the point where it gets modified (= increased parser complexity), at which point costly memory allocation/duplication happens, possibly to only append a few characters to a very long string, something that could also be handled by applications themselves instead, in a more efficient way.

In consequence all of these considerations lead to this proposal - less might be more here.

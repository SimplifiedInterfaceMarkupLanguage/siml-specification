# Strong-Typed SIML Compilation

SIML can be deserialized into any type you define. Each `SIMLElement` expects one argument (a `SIMLNode` of a specific type) and returns a node of a specific type.

---

### Example 1
`siml.html5` returns an `HTMLTree` that represents a standard HTML5 tree. It expects a `SIMLObject` argument of type `HTMLNode`, such as `HTMLElementDiv`, `HTMLElementHead`, `HTMLElementBody`, and so on.

### Example 2
`siml.ehtml` also returns an `HTMLTree`, but it applies additional computation and post-processing, which may generate a different node structure than defined in the file.

```siml
siml.ehtml {
  .meta {
    .charset: utf8;
  }
}
```

produces the same `HTMLTree` as:

```siml
siml.html5 {
  head {
    meta {
      .charset: "utf8";
    }
  }
}
```

## Scope System

Different `div` elements may produce different outputs depending on the namespace. For example, `siml.html5.div` returns a standard `HTMLElement`, while `siml.ehtml.div` returns a post-processed `HTMLElement`. To simplify writing SIML, the language allows using namespaces for arguments. When a component or value is used, SIML resolves it by searching the nearest scope, continuing upward until a match is found.

### Example

In this example:

```siml
siml.ehtml {
  layout {
    div {}
  }
}
```

when resolving the `div` element, SIML first checks the namespace provided by `layout`, which contains no `div`. It then checks the `siml.ehtml` namespace, which provides a `siml.ehtml.div` element and it used.

### Scope optimizations

Some libraries can optimize scope search by providing global scope
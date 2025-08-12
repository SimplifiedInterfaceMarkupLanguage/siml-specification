# SIML Syntax Specification
---

### Base syntax:

```
Value -> 
    (String `;`)
  | (Number `;`)
  | Element
  | Text

Element ->
  Identifier (Object | Value | `;`)

Object ->
  `{` (Value | NamedObjectProperty)* `}`

NamedObjectProperty ->
  `.` Identifier `:` (Value | Object)

Text ->
  `[` AnyStringWithAnyWhitespace (Object AnyStringWithAnyWhitespace)* `]`

String ->
  `"` AnyStringWithEscaping `"` (Identifier)?

Number ->
  Integer (`.` Integer)? (Identifier)?
```

---

### Comments:

##### Line comments:
Comment starts from a `//*` and end with a `*//`. Anything inside a comment will be ignored by parser

```
//* This is a comment *//
```
# Weak-Type SIML parsing

SIML can be parsed into simple SIML-tree builded of SIMLNode.

### All SIMLNode types:

* `SIMLObject`:
  * named properties: `HashSet<String, SIMLNode>`
  * ordered properties: `List<SIMLNode>`
* `SIMLString`
  * source string: `String`
  * formatted string: `String`
  * string type: `String?`
* `SIMLNumber`:
  * integer part: `Integer64`
  * float part: `Integer64`
  * number type: `String?`
* `SIMLElement`:
  * element: `String`
  * argument: `SIMLNode?`
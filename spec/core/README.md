# SIML Specification

This document provides full documentation for SIML syntax and tree, that it provides

## Tree structure

### value
*value* is a base type, that can be any other type that listed there. 
It doesnt have any properties on itself.

**All possible value types are:**

* **object**
  Contains list of *named parameters* also know as *properties* and list of *unnamed parameters* also know as *children*. Defined as follow:
  ```siml
    {
      .propertyName: propertyValue;
      unnamedValue1; 
      unnamedValue2;
    }
  ```
  **Fields**:
  * `map<ident name, value>` **properties**
    Map of properties, defined like:
    ```siml
    { .name1: value1; .name2: value2; ... }
    ```
    Can't contain repeated keys
  * `list<value>` **children**
    List of child values, defined like:
    ```siml
      { value1; value2; ... }
    ```
* **component**
  Contains component name as ident and underlying value.
  Defined as follow:
  ```siml
  componentName anyValue;
  ```
  **Fields**:
  * `ident` **name**
    Component name
  * `value` parameter:
    Any underlying value, oftenly - object
* **identifier**
  Simple identifier symbol. Can represent reference to another field (see [scoping](../ui-simplified-tree/scoping/README.md)), any constant, enum value or even boolean.
* **string**
  Represents any string
* **number**
  *(TODO: Remove all of that and move out as optional, because for most of uscases float or double is fine)*
  Represents any integer or float number. 
  *(Implementation note: some implementations may store that as float or double without preserving original integer and float part, wich is not situable when you required to use fixed point math or know when value is defined like `0` or `0.`, please consider that when choosing implementation)*
  **Fields**:
  * `integer` **integer part**:
    integer part of an number. Defined as 0 in cases like `.123;`
  * `optional<optional<integer>>` **float part**
    Defined as `none` when `.` isn't typed (e. g. `10`),

    otherwise defined as `some(none)` when float part isnt typed (e. g. `10.`),
    
    otherwise defined as `some(some(float part))` when float part is defined (e. g. `10.2`)
  

## Syntax

Full syntax described in [ebnf file](./syntax.ebnf).
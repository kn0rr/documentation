# Primitive Types

There exists following `Primitive Types`:

    - Number: Numeric Value 
    - String: Text
    - Boolean: True|False
    - Null
    - Undefined
    - Symbol
    - BigInt

## Numbers

Working with numbers you can run also some mathematical operations, e. g. :

 - Modulo:  12%4=0 or 27%5=2
 - Power(Potenzieren): 2 ** 3=8 or 3 ** 2=9
 - ...

**NaN:**

Stands for not a Number but it is a numeric value that represents something that is not ... a number -> dividing by 0 or NaN + 5

**Infinity**

1/0 -> Inifinity

## String

Strings are indexed (Starting by 0), e. g.
````js
let test="hello"
hello[2]=l
````
You can use Methods, e. g. 
````js
let print="  priint   "
print.trim().toUpperCase();
````
will result in `PRIINT` without spaces and capitalized. 

**String Escapes:**

You can escape special characters so that you don't interfere with the normal javascript syntax (see also in [Escape-Notations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String))

    1. \n - newline
    2. \' - single quote
    3. \" - double quote
    4. \\ - backslash

**Embedded Expression**

You can have embedded expressions like:

````js
`I couned ${3+4} sheep`
````
-> Not single quotes they are back-tick characters!

Use `${}` and back-ticks to use variables,expressions or methods in the string

## Null and Undefined

**Null**: Intentional absence of any value; must be assigned

**Undefinded**: Varaibles that do not have an assigned value are undefined



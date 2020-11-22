# JavaScript Introduction

## Primitive Types

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

**Undefinded**: Varaibles that do nto have an assigned value are undefined

## Math Object

Some Examples:
````js
Math.PI // 3.141592653589793

//Absolute value:
Math.abs(-432) //432

// Raises 4 to the 5th power:
Math.pw(4,5) //1024

//Removes decimal 
Math.floor(3.9999) //3

// Returns random decimal
Math.random()

//Returns random decimal between 0 and 6
Math.random()*6

// Returns value between 0 and 6 with removed decimal!
Math.floor(Math.random()*6)
````

## Type Of

`typeof` is a operator like `+` or `-` and not a method so you don't need `()`

````js
typeof mystery //String
typeof undefinded //undefined
typeof null //object
typeof 2 //number
````

## parseInt & parseFloat

Used to parse strings into numbers, but watch out for NaN

````js
parseInt('24') //24
parseInt('24.987') //24
parseInt('28dayslater') //28
parseInt('28dayslater 2') //28
parseInt('a28dayslater') //NaN

parseFloat('24.987') //24.987
parseFloat('7') //7
parseFloat('i ate 2 mushrooms') //NaN
````

## Comparison Operator

````js
// ALL of them return a boolean true|false

> // greater then
< // less than
>= // greater or equal
<= // less or equal
== // Equality
!= // Not Equal
=== // strict equlity (also the data type (number, integer) must be the same)
!== //strict non-equality
````

Examples for `==`:
````js
false==false //true
7=='7' //true
0==false //true
0=='' //true
null==undefined //true
````

Examples for `===`:
````js
// Should in most cases go with ===

2==='2' //false
2===2 //true
0===false //false
undefined ===0 //false
null = null //true
````
# Operators

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

## Logical Operator

````js
 && //AND
 || //OR
 ! //NOT

 //Precedence of the Operator
 // ! has the highest precedense then comes && and then || -> alter it by ()
 ! //runs first 
 && //runs seconds
 || //runs third
````
Further Info for precedence for other operator you can see in the [docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence).

## Ternary Operator

````js
//condition ? expIfTrue : expIfFalse
num ==== 7 ? consoloe.log('seven'): console.log('Not seven')

// if status is offline color should be red 
let color = status === 'offline'?'red':'green'
````
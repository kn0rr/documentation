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

## Arrays

### Array types
````js
//empty array
let students= [];
//array of strings
let colors= ['red','white','green'];
//array of numbers
let numbers= [1,2,3,4,5];
//a mixed array
let stuff=[true,3,'dog',null]
````
### Add or delete values
````js
//last item
stuff[stuff.length-1] //null

//change array values
stuff[1]=4 //stuff=[true,4,'dog',null]

// ADD item to the end 
//Not ideal approach
stuff[stuff.length]='yes' //stuff=[true,4,'dog',null,'yes']
//Push- add to end
stuff.push(1) //stuff=[true,4,'dog',null,'yes',1]
//Pop remove  from end
stuff.pop() //stuff=[true,4,'dog',null,'yes']
//shift remove from start
stuff.shift() //stuff=[4,'dog',null,'yes']
//unshift add to start
stuff.unshift('hi')//stuff=['hi',4,'dog',null,'yes']

//Also possible to add multiple values
stuff.unshift('do','it')//stuff=['do','it','hi',4,'dog',null,'yes']
````
### More Array Methods

````js
let numbers=[1,2,3]
let fruits=['apple','banana']
let color=['green','blue']
//concat: merge arrays (doesn't change the original arrays!)
numbers.concat(fruits) //[1,2,3,'apple','banana']
numbers.concat(fruits,color) //[1,2,3,'apple','banana','green','blue']

//includes: look for a value (not on IE available)
color.includes('green') //true
color.includes('yellow') //false
//includes after indes of one
color.includes('green',1) //false

//indexOf: just like str.indexOf returns the first index at which a given element can be found in the array or -1 if not present
numbers.indexOf(2) //3
//index of after indes of one
numbers.indexOf(3,1) //true
//check if value is there
number.indexOf(3)!==-1 //true
number.includes(3)//true 

//join: creates a string from array 
numbers.join() //"1,2,3"
numbers.join('&')//"1&2&3"

//reverse: reverses an array (changes the original!)
numbers.reverse(3,2,1)

color.revers().join('-') //"blue-green"
//slice: copy portion of an array (includes the first but not the last; doesn't change the original array)
numbers.slice(0,2) //[1,2]
color.slice() //['green','blue'] makes a copy of the original

//splice: remove/replace elements
// at index one, delete 0 elements and add 5
number.splice(1,0,5)//[3, 5, 2, 1]
//at index one, delete 1 element
numbers.splice(1,1)//[3,2,1]
//at index one, delete 1 element, add 4,5,6
numbers.splice(1,1,4,5,6)//[3, 4, 5, 6, 1]

//sort: sorts an array
numbers.sort() //[1, 3, 4, 5, 6]
// sort converting the elements into strings, then comparing their sequence of UTF-16 code unit values!!!!
numbers.splice(1,0,1000,2000)
numbers.sort()//[1, 1000, 2000, 3, 4, 5, 6]
numbers.splice(1,1,4400)//[1, 4400, 2000, 3, 4, 5, 6]
numbers.sort()//[1, 2000, 3, 4, 4400, 5, 6]
````

### Reference Types

The value of an array is stored in memory and javascript points at this value
e.g. :

````js
let nums =[1,2,3]
//nums=1233213412
let otherNums=nums //otherNums=1233213412
nums.push[9] //[1,2,3,9]
otherNums //[1,2,3,9] -> Because the variable points to the same memory reference!
otherNums.pop()//[1,2,3]
nums //[1,2,3] -> Also effected because of same reference!
````

### Const with arrays

With const you normally can't change the value like you do with let.
But if its reference remains the same you can change its value!

````js
const color=['green', 'blue']
color.push('yellow') //possible because reference will be the same
color[0]="red" //possible because reference will be the same
color=["orange","purple"] //not possible because reference will change!
````
>Therefore it is better to use const when working with arrays!

### Nested Arrays

We can store arrays into other arrays!

````js
//3 arrays in one array
const animal=[['tiger','ram'],['doe','ewe'],['dog','cat']]
animal[1] //['doe','ewe']
animal[1][1] //'ewe'
animal[2][1]='tiger' //['dog','tiger']

//Further nesting
const animal=[['tiger',['ram','cow']],['doe','ewe'],['dog','cat']]
animal[0][1][1] //'cow'
````

## Objects

Objects are collections of properties. A property is a key-value pair.
Instead of accessing data using an index, we use custom keys.
all keys are converted to strings (except for symbols).

````js
const animals={
    name: 'Rex',
    type: 'dog',
    age: 12
}

//access property:
animals.type//dog

//access property where key is a number:
const number={1:2}
number[1] //2 
animals.['name'] //'Rex'

//Use variable to look for value in object

const n=1
const prop ='name'
number[n] //2
animals[prop] // 'Rex'
animals.prop //undefined it is not working vor variables you have to use []

//Add and change values
const userReviews= {};

userReviews['user1']=3.0 //userReviews{user1:3.0}
userReviews.user2=2.5 //userReviews{user1:3.0, user2:2.5}
userReviews.user1=2.0 //userReviews{user1:2.0, user2:2.5}
userReviews.user1+=2.0 //userReviews{user1:4.0, user2:2.5}
userReviews.user2++ //userReviews{user1:4.0, user2:3.5}

//More Complex Object

const student= {
    firstName:'John',
    lastName:'Doe',
    strengths:['Math', 'Sports'],
    exams: {
        midterm: 50,
        final: 12
    }
}
//avg of scores
const avg =(student.exams.midterm+student.exams.final)/2 // 31
student.strengths[1] //'Sports'

// Multiple Objects in an Array

const shoppingCart=[
    {
        product: 'pencil',
        price: 0.5,
        quantity: 30
    },
    {
        product: 'rubber',
        price: 0.25,
        quantity: 50
    },
    {
        product: 'basket',
        price: 12.0,
        quantity: 10
    }
]

//Comparing arrays
let nums=[1,2,3] //nums->12546
let nums2=[1,2,3] // nums->456789

nums===nums2 //false because nums stores reference in 123456 and nums 2 in 456789
nums==nums2 //false because nums stores reference in 123456 and nums 2 in 456789

let moreNums=nums

moreNums===nums //true
moreNums===nums2 //false

//How to check values than
const user={
    name:'John'
    email:'john.doe@gmail.com'
    notifications:[]
}
//not working
if (user.notifications===[]){   
    console.log("no new Notifications")
}
// working
if (user.notifications.length===0){   
    console.log("no new Notifications")
}
// working
if (!user.notifications.length){   
    console.log("no new Notifications")
}



````
>Object is also a reference type like array (stores data in a reference) -> therefore use in most cases const

## Loops

### For Loops

````js
//Structure
for ([initialExpression];[condition];[increment]){
}

for (let i=0; i<=20; i++){
    let number=i;
    console.log(number)
}
//for-loops with array
const name=['thomas','peter','otto']
for (let i=0; i<name.length; i++){
    console.log(i,name[i])
}

//for-loops and objects
const students=[
    {
        name:'Joe',
        grade:5
    },
    {
        name:'Kai',
        grade:8
    },
    {
        name:'Ina',
        grade:10
    }
]
for (let i=0;i<students.length;i++){
    let student=students[i]
console.log(`${student.name} is ${student.grade}`)
}

//for-loops and strings
const word='Hello World'
for (let i=word.length-1; i>=0; i--){
    console.log(i,word[i])
}

//nested for-loops
const gameBoards=[
    [4,32,8,4],
    [64,8,32,2],
    [8,32,16,4],
    [2,8,4,2]
]
let totalScore=0;
for (let i=0;i<gameBoards.length; i++){
    let row=gameBoards[i];
    for(let j=0;j<row.length;j++){
        console.log(row[j]);
        totalScore+=row[j]
    }

}

````


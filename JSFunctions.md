# Functions

 Functions are reusable procedures. They allow us to write reusable, modular code.
 We define a "chunk" of code that we can then execute at a later point.

 ````js
 //Structure

 function functionName() {
     // do something
 }

 //Dice Roll function

 function rollDie() {
     let roll=Math.floor(Math.random()*6)+1;
     console.log(`Rolled: ${roll}`)
 }

 function throwDice(){
     rollDie();
     rollDie();
     rollDie();
     rollDie();
     rollDie();
     rollDie();
 }
 ````

## Parameter & Arguments

You can give a function an Input by passing an Argument to the function.
To enable this, the function needs to have parameters.
If argument for a parameter is missing it will be undefined.

````js

// name is the parameter of the Funciton and the Input e.g. 'Tim' would be an argument
function greetings(name){
    console.log(`Hi ${name}`)
}

 function throwDice(numRolls){
     for (let i=0; i<numRolls; i++){
         rollDie()
     }
 }
 
````
## Return

If the function should return something you need to define a The return statement ends function execution AND specifies the value to be returned ba that function

## Scope

The location where a variable is defined ditcates where we have access to that variable.

### Function Scope

````js
function helloWorld() {
    let message="Hello World" //message is scoped to the helloWorld function
    message; //Hello World
}

message; //NOT defined
````

### Block Scope

````js
let radius =8;

if (radius > 0 {
    const PI=3.14 // PI is scoped to the block
    let circ =2*PI*radius; //circ is scoped to the block
    var test='test' //var has a different scope then let and const; var is scoped to the function not to the block!
})
console.log(radius); // 8
console.log(PI);// NOT DEFINED
console.log(circ); //NOT DEFINED
console.log(test) //test  
````

### Lexical Scope

````js
function outer(){
    let text='Hallo'
    function inner(){
        console.log(text.toUpperCase());
    }
    inner(); //HALLO
}
inner() // UNDEFINED because the function inner is only known to function outer
````
## Function Expression

Another syntax to define a function

````js
// All of them are valid!
function squ(num){
    return num*num
}
squ(7)//49

const square = function (num){
    return num*num;
}
square(7) //49

const square = function mulitply(num){
    return num*num;
}
square(7) //49
````

> Functions are Objects, therefore you can store them in a variable!

## Higher Order Functions

````js

function add(x,y){
    return x+j
}
function subtract(x,y){
    return x-j
}
function multiply(x,y){
    return x*j
}
function divide(x,y){
    return x/j
}
const operations=[add,subtract,multiply,divide];

operation [0](100,4) //104
operation [1](100,4) //96
operation [2](100,4) //400
operation [3](100,4) //25

for(let func of operations){
   let result= func(30,5)
   console.log(result);
}
//35
//25
//150
//6

//By adding a function to an Object, we created a method!
const thing={
    doSomething: multiply
}
thing.doSomething(50,2) //100

````

Higher Order functions are functions that operate on/with other functions. They can 
- Accept other functions as arguments
- Return a function

````js
//Accepting other functions as arguments

function callTwice(func){
    func();
    func();
}

function laugh(){
    console.log("HAHAHAHA")
}
callTwice(laugh);
//HAHAHAHA
//HAHAHAHA

function repeatNTimes(action,num){
    for (let i=0;i<num;i++){
        action();
    }
}
repeatNTimes(laugh,3);
//HAHAHAHA
//HAHAHAHA
//HAHAHAHA
````

````js
//Returning a function

function multiplyBy(num){
    return function(x) {
        return x*num
     }
}


const triple = multiplyBy(3) 
triple(6)//18
tirple(2)//6
const double = multiplyBy(2)
double(6) //12
double(2) //4


function makeBetweenFunc(x,y){
    return function(num){
      return num >= x && num <= y
    }
}
const isChild=makeBetweenFunc(0,18);

isChild(17) //true
isChild(99) //false
````

## Callback Functions

A callback funciton is afunction passed into another function as an argument, which is then invoked inside the outer function.

````js
function callTwice(func){
    func();
    func();
}

function laugh(){
    console.log("HAHAHAHA")
}
callTwice(laugh);//pass a function as an argument-> laugh is the Callback Function!
//HAHAHAHA
//HAHAHAHA

//Other Example
function grumpus() {
    alert("hello")
}
//setTimeout() method sets a timer which executes a funciton or specified piece of code once the timer expires
setTimeout(grumpus, 5000)

//or
setTimeout(function () {
    alert("welcome")
},5000)

````

## Hoisting

````js
//Hoisting for VAR-Variables

console.log(animal) // If I run only this we get an error 
//Uncaught ReferenceError: animal is not defined
//But if i run both it returns undefined, because JavaScripts defines first all var-variables which is called Hoisting.
var animal='Tapir'

//Hoisting for let-Variables

console.log(tiger)
let tiger='Tiger is an animal'
//When i run both there will be an error
//Uncaught ReferenceError: Cannot access 'tiger' before initialization
//Different behaviour like for VAR variables, but it's more likely the bevaiour we want to watch, so prefer let over VAR!


//Hoisting with functions

speak() //this is working because Javascripts interpreter process the function beforehand
function speak() {
    console.log("I can speak")
}

//This gives back the same error as for defining a normal let variable, because it works in the same way! 
//Uncaught ReferenceError: Cannot access 'speaker' before initialization
speaker()
let speaker=function speak() {
    console.log("I can speak")
}
````

## Arrow Functions

Syntactically compact alternative to a regular funciton expression.
But there is a different behaviour when you are working with **`this`**!

````js
const square = function (x){
    return x*x
}
// Is the same like :
const square=(x)=>{
    return x*x;
}
//brackets are optional if you have only ONE parameter
const square=x=>{
    return x*x;
}
//With multiple or no parameter you need to use brackets
const multiply=(x,y)=>{
    return x*y;
}
const helloWorld=()=>{
  console.log('Hello World!')
}

````
### Implicit Return

````js
// "Regular" arrow function:
const square = n => {
  return n * n;
}
// Implicit Return, on multiple lines using parens
const square1 = n => (
  n * n
)

// Implicit return one-liner:
const square2 = n => n * n;


const nums = [1, 2, 3, 4, 5, 6, 7, 8];

// ALL THREE VERSIONS GIVE US THE SAME RESULT:
const doubles1 = nums.map(function (n) {
  return n * 2;
})

const doubles2 = nums.map(n => {
  return n * 2;
})

const doubles3 = nums.map(n => n * 2);


const parityList = nums.map(function (n) {
  if (n % 2 === 0) return 'even';
  return 'odd';
})

const parityList1 = nums.map((n) => {
  if (n % 2 === 0) return 'even';
  return 'odd';
});
const parityList2 = nums.map((n) => (
  n % 2 === 0 ? 'even' : 'odd'
));

const parityList3 = nums.map((n) => n % 2 === 0 ? 'even' : 'odd');

````

# Type Annotations and Type inference

## Definition

`Type annotations` -> Code we add to tell Typescript what type of value a variable will refer to.

`Type inference` -> Typescript tries to figure out what type ofvalue a variable refers to.

`Type annotations:` We (developers) tell Typescript the type <--->`Type inference:`Typescript guesses the type

## Annotation Examples

![Annotation](img/typescript/annotation.svg)

```ts
------------------------------
// Annotations

// with variables
let apples: number = 5;

let speed: string = 'fast';
let hasName: boolean = true;

let nothingMuch: null = null;
let nothing: undefined = undefined;

// built in objects

let now: Date = new Date();

// Array

let colors: string [] = ['red', 'green', 'blue'];
let myNumbers: number [] =[1,2,3,4];
let truths: boolean [] = [false, true, false];

// Classes

class Car {
}

let car: Car = new Car();

// Object literal

let point: {x: number; y: number} = {
  x: 10,
  y: 20
}

// Function

// we expect a value of i which is a number and a return value of void (which indicates that we don't want to return anything)
const logNumber: (i: number)=>void = (i: number) =>{
  console.log(i);
}
------------------------------

```

## Inference Examples

![Inference](img/typescript/inference.svg)

![Inference2](img/typescript/inference2.svg)

## When to use what?

![Inference2](img/typescript/Annotation_vs_Inference.svg)

```ts
// When to use annotations

// 1) Function that returns the 'any' type

const json = '{"x": 10, "y": 20 }';

const coordinates = JSON.parse(json);

console.log(coordinates); // {x:10, y: 20};

// --> Fix Any Type: Assing annotation to coordinates

const coordinates: { x: number; y: number } = JSON.parse(json);

// 2) When we declare a variable on one line and initialize it later

let words = ['red', 'green', 'blue'];

let foundWord;

for (let i= 0; i< words.length; i++){#
if (words[i] === 'green'){
  foundWord = true;
  }
}

// --> Fix: Assing annotation to foundWord

let foundWord: boolean;

// 3)Variable whose type cannot be inferred correctly
let numbers = [-10, -1, 12];
let numberAboveZero = false;

for (let i = 0 ; i< numbers.length; i++){
  if (numbers[i]>0){
    numberAboveZero =numbers[i];
  }
}

// --> Fix: Add annotation with an "or" statement

let numberAboveZero: boolean | number = false;
```

![Any](img/typescript/any.svg)

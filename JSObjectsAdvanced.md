# Objects Advanced

## Shorthand Properties

````js
// const getStats = (arr) => {
//   const max = Math.max(...arr);
//   const min = Math.min(...arr);
//   const sum = arr.reduce((sum, r) => sum + r);
//   const avg = sum / arr.length;
// The "old" way:
//   return {
//     max: max,
//     min: min,
//     sum: sum,
//     avg: avg
//   }
// }

const getStats = (arr) => {
  const max = Math.max(...arr);
  const min = Math.min(...arr);
  const sum = arr.reduce((sum, r) => sum + r);
  const avg = sum / arr.length;
  // Using the new shorthand property syntax:
  return {
    max,
    min,
    sum,
    avg
  }
}
const reviews = [4.5, 5.0, 3.44, 2.8, 3.5, 4.0, 3.5];

const stats = getStats(reviews);

function pick(arr) {
  //return random element from arr
  const idx = Math.floor(Math.random() * arr.length);
  return arr[idx];
}

function getCard() {
  const values = [
    '1',
    '2',
    '3',
    '4',
    '5',
    '6',
    '7',
    '8',
    '9',
    '10',
    'J',
    'Q',
    'K',
    'A'
  ];
  const suits = ['clubs', 'spades', 'hearts', 'diamonds'];
  const value = pick(values);
  const suit = pick(suits)
  return {
    value,
    suit
  };
}
````

## Computed Properties

````js
const role = 'host';
const person = 'Jools Holland';
const role2 = 'Director'
const person2 = 'James Cameron'

// The old way: 
// Make the object
// const team = {};
// Then add a property using dynamic key:
// team[role] = person;
// team[role2] = person2;

// USING COMPUTED PROPERTIES!
const team = {
  [role]: person,
  [role2]: person2,
  [1 + 6 + 9]: 'sixteen'
}
/*
{ '16': 'sixteen', host: 'Jools Holland', Director: 'James Cameron' }
*/


// OLD WAY:
 function addProp(obj, k, v) {
   const copy = {
     ...obj
   };
   copy[k] = v;
  return copy;
 }
 const res=addProp(team,'happy', ':)')

 /*
 {
  '16': 'sixteen',
  host: 'Jools Holland',
  Director: 'James Cameron',
  happy: ':)'
}
 */
// New Way:
 const addProp = (obj, k, v) => {
  return {
    ...obj,
     [k]: v
  }
 }

const addProp = (obj, k, v) => ({
  ...obj,
  [k]: v
})
const res = addProp(team, 'happy', ':)')
````

## Adding Methods to Objects
We can add functions as properties on objects. 
**They are called Methods!**
You should use this to group functions.

### Long Way

````js
const add= function (x,y){
    return x+y
}
// Group add in Math object.
const math={
    add
}

// Normally you would do something like this

const math={
    numbers: [1,2,3,4,5],
    add: function(x,y){
        return x+y;
    },
    multiply: function (x,y){
        return x*y;
    }
}

````
### Short Way

````js
const auth = {
  username: 'TommyBot',
  login() {
    console.log("LOGGED YOU IN!")
  },
  logout() {
    console.log("GOODBYE")
  }
}
````

## Keyword This


````js
function sayHi() {
  console.log("HI")
  //this refers to the window (global scope object in the browser)
  console.log(this);
}

const greet = function () {
  //this refers to the window (global scope object in the browser)
  console.log(this);
}
````


## Shorthand Properties

````js
````
## Shorthand Properties

````js
````
## Shorthand Properties

````js
````
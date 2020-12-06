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

### Using This in Methods

Use the keyword `this` to access other properties on the same object.

````js
function sayHi() {
  console.log("HI")
  //this refers to the window (global scope object in the browser)
  console.log(this);
}


const person = {
  first: 'Cherilyn',
  last: 'Sarkisian',
  nickName: 'Cher',
  fullName() {
    //In a method, this refers to the object the method "lives" in:
    const {
      first,
      last,
      nickName
    } = this;
    return `${first} ${last } AKA ${nickName}`;
  },
  printBio() {
    const fullName = this.fullName();
    console.log(`${fullName} is a person!`)
  }
}
````
### THIS: Invoation Context

The value of this depends on the invocation context of the function it is used in.

````js
function sayHi() {
  console.log("HI")
  //this refers to the window (global scope object in the browser)
  console.log(this);
}

const person = {
  first: 'Cherilyn',
  last: 'Sarkisian',
  nickName: 'Cher',
  fullName() {
    //In a method, this refers to the object the method "lives" in
    const {
      first,
      last,
      nickName
    } = this;
    return `${first} ${last } AKA ${nickName}`;
  },
  printBio() {
    console.log(this);
    const fullName = this.fullName();
    console.log(`${fullName} is a person!`)
  },
  laugh: () => {
    //Arrow functions don't get their 'own' this.
    console.log(this); // Value is set to the window (global scope)
    console.log(`${this.nickName} says HAHAHAHAH`)
  }
}

// INVOCATION CONTEXT MATTERS!!!
person.printBio(); //THIS refers to the person object
// So you can say this refers to the Object on the left before the '.'
// If there is nothing left it will be the global scope object, the window!

const printBio = person.printBio;
printBio(); //THIS refers to window object which results in an error
// this.fullName is not a function

````

### This Example white Arrow Function

````js
const annoyer = {
  phrases: ["literally", "cray cray", "I can't even", "Totes!", "YOLO", "Can't Stop, Won't Stop"],
  pickPhrase() {
    const {
      phrases
    } = this;
    const idx = Math.floor(Math.random() * phrases.length);
    return phrases[idx]
  },
  start() {
    //Use an arrow function to avoid getting a different 'this':
    // Because Arrow function don't have their own this,  they refer to the this of start(), which refers to the object 'this', in our case phrases! 
    this.timerId = setInterval(() => {
      // We can specify a new property for this which we can later call in the scope of the object
      console.log(this.pickPhrase())
    }, 3000)
  },
  stop() {
    // here we call the timerId from this
    clearInterval(this.timerId);
    console.log("PHEW THANK HEAVENS THAT IS OVER!")
  }
}
````

## Real Life Example: "Deck of Cards"

````js
// **********************************
// WRITING EVERYTHING USING FUNCTIONS
// **********************************
function initializeDeck() {
  const deck = [];
  const suits = ['hearts', 'diamonds', 'spades', 'clubs'];
  const values = '2,3,4,5,6,7,8,9,10,J,Q,K,A';
  for (let value of values.split(',')) {
    for (let suit of suits) {
      deck.push({
        value,
        suit
      })
    }
  }
  return deck;
}

function drawCard(deck, drawnCards) {
  const card = deck.pop();
  drawnCards.push(card);
  return card;
}

function drawMultiple(numCards, deck, drawnCards) {
  const cards = [];
  for (let i = 0; i < numCards; i++) {
    cards.push(drawCard(deck, drawnCards));
  }
  return cards;
}

function shuffle(deck) {
  // loop over array backwards
  for (let i = deck.length - 1; i > 0; i--) {
    //pick random index before current element
    let j = Math.floor(Math.random() * (i + 1));
    //swap
    [deck[i], deck[j]] = [deck[j], deck[i]];
  }
  return deck;
}


// We have to create a bunch of variables:
const firstDeck = initializeDeck();
const drawnCards = [];
shuffle(firstDeck);
// We have to pass a ton of arguments around:
const hand1 = drawMultiple(2, firstDeck, drawnCards);
const hand2 = drawMultiple(2, firstDeck, drawnCards);
const pokerHand = drawMultiple(5, firstDeck, drawnCards);





// **********************************
// USING AN OBJECT + METHODS INSTEAD:
// **********************************

const myDeck = {
  deck: [],
  drawnCards: [],
  suits: ['hearts', 'diamonds', 'spades', 'clubs'],
  values: '2,3,4,5,6,7,8,9,10,J,Q,K,A',
  initializeDeck() {
    const {
      suits,
      values,
      deck
    } = this;
    for (let value of values.split(',')) {
      for (let suit of suits) {
        deck.push({
          value,
          suit
        })
      }
    }
    // return deck;
  },
  drawCard() {
    const card = this.deck.pop();
    this.drawnCards.push(card);
    return card;
  },
  drawMultiple(numCards) {
    const cards = [];
    for (let i = 0; i < numCards; i++) {
      cards.push(this.drawCard());
    }
    return cards;
  },
  shuffle() {
    const {
      deck
    } = this;
    // loop over array backwards
    for (let i = deck.length - 1; i > 0; i--) {
      //pick random index before current element
      let j = Math.floor(Math.random() * (i + 1));
      //swap
      [deck[i], deck[j]] = [deck[j], deck[i]];
    }
  }
}

// Much cleaner!!
myDeck.initializeDeck();
myDeck.shuffle();
const h1 = myDeck.drawMultiple(2);
const h2 = myDeck.drawMultiple(2);
const h3 = myDeck.drawMultiple(5);
````

### Deck Factory

````js
// THIS FUNCTION RETURNS A NEW DECK EVERYTIME WE CALL IT!
const makeDeck = () => {
  return {
    deck: [],
    drawnCards: [],
    suits: ['hearts', 'diamonds', 'spades', 'clubs'],
    values: '2,3,4,5,6,7,8,9,10,J,Q,K,A',
    initializeDeck() {
      const {
        suits,
        values,
        deck
      } = this;
      for (let value of values.split(',')) {
        for (let suit of suits) {
          deck.push({
            value,
            suit
          })
        }
      }
      // return deck;
    },
    drawCard() {
      const card = this.deck.pop();
      this.drawnCards.push(card);
      return card;
    },
    drawMultiple(numCards) {
      const cards = [];
      for (let i = 0; i < numCards; i++) {
        cards.push(this.drawCard());
      }
      return cards;
    },
    shuffle() {
      const {
        deck
      } = this;
      // loop over array backwards
      for (let i = deck.length - 1; i > 0; i--) {
        //pick random index before current element
        let j = Math.floor(Math.random() * (i + 1));
        //swap
        [deck[i], deck[j]] = [deck[j], deck[i]];
      }
    }
  }
}

// OUR FIRST DECK!
const myDeck = makeDeck();
myDeck.initializeDeck();
myDeck.shuffle();
const h1 = myDeck.drawMultiple(2);
const h2 = myDeck.drawMultiple(2);
const h3 = myDeck.drawMultiple(5);

// OUR SECOND DECK!
const deck2 = makeDeck();
deck2.initializeDeck()
````
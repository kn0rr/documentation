# Apply Functions to Collections of Data

## Array Callback Methods

Arrays come with many built-in methods that accept callback functions.

### FOREACH

Accepts a callback functions. Calls the funciton once per element in the array

````js
const nums= [9,8,7,6,5,4,3,2,1]

nums.forEach(function (n){
    console.log(n*n)
 //prints: 81,64,49,36,25,16,9,4,1
})

//Use second parameter to print the index
nums.forEach(function (el,idx){
    if(el%2===0){
        console.log(el, idx)
//prints: 8,6,4,2
    }
})

````

### MAP

Creates a new array with the results of calling a callback on every element in the array.

````js
const texts =['Hi','wie','geht','es','dir'];
const capitalize = texts.map(function(t){
    return t.toUpperCase();
})
texts; //'Hi','wie','geht','es','dir'
capitalize; //["HI", "WIE", "GEHT", "ES", "DIR"]

const numbers = [20,21,22,23,24,25,26,27]

//Create Array with Objects
const numDetail=numbers.map(function (n){
    return {
        value: n,
        isEven: n%2===0
    }
})
/*
[
  { value: 20, isEven: true },
  { value: 21, isEven: false },
  { value: 22, isEven: true },
  { value: 23, isEven: false },
  { value: 24, isEven: true },
  { value: 25, isEven: false },
  { value: 26, isEven: true },
  { value: 27, isEven: false }
]
*/

//Work with strings

const words =['asap','byob','rsvp','diy']

const abbrevs = words.map(function(word){
    return word.toUpperCase().split('').join('.');
})
//[ 'A.S.A.P', 'B.Y.O.B', 'R.S.V.P', 'D.I.Y' ]

//Work with Objects in an Array

const books = [{
    title: 'Good Omens',
    authors: ['Terry Pratchett', 'Neil Gaiman'],
    rating: 4.25
  },
  {
    title: 'Bone: The Complete Edition',
    authors: ['Jeff Smith'],
    rating: 4.42
  },
  {
    title: 'American Gods',
    authors: ['Neil Gaiman'],
    rating: 4.11
  },
  {
    title: 'A Gentleman in Moscow',
    authors: ['Amor Towles'],
    rating: 4.36
  }
]

const titles = books.map(function (b) {
  return b.title;
})
//["Good Omens", "Bone: The Complete Edition", "American Gods", "A Gentleman in Moscow"]
````

### FIND

Returns the value of the first element in the array that satisfies the provided testing function.

````js
let movies= {
    "The Fantastic Mr. Fox",
    "Mr. and Mrs. Smith",
    "Mrs. Doubtfire",
    "Mr. Deeds"
}

let movie =movies.find(movie=> {
    return movie.includes('Mrs.')
}) //Mr.and Mrs. Smit

let movie2=movies.find(m=>m.indexOf('Mrs')===0) // Mrs. Doubtfire

const books = [{
    title: 'Good Omens',
    authors: ['Terry Pratchett', 'Neil Gaiman'],
    rating: 4.25
  },
  {
    title: 'Bone: The Complete Edition',
    authors: ['Jeff Smith'],
    rating: 4.42
  },
  {
    title: 'American Gods',
    authors: ['Neil Gaiman'],
    rating: 4.11
  },
  {
    title: 'A Gentleman in Moscow',
    authors: ['Amor Towles'],
    rating: 4.36
  }
]
 books.find(b=> b.rating>=4.3) //{ title: 'Bone: The Complete Edition', authors: [ 'Jeff Smith' ], rating: 4.42 }
````

### Filter

Creates a new array with all elements that pass the test implemented by the provided function.

````js
const nums=[9,8,7,6,5,4,3,2,1];
const odds= nums.filter(n=>{
    return n%2===1; //Our callback returns true or false
    //if true, n is added to the filtered array
})
//9,7,5,3,1

const smallNums =nums.filter(n=>n<5);
//4,3,2,1

const books = [{
    title: 'Good Omens',
    authors: ['Terry Pratchett', 'Neil Gaiman'],
    rating: 4.25,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'Changing My Mind',
    authors: ['Zadie Smith'],
    rating: 3.83,
    genres: ['nonfiction', 'essays']
  },
  {
    title: 'Bone: The Complete Edition',
    authors: ['Jeff Smith'],
    rating: 4.42,
    genres: ['fiction', 'graphic novel', 'fantasy']
  },
  {
    title: 'American Gods',
    authors: ['Neil Gaiman'],
    rating: 4.11,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'A Gentleman in Moscow',
    authors: ['Amor Towles'],
    rating: 4.36,
    genres: ['fiction', 'historical fiction']
  },
  {
    title: 'The Name of the Wind',
    authors: ['Patrick Rothfuss'],
    rating: 4.54,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'The Overstory',
    authors: ['Richard Powers'],
    rating: 4.19,
    genres: ['fiction', 'short stories']
  },
  {
    title: 'The Way of Kings',
    authors: ['Brandon Sanderson'],
    rating: 4.65,
    genres: ['fantasy', 'epic']
  },
  {
    title: 'Lord of the flies',
    authors: ['William Golding'],
    rating: 3.67,
    genres: ['fiction']
  }
]

const goodBooks = books.filter(b=>b.rating>4.3)

const fantasyBooks=books.filter(book=> (
    book.genres.includes('fantasy')
))

const query='The'
const results =books.filter(book=>{
    const title=book.title.toLowerCase();
    return title.includes(query.toLowerCase())
})
````

### Every & Some

**EVERY:** Tests whether all elements in the array pass the provided function. It returns a Boolean value.
**SOME:**  Similar to every but returns true if ANY(just needs one to pass) of the array elements pass the test function

````js
const words = ['dog','dig','bag','log','wag']

words.every(word=>{
    return word.length==3;
}) //true

words.every(word=>[0]==='d') //false

words.some(word=>[0]==='d') //true

words.every(w=>{
    let last_letter=w[w.lenthg-1];
    return last_letter==='g'
})//true
````

### SORT

`arr.sort(compareFunc(a,b))`:
- If compareFunc(a,b) returns less than 0
    - Sort a before b
- If compareFunc(a,b) returns  0
    - Leave a and b unchanged with respect to each other
- If compareFunc(a,b) returns greater than 0
    - Sort b bevore a

````js
const prices=[400.50,333,99.99,35.99,12.00,9500]

prices.sort();// sort converting the elements into strings, then comparing their sequence of UTF-16 code unit values!!!!
//[ 12, 333, 35.99, 400.5, 9500, 99.99 ]

prices.sort((a,b)=>a-b)
//[ 12, 35.99, 99.99, 333, 400.5, 9500 ]
const ascSort=price.split().sort((a,b)=>a-b)


prices.sort((a,b)=>b-a)
//[ 9500, 400.5, 333, 99.99, 35.99, 12 ]
const descSort=price.split().sort((a,b)=>b-a)

const books = [{
    title: 'Good Omens',
    authors: ['Terry Pratchett', 'Neil Gaiman'],
    rating: 4.25,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'Changing My Mind',
    authors: ['Zadie Smith'],
    rating: 3.83,
    genres: ['nonfiction', 'essays']
  },
  {
    title: 'Bone: The Complete Edition',
    authors: ['Jeff Smith'],
    rating: 4.42,
    genres: ['fiction', 'graphic novel', 'fantasy']
  },
  {
    title: 'American Gods',
    authors: ['Neil Gaiman'],
    rating: 4.11,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'A Gentleman in Moscow',
    authors: ['Amor Towles'],
    rating: 4.36,
    genres: ['fiction', 'historical fiction']
  },
  {
    title: 'The Name of the Wind',
    authors: ['Patrick Rothfuss'],
    rating: 4.54,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'The Overstory',
    authors: ['Richard Powers'],
    rating: 4.19,
    genres: ['fiction', 'short stories']
  },
  {
    title: 'The Way of Kings',
    authors: ['Brandon Sanderson'],
    rating: 4.65,
    genres: ['fantasy', 'epic']
  },
  {
    title: 'Lord of the flies',
    authors: ['William Golding'],
    rating: 3.67,
    genres: ['fiction']
  }
]

books.sort((a,b)=>a.rating-b.rating)

````

## Reduce

Executes a reducer function on each element of the array, resulting in a single value.

````js
//Summing an Array
[3,5,7,9,11].reduce((accumulator, currentValue)=>{
    return accumulator+ currentValue;
})
````
What it actually do:
![Reduce_Example](img\javaScript\Reduce_Example.png)


### Finding Max Value

````js
let grades =[89,96,58,77,62,93,81,99,73]

const topScore= grades.reduce((max,currVal)=>{
    if (currVal>max) return currVal;
    return max;
})
topScore //99

//A shorter option with Math.max & implicit return
const maxGrade=grades.reduce((max,currVal)=>(
    Math.max(max,currVal)
))
//Same with Math.min
const minGrade=grades.reduce((min,currVal)=>(
    Math.min(min,currVal)
))

// Reducer with Initial Value

[4,5,6,7,8].reduce((accumulator,currentValue)=>{
    return accumulator+currentValue
})//30
[4,5,6,7,8].reduce((accumulator,currentValue)=>{
    return accumulator+currentValue
},100)//130

const votes = ['y', 'y', 'n', 'y', 'n', 'y', 'n', 'y', 'n', 'n', 'n', 'y', 'y'];

// To tally the votes:
// const results = votes.reduce((tally, val) => {
//   if (tally[val]) {
//     tally[val]++
//   } else {
//     tally[val] = 1;
//   }
//   return tally;
// }, {})

// The shorter version:
const voteResults = votes.reduce((tally, val) => {
  tally[val] = (tally[val] || 0) + 1;
  return tally;
}, {});

const books = [{
    title: 'Good Omens',
    authors: ['Terry Pratchett', 'Neil Gaiman'],
    rating: 4.25,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'Changing My Mind',
    authors: ['Zadie Smith'],
    rating: 3.83,
    genres: ['nonfiction', 'essays']
  },
  {
    title: 'Bone: The Complete Edition',
    authors: ['Jeff Smith'],
    rating: 4.42,
    genres: ['fiction', 'graphic novel', 'fantasy']
  },
  {
    title: 'American Gods',
    authors: ['Neil Gaiman'],
    rating: 4.11,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'A Gentleman in Moscow',
    authors: ['Amor Towles'],
    rating: 4.36,
    genres: ['fiction', 'historical fiction']
  },
  {
    title: 'The Name of the Wind',
    authors: ['Patrick Rothfuss'],
    rating: 4.54,
    genres: ['fiction', 'fantasy']
  },
  {
    title: 'The Overstory',
    authors: ['Richard Powers'],
    rating: 4.19,
    genres: ['fiction', 'short stories']
  },
  {
    title: 'A Truly Horrible Book',
    authors: ['Xavier Time'],
    rating: 2.18,
    genres: ['fiction', 'garbage']
  },
  {
    title: 'The Way of Kings',
    authors: ['Brandon Sanderson'],
    rating: 4.65,
    genres: ['fantasy', 'epic']
  },
  {
    title: 'Lord of the flies',
    authors: ['William Golding'],
    rating: 3.67,
    genres: ['fiction']
  }
]
// To group books by rating: 
const groupedByRatings = books.reduce((groupedBooks, book) => {
  const key = Math.floor(book.rating);
  if (!groupedBooks[key]) groupedBooks[key] = [];
  groupedBooks[key].push(book)
  return groupedBooks;
}, {})
````
# Loops

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

### While Loop

````js
//Structure
let j=0;
while (j<=5){
    console.log(j)
    j++;
}
````

### For...Of (No IE)

A nice and easy way of iterating over arrayrs (or other iterable objcets)
````js
//Structure
for (variable of iterable){
    statement
}
//Example with Array

let colors=['green', 'blue','yellow','black','white']

for (color of colors){
    console.log(color)
}

const magicSquare =[
    [2,7,6],
    [9,5,1],
    [4,3,8]
]

for (let row of magicSquare){
    let sum=0
    for (let num of row){
        sum+=num
    }
    console.log(`${row}summed to ${sum}` )
}

//Example with Object

const movieReviews={
    Arrival : 9.5,
    Alien: 9,
    Amelie:8,
    'In Bruges': 9,
    Amadeus: 10,
    'kill Bill': 8,
    'Little Miss Sunshine': 8.5,
    Coraline: 7.5
}
// not Working! (because not iterabel object)
for (let x of movieReviews){
    console.log(x)
}
//Instead go over keys 

for (let movie of Objcet.keys(movieReviews)){
    console.log(movie, movieReviews[movie]);
}
//or  values
const ratings= Object.values(movieReviews);
let total=0;
for (let rating of ratings){
    total+=rating;
}
let avg =total/ratings.length;

console.log(avg)
````

### For...In Loop

Loop over the keys in an object

````js
//structur
for (variable in object){
    statement
}

//Example
const movieReviews={
    Arrival : 9.5,
    Alien: 9,
    Amelie:8,
    'In Bruges': 9,
    Amadeus: 10,
    'kill Bill': 8,
    'Little Miss Sunshine': 8.5,
    Coraline: 7.5
}

for (let movie in movieReviews){
    console.log(movie)
    console.log(movieReviews[movie])
}
````
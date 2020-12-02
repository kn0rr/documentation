# Arrays

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

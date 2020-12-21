
# DOM Selecting

There are different methods to select an element in the DOM.

- getElementById
- getElementsByTagName
- getElementsByClassName

And there also exists a method who rules them all:

- querySelector 
- querySelectorAll

````js
//Example for Google.de

//*********************
//getElementById
//*********************

// There can only exists one Element per ID because the ID must be unique! 
// If there exists an Element with this ID we get the Object
// If there exists non Element we get null
document.getElementById('gbqfbb') 
const btnObj = document.getElementById('gbqfbb')
console.dir(btnObj)
/*
input#gbqfbb
accept: ""
accessKey: ""
align: ""
more and more and more.....
*/

//*********************
// getElementsByTagName
//*********************

// We can get more then one element because tags are not unique
// The output will be stored in a list
// If there exists nothing it will be an empty collection
const inputTag=document.getElementsByTagName('input')

//Access the List (it is something like a leightweight array with less methods)
inputTag[0]
// <input name="source" type="hidden" value="hp">

// iterate over the List
for (let input of inputTag){
    console.log(input)
}
// but you can spread it into an array
const array = [...inputTag]
// or
for (let input of inputTag){
    console.log(input.value)
}

//*********************
// getElementsByClassName
//*********************

// We can get more then one element because classes are not unique
// The output will be stored in a list
// If there exists nothing it will be an empty collection
document.getElementsByClassName('header')

// For all methods you can further drill down the search e.g.:
// Except for getElementById because the ID is always unique within the whole document!
const ul = document.getElemetnsByTagName('ul')[0]
ul.getElemetnsByClassName('special')

````

### querySelector

A newer, all-in-one method to select `a single element`.
Pass in CSS selector.
It is a little bit less performant than the getElement methods.

````js
//*********************
// querySelector
//*********************

// Finds first h1 element
document.querySelector('h1')
//Finds first element with ID of red
document.querySelector('#red')
//Finds first element with class of big
document.querySelector('.big')
// Or more complex e.g. by looking by a list item from class big
document.querySelector('li.big')
// Or more complex e.g. by looking for a class big inside of the body which is in a selection which is in an unorderd list which is a list element
document.querySelector('body selection ul li.big')


//*********************
// querySelectorAll
//*********************

//Works the same as querySelector but returns a collection and not only the first result

//Finds all elements with class of big
document.querySelectorAll('.big')

````
# DOM Events

Events responding to user inputs and actions.
A small list:
- clicks
- drags
- drops
- hovers
- scrolls
- form submission
- key presses
- focus/blur
- mouse wheel
- double click
- copying
- pasting
- audio start
- scree resize
- printing

## Two ways NOT to add an event

You shouldn't use the following approaches because it's really hard to handle them in a real life scenario.


````html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>2 Ways NOT to Add Event Listeners</title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <!-- BOOOOOOO Don't do this! -->
  <button onmouseover="alert('YOU CLICKED ME')">Click Me!</button>
  <!-- OR THIS! -->
  <button onclick="alert('YOU CLICKED ME TOO!')">Click Me TOO!</button>

  <button id="clicker">CLICKER</button>

  <form action="">
    <!-- OR THIS!!!! -->
    <input onclick="console.log('CLICKED THE INPUT')" type="range" min="10" max="50">
  </form>
  <script src="app.js"></script>
</body>

</html>
````
````js
// ***********************************
// Two ways NOT to add event handlers
// ***********************************

// **********************************
// Inline - take a look at index.html
// **********************************
// Check out index.html to see an example

// **********************************
// Via JS - setting the onclick property
// **********************************

// Select an element:
const btn = document.querySelector('#clicker');

// Set the onclick property to a function:

// You can use an existing function: (not that common)
// btn.onclick = greet; 

// Or use an anonymous function (more common)
btn.onclick = () => {
  console.log('YOU CLICKED ME UGHHHH!!');
}

function greet() {
  alert('HEY BUDDY!')
}
````

## addEventListener

Specify the event type and a callback to run

````js
const button=document.querySelector('h1');

button.addEventListener('click',()=>{
    alert("You clicked me!!")
}

const btn = document.querySelector('button');

btn.addEventListener('click', function() {
	alert('CLICKED!!!');
});

btn.addEventListener('click', function() {
	console.log('SECOND THING!!');
});

btn.addEventListener('mouseover', function() {
	btn.innerText = 'STOP TOUCHING ME';
});

btn.addEventListener('mouseout', function() {
	btn.innerText = 'Click Me!';
});

window.addEventListener('scroll', function() {
	console.log('STOP SCROLLING!!');
});

````

## The Impossible Button

Small demo of a button that can never be clicked

````html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>World's Most Annoying Button
  </title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <button>Try To Click Me!</button>
  <script src="app.js"></script>
</body>

</html>
````

````js
const btn = document.querySelector('button');

btn.addEventListener('mouseover', function() {
	console.log('MOUSED OVER ME!');
	const height = Math.floor(Math.random() * window.innerHeight);
	const width = Math.floor(Math.random() * window.innerWidth);
	btn.style.left = `${width}px`;
	btn.style.top = `${height}px`;
});

btn.addEventListener('click', function() {
	btn.innerText = 'YOU GOT ME!';
	document.body.style.backgroundColor = 'green';
});

````
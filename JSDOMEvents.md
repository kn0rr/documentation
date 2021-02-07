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

## Events on Multiple Elements

It is possible to create multiple elements and also multiple events with the help of a loop.
This helps us to create a dynamic webpage based on the content of e.g. an array.

The HTML Code

````html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Multiple Events</title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <h1>Pick a Color</h1>
  <section id="boxes">

  </section>
  <script src="app.js"></script>
</body>

</html>
````
The Javascript Code:

````js
const colors = [
	'red',
	'orange',
	'yellow',
	'green',
	'blue',
	'purple',
	'indigo',
	'violet'
];
const changeColor = function() {
	const h1 = document.querySelector('h1');
	h1.style.color = this.style.backgroundColor;
};
const container = document.querySelector('#boxes');

for (let color of colors) {
	const box = document.createElement('div');
	box.style.backgroundColor = color;
	box.classList.add('box');
	container.appendChild(box);
	box.addEventListener('click', changeColor);
}

````

The Css-File:
`````css
#boxes {
	display: flex;
	justify-content: center;
	align-items: center;
}
.box {
	width: 200px;
	height: 200px;
}
h1 {
	text-align: center;
}

`````

## Event Object

Lets go with the example from above.
We are never executing `changeColor` ourself fits beeing called for us.
And it actually gets based an event object, which is sometimes extrem useful to have access to.
If we want to take a look into the event, we can pass ist as an argument and we will see the actual event if we console.log that stuff.

````js
const colors = [
	'red',
	'orange',
	'yellow',
	'green',
	'blue',
	'purple',
	'indigo',
	'violet'
];
const changeColor = function(event) {
  console.log(event)
	const h1 = document.querySelector('h1');
	h1.style.color = this.style.backgroundColor;
};
const container = document.querySelector('#boxes');

for (let color of colors) {
	const box = document.createElement('div');
	box.style.backgroundColor = color;
	box.classList.add('box');
	container.appendChild(box);
	box.addEventListener('click', changeColor);
}

````
The event shows us, which type of event e.g. `Mouse click` or on which position the event happend and further more e.g. `timestamp`.

If you execute the following code, you will see which key you pressed:

````js
document.body.addEventListener('keypress',function(e){console.log(e)})
````

Extract of the `console.log`- output:

````js
KeyboardEvent {isTrusted: true, key: "d", code: "KeyD", location: 0, ctrlKey: false, …}
````

So if you need further information on an event, you use access the event object!

## Key Events: keypress, keyup, keydown

Basic html page:

````html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Key Events</title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <input id="username" placeholder="username" type="text">
  <h3>Shopping List</h3>
  <input type="text" id="addItem" placeholder="enter a food">
  <ul id="items"></ul>
  <script src=" app.js"></script>
</body>

</html>
````
JavaScript code:

````js
const input = document.querySelector('#username');

// ***********************************
// Keydown: Anytime a key is pressed down
// ***********************************


input.addEventListener('keydown', function(e) {
	console.log('KEY DOWN!');
});

// ***********************************
// Keyup: Anytime a key is released
// ***********************************

input.addEventListener('keyup', function(e) {
	console.log('KEY UP!');
});

// ***********************************
// Keypress: everytime a key gets pressed and input gets changed
// ***********************************

//Some keys are not counted as keypress event, e.g. Shift does not count as keypressed event because input is not changing, only in combination with another letter 

//Keypress differs by browser!

input.addEventListener('keypress', function(e) {
	console.log('KEY PRESS!');
});

//practical example to use keypress to create new Item
const addItemInput = document.querySelector('#addItem');
const itemsUL = document.querySelector('#items');

addItemInput.addEventListener('keypress', function(e) {
	if (e.key === 'Enter') {
		if (!this.value) return; //if input is empty, skip everything
		//add a new item to list
		const newItemText = this.value;
		const newItem = document.createElement('li');
		newItem.innerText = newItemText;
		itemsUL.appendChild(newItem);
		this.value = '';
	}
});

````

## Form Events & PreventDefault 
Normally the form event is used to take you to a new endpoint, but with preventDefault you can intercept that default behaviour and do some other stuff.

````html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Form Events</title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <form id="signup-form" action="/NOOOO" method="get">
    <input type="text" placeholder="credit card" id="cc">
    <label>
      I agree to sell my soul to your company
      <input type="checkbox" id="terms">
    </label>
    <select name="" id="veggie">
      <option value="eggplant">Eggplant</option>
      <option value="asparagus">Asparagus</option>
      <option value="carrot">Carrot</option>
    </select>
    <input type="submit">
  </form>
  <script src=" app.js"></script>
</body>

</html>
````
JavaScript Code:

````js
// ***********************************
// Form Events and Prevent Default
// ***********************************

const form = document.querySelector('#signup-form');

const creditCardInput = document.querySelector('#cc');
const termsCheckbox = document.querySelector('#terms');
const veggieSelect = document.querySelector('#veggie');

form.addEventListener('submit', function(e) {
	e.preventDefault(); //stops the request from being sent (prevents page reload)
	console.log('cc', creditCardInput.value);
	console.log('terms', termsCheckbox.checked);
	console.log('veggieSelect', veggieSelect.value);
	//send form data to db
	//append something to page using form data
});
````

## Input & Change Events


The Input Event doesn't wait for a submit to happen, instead it gets called everytime when an input is happening!

The Change Event is called everytime when you switch the focus or hit enter in a textbox, so it is looking for an actuall change after a full input.

You could also manul

````js
// ***********************************
// Input & Change Events
// ***********************************

const creditCardInput = document.querySelector('#cc');
const termsCheckbox = document.querySelector('#terms');
const veggieSelect = document.querySelector('#veggie');
const formData = {};
// ONE callback works for any number of inputs!!
// It works dynamically for any type of input, which is really nice!
for (let input of [ creditCardInput, termsCheckbox, veggieSelect ]) {
	//Destrucutre, we want only the target of the event
  input.addEventListener('input', ({ target }) => {
    //further destructure, we only want these attributes from target
		const { name, type, value, checked } = target;
		formData[name] = type === 'checkbox' ? checked : value;
		console.log(formData);
	});
}

//Change Event:
for (let input of [ creditCardInput, termsCheckbox, veggieSelect ]) {
	//Destrucutre, we want only the target of the event
  input.addEventListener('change', ({ target }) => {
    //further destructure, we only want these attributes from target
		const { name, type, value, checked } = target;
		formData[name] = type === 'checkbox' ? checked : value;
		console.log(formData);
	});
}

//We could use hard-coded callbacks:
// creditCardInput.addEventListener('input', (e) => {
// 	console.log('CC CHANGED!', e);
// 	formData['cc'] = e.target.value;
// });

// veggieSelect.addEventListener('input', (e) => {
// 	console.log('VEGGIE!', e);
// 	formData['veggie'] = e.target.value;
// });

// termsCheckbox.addEventListener('input', (e) => {
// 	console.log('CHECKBOX', e);
// 	formData['agreeToTerms'] = e.target.checked;
// });



````

````html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Input/Change Events</title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <input name="creditCard" type="text" placeholder="credit card" id="cc">
  <label>
    I agree to sell my soul to your company
    <input name="agreeToTerms" type="checkbox" id="terms">
  </label>
  <select name="selectedVeggie" id="veggie">
    <option value="eggplant">Eggplant</option>
    <option value="asparagus">Asparagus</option>
    <option value="carrot">Carrot</option>
  </select>
  <script src=" app.js"></script>
</body>

</html>
````
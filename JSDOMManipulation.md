# DOM Manipulation

## Important Methods and Properties

- classList
- getAttribute()
- setAttribute()
- appendChild()
- prepend()
- removeChild()
- remove
- create Element
- innerText
- textContent
- innerHTLM
- value
- parentElement
- children
- nextSibling
- previousSibling
- style

## InnerText & textContent

````js
//Example for Google.de


//*********************
//      innerText
//*********************

const text=document.querySelector('#SIvCob')

// Inner Text is aware of the content that is on the screen and ignores the Text formatting like line breaks.
text.innerText
//"Google angeboten auf: English"

const footText=document.querySelector('#fsr')
//"DatenschutzerklärungNutzungsbedingungenEinstellungen"
// If we use innerText on an element we get all the innerText
document.body.innerText
/*
"Google angeboten auf: English
Deutschland
CO2-neutral seit 2007
DatenschutzerklärungNutzungsbedingungenEinstellungen
WerbeprogrammeUnternehmenWie funktioniert die Google Suche?"
*/

// You can also manipulate that 
document.body.innerText='Text' //cleans out the whole body and just shows Text


//*********************
//      textContent
//*********************

//textContent returns even hidden content and also returns the Text formatting like line breaks

const footer=document.querySelector('#fsr')

footer.textContent
/*
"DatenschutzerklärungNutzungsbedingungenEinstellungenSucheinstellungenErweiterte SucheMeine Daten in der Google SucheSuchverlaufHilfe zur SucheFeedback geben"
*/
````

## innerHTML

````js
//Example for Google.de

//*********************
//      innerHTML
//*********************

// innerHTML not only retrieves the text content but also all the tags in the element

const footer=document.querySelector('#fsr')

footer.innerHTML
/*
"<a class="Fx4vi" href="https://policies.google.com/privacy?hl=de&amp;fg=1" ping="/url?sa=t&amp;rct=j&amp;source=webhp&amp;url=https://policies.google.com/privacy%3Fhl%3Dde%26fg%3D1&amp;ved=0ahUKEwip9aDQ_rbtAhURnBQKHY-WDmkQ8awCCBU">Datenschutzerklärung</a><a class="Fx4vi" href="https://policies.google.com/terms?hl=de&amp;fg=1" ping="/url?sa=t&amp;rct=j&amp;source=webhp&amp;url=https://policies.google.com/terms%3Fhl%3Dde%26fg%3D1&amp;ved=0ahUKEwip9aDQ_rbtAhURnBQKHY-WDmkQ8qwCCBY">Nutzungsbedingungen</a><span jscontroller="GPhFgf" style="display:inline-block;position:relative"><a class="Fx4vi" href="https://www.google.de/preferences?hl=de" id="fsettl" aria-controls="fsett" aria-expanded="false" aria-haspopup="true" role="button" jsaction="noGWuc" ping="/url?sa=t&amp;rct=j&amp;source=webhp&amp;url=https://www.google.de/preferences%3Fhl%3Dde&amp;ved=0ahUKEwip9aDQ_rbtAhURnBQKHY-WDmkQzq0CCBc">Einstellungen</a><span id="fsett" aria-labelledby="fsettl" role="menu" style="display:none"><a href="https://www.google.de/preferences?hl=de&amp;fg=1" role="menuitem">Sucheinstellungen</a><a href="/advanced_search?hl=de&amp;fg=1" role="menuitem">Erweiterte Suche</a><a href="https://myactivity.google.com/privacyadvisor/search?utm_source=googlemenu&amp;fg=1" role="menuitem">Meine Daten in der Google Suche</a><a href="https://myactivity.google.com/product/search?utm_source=google&amp;hl=de&amp;fg=1" role="menuitem">Suchverlauf</a><a href="https://support.google.com/websearch/?p=ws_results_help&amp;hl=de&amp;fg=1" role="menuitem">Hilfe zur Suche</a><a href="#" data-bucket="websearch" role="menuitem" id="dk2qOd" target="_blank" jsaction="gf.sf" data-ved="0ahUKEwip9aDQ_rbtAhURnBQKHY-WDmkQLggY">Feedback geben</a></span></span>"
*/

//Manipulation with HTML Tags inside which is not poosible for innerText!
footer.innerHTML='<h1>Text</h1>'
footer.innerHTML+='<h2>Text2</h2>'
````

## Value, src, href and ohters

````js
//Example for Google.de

const inputs=document.querySelectorAll('input')

//Get value of first input in the list
input[0].value
//"de"
// Change placeholder
input[0].placeholder="Hallo Welt"
//"de"

//Manipulate value
input[0].value='en'

const a=document.querySelector('a')

a.href
/*
"https://www.google.de/webhp?hl=de&ictx=2&sa=X&ved=0ahUKEwiF9cKIirftAhVHrxoKHT-BCK0QPQgI"
*/
a.href="google.de"

const img=document.querySelector('img')

//Change picture
img.src='...'

````

## Getting & Setting Attributes

````js
// Some arbitrary examples

//*********************
//      getAttribute
//*********************

const range= document.querySlecotr('input[type="range"]')

range.getAttribute('max')
//500
range.getAttribute('min')
//100

//*********************
//      setAttribute
//*********************

range.setAttribute('min','-500')

//set Type to Radio Button
range.setAttribute('type','radio')
````

## Finding Parent / Children / Siblings

````js
// Some arbitrary examples

//*********************
//      parentElement
//*********************

//Get a List Item
const li = document.querySelector('li')

//Parent Element can be an unordered list
li.parentElement
//<ul>...</ul>
//You can also go further up and so on...
li.parentElement.parentElement
//<body>...</body>

//Get an Unordered List
const ul = document.querySelector('ul')

//*********************
//      children
//*********************


//Children element is most likely a collection of list item
ul.children
//HTMLCollection of list items
ul.children[0]
//<li>...</li>

//*********************
//      Siblings
//*********************
//Next Sibling is another li
li.nextElementSibling
//<li>2</li>
const thirdLi=li.nextElementSibling.nextElementSibling
//<li>3</li>
thirdLi.previousElementSibling
//<li>2</li>
````

## Manipulate Multiple Elements

````js
//Example for _data/index.html

// Select all LI's on the page:
const allLis = document.querySelectorAll('li');

// One option, a regular for loop:
for (let i = 0; i < allLis.length; i++) {
  allLis[i].innerText = 'WE ARE THE CHAMPIONS!'
}

//Another option using for...of:
for (let li of allLis) {
  li.innerHTML = 'WE ARE <b>THE CHAMPIONS</b>'
}

````

## Altering Styles

````js
//Example for _data/index.html

//*********************
//      Style
//*********************


//Only inline properties not changing the stylesheet-css

// Changing the color and background-color:
const h1 = document.querySelector('h1');
h1.style.color = 'pink';
h1.style.backgroundColor = 'yellow' //camel cased! (not background-color but backgroundColor)

// Changing Multiple Elements:
const allLis = document.querySelectorAll('li');
const colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple'];

allLis.forEach((li, i) => {
  const color = colors[i];
  li.style.color = color;
})

//*********************
//   getComputedStyle
//*********************

//Example for _data/index.html

const h1 = document.querySelector('h1');

// style property only contains INLINE styles...
// Even though we gave the h1 a purple color, we still get:
h1.style.color; //"" 
// Same with any property we did not set inline:
h1.style.fontSize; //""

// We can use getComputedStyle to figure out the ACTUAL styles that are applying:
const compStyles = getComputedStyle(h1);
compStyles.color; //"rgb(128, 0, 128)"  (purple as an RGB color)
compStyles.fontSize; //"60px"
````

## Manipulating Classes

````js
//Example for _data/index2.html

//*********************
//      classList
//*********************


/const todo = document.querySelector('#todos .todo');

// Setting styles one at a time is not ideal:
// todo.style.color = 'gray';
// todo.style.textDecoration = 'line-through';
// todo.style.opacity = '50%'


// We can use a class instead!
// In app.css I've defined a 'done' class that we can apply

// OPTION 1 - using setAttribute
//This adds the class 'done', but it overwrites any existing classes...
// todo.setAttribute('class', 'done');

// OPTION 2 - classList
// We can use the classList property and it's methods to add,remove, and toggle classes!
todo.classList.add('done');
//to remove it
todo.classList.remove('done');
//to toggle:
todo.classList.toggle('done'); //add
todo.classList.toggle('done'); //remove
todo.classList.toggle('done'); //add
todo.classList.toggle('done'); //remove
todo.classList.toggle('done'); //add
````

## Create Element, Append Child, Prepend & insertBefore

````js
//Arbitrary Examples

//*********************
//create Element & Append Child
//*********************


// Make a new empty img element:
const newImg = document.createElement('img');
// Add a src:
newImg.src = 'https://images.unsplash.com/photo-1504006833117-8886a355efbf?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2850&q=80';
// Change its width:
newImg.style.width = "300px";

//Add it to the end of the body:
document.body.appendChild(newImg);


// Create a new anchor tag
const newLink = document.createElement('a');
// Set its innerText:
newLink.innerText = 'Mr. Bubz Video! CLICK MEEE';
// Set its src:
newLink.href = 'https://www.youtube.com/watch?v=QQNL83fhWJU';

// Select the first paragraph:
const firstP = document.querySelector('p');
// Add the link as a child of the paragraph:
firstP.appendChild(newLink);

//*********************
//insertAdjacentElement*()
//*********************

const i = dcoument.createElement('i')
i.innerText= "Hello Again"

const firstP= document.querySelector('p')
//Add i BeforeBegin firstP 
firstP.insertAdjacentElement('beforebegin',i)
//Add i afterBegin firstP 
firstP.insertAdjacentElement('afterbegin',i)
//Add i afterend firstP 
firstP.insertAdjacentElement('afterend',i)

//*********************
//Append, Prepend & insertBefore
//*********************

const parentUL = document.querySelector('ul');
const newLI = document.createElement('li');
newLI.innerText = 'I AM A NEW LIST ITEM!';

//prepend will add newLI as the FIRST child of parentUL
parentUL.prepend(newLI) //Doesn't work in IE!
//append will add newLI as child of parentUL
parentUL.append(newLI) //Doesn't work in IE!

//We can also insert something BEFORE another element, using insertBefore.
// First, select the element to insert before:
const targetLI = document.querySelectorAll('li.todo')[2] //3rd li with class of 'todo'
// To insert our new LI before targetLI...
//parent.insertBefore(what to insert, where to insert)
parentUL.insertBefore(newLI, targetLI);
````

## Remove

````js
// USING removeChild()
//Select the element you want to remove;
const removeMe = document.querySelector('.special')
//We call removeChild() on the parent element and pass in the element we want to remove:
removeMe.parentElement.removeChild(removeMe)

// USING THE NEWER REMOVE() METHOD - NO INTERNET EXPLORER SUPPORT!
//Select the H1
const h1 = document.querySelector('h1');
h1.remove(); //REMOVE IT!
````

## Example Project: NBA Scores Chart

````css
/* app.css */
.win {
  background-color: rgba(0, 255, 0, 0.3);
}

.loss {
  background-color: rgba(255, 0, 0, 0.3);
}
````

````html
<!--index.html-->
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>NBA Score Table</title>
  <link rel="stylesheet" href="app.css">
</head>

<body>
  <section id="gs">
    <h2>Golden State Warriors</h2>
  </section>
  <section id="hr">
    <h2>Houston Rockets</h2>
  </section>
  <script src="app.js"></script>
</body>

</html>

````


````js
//app.js

//data:
const warriorsGames = [{
    awayTeam: {
      team: 'Golden State',
      points: 119,
      isWinner: true
    },
    homeTeam: {
      team: 'Houston',
      points: 106,
      isWinner: false
    }
  },
  {
    awayTeam: {
      team: 'Golden State',
      points: 105,
      isWinner: false
    },
    homeTeam: {
      team: 'Houston',
      points: 127,
      isWinner: true
    }
  },
  {
    homeTeam: {
      team: 'Golden State',
      points: 126,
      isWinner: true
    },
    awayTeam: {
      team: 'Houston',
      points: 85,
      isWinner: false
    }
  },
  {
    homeTeam: {
      team: 'Golden State',
      points: 92,
      isWinner: false
    },
    awayTeam: {
      team: 'Houston',
      points: 95,
      isWinner: true
    }
  },
  {
    awayTeam: {
      team: 'Golden State',
      points: 94,
      isWinner: false
    },
    homeTeam: {
      team: 'Houston',
      points: 98,
      isWinner: true
    }
  },
  {
    homeTeam: {
      team: 'Golden State',
      points: 115,
      isWinner: true
    },
    awayTeam: {
      team: 'Houston',
      points: 86,
      isWinner: false
    }
  },
  {
    awayTeam: {
      team: 'Golden State',
      points: 101,
      isWinner: true
    },
    homeTeam: {
      team: 'Houston',
      points: 92,
      isWinner: false
    }
  }
]

// **************************************************
// STEP 1 - UGLY, UN-REFACTORED CODE! (but it works!)
// **************************************************

/*
const ulParent = document.createElement('ul');
for (let game of warriorsGames) {
  const {
    homeTeam,
    awayTeam
  } = game;
  const gameLi = document.createElement('li');
  const {
    team: hTeam,
    points: hPoints
  } = homeTeam;
  const {
    team: aTeam,
    points: aPoints
  } = awayTeam;
  const teamNames = `${aTeam} @ ${hTeam}`;
  let scoreLine;
  if (aPoints > hPoints) {
    scoreLine = `<b>${aPoints}</b>-${hPoints}`;
  } else {
    scoreLine = `${aPoints}-<b>${hPoints}</b>`;
  }
  const warriors = hTeam === 'Golden State' ? homeTeam : awayTeam;
  gameLi.classList.add(warriors.isWinner ? 'win' : 'loss')

  gameLi.innerHTML = `${teamNames} ${scoreLine}`
  console.log(scoreLine)
  ulParent.appendChild(gameLi);
}

document.body.prepend(ulParent)
*/

// **************************************************
// STEP 2 - Refactored & Re-usable
// **************************************************

const makeChart = (games, targetTeam) => {
	const ulParent = document.createElement('ul');
	for (let game of games) {
		const gameLi = document.createElement('li');
		gameLi.innerHTML = getScoreLine(game);
		gameLi.classList.add(isWinner(game, targetTeam) ? 'win' : 'loss');
		ulParent.appendChild(gameLi);
	}
	return ulParent;
};

const isWinner = ({ homeTeam, awayTeam }, targetTeam) => {
	const target = homeTeam.team === targetTeam ? homeTeam : awayTeam;
	return target.isWinner;
};

const getScoreLine = ({ homeTeam, awayTeam }) => {
	const { team: hTeam, points: hPoints } = homeTeam;
	const { team: aTeam, points: aPoints } = awayTeam;
	const teamNames = `${aTeam} @ ${hTeam}`;
	let scoreLine;
	if (aPoints > hPoints) {
		scoreLine = `<b>${aPoints}</b>-${hPoints}`;
	}
	else {
		scoreLine = `${aPoints}-<b>${hPoints}</b>`;
	}
	return `${teamNames} ${scoreLine}`;
};

//Select the 2 sections to append to (from index.html)
const gsSection = document.querySelector('#gs');
const houstonSection = document.querySelector('#hr');

// Make the 2 charts:
const gsChart = makeChart(warriorsGames, 'Golden State');
const hrChart = makeChart(warriorsGames, 'Houston');

//Append them!
gsSection.appendChild(gsChart);
houstonSection.appendChild(hrChart);
````
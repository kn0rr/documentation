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
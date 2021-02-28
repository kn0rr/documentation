# Making HTTP Requests
 
Three types of requests
- XMLHTTP
- FETCH
- AXIOS 

## Intro to AJAX

Ajax stands for **A**synchronous **J**avascript **A**nd **X**ML. (But we will no longer use XML instead the modern way is to use json) -> Ajaj **A**synchronous **J**avascript **A**nd **J**SON.

## XMLHttpRequests: The Basics

- The "original" way of sending requests via JavaScript
- Does not support promises, so... lots of callbacks!
- Difficult syntax to remember

Example:

````js
//New request
const myReq = new XMLHttpRequest();
//if request successful
myReq.onload= function(){
    const data = JSON.parse(this.responseText);
    console.log(data);
}
//if error occurs
myReq.onerror = function(err){
    console.log('Error!',err);
};
//First parameter, what type of request, 
//second where the request should be send to
//
myReq.open('get', 'https://icanhazdadjoke.com/',true);
//header
myReq.setRequestHeader('Accept', 'application/json');
//send request
myReq.send();

````

Other Example:

````js
const firstReq = new XMLHttpRequest();
//its better to work with function instead of error function so you can use this
firstReq.addEventListener('load', function() {
	console.log('IT WORKED!!!');
    //`this` refers to the request itself
	const data = JSON.parse(this.responseText);
	for (let planet of data.results) {
		console.log(planet.name);
	}
});
firstReq.addEventListener('error', () => {
	console.log('ERROR!!!!!!');
});
firstReq.open('GET', 'https://swapi.dev/api/planets/');
firstReq.send();
console.log('Request Sent!');

````

````html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>XMLHttpRequests</title>
</head>

<body>

  <script src="app.js"></script>
</body>

</html>
````

## XMLHttpRequests: Chaining Requests

You need to use callbacks to call chained requests

````js
const firstReq = new XMLHttpRequest();
firstReq.addEventListener('load', function() {
	console.log('FIRST REQUEST WORKED!!!');
	const data = JSON.parse(this.responseText);
	const filmURL = data.results[0].films[0];
	const filmReq = new XMLHttpRequest();
	filmReq.addEventListener('load', function() {
		console.log('SECOND REQUEST WORKED!!!');
		const filmData = JSON.parse(this.responseText);
		console.log(filmData.title);
	});
	filmReq.addEventListener('error', function(e) {
		console.log('ERROR!!', e);
	});
	filmReq.open('GET', filmURL);
	filmReq.send();
});
firstReq.addEventListener('error', (e) => {
	console.log('ERROR!!!!!!');
});
firstReq.open('GET', 'https://swapi.dev/api/planets/');
firstReq.send();
console.log('Request Sent!');

````

## Fetch

- The newer way of making requests via JS
- Supports promises!
- Not supported in Internet Explorer ...

Example:

````js
fetch('https://icanhazdadjoke.com/25/2', {
    headers: {Accept: 'application/json'}
})
    .then((res)=>{
        if (res.status !==200){
            console.log('Problem!',res.status);
            return;
        }
        res.json().then((data)=>{
            console.log(data);
        });
    })
    .catch(function(err){
        console.log('Fetch Error', err);
    })
````

Rewrite chained XMLHttpRequest:

````js
// const firstReq = new XMLHttpRequest();
// firstReq.addEventListener('load', function() {
// 	console.log('FIRST REQUEST WORKED!!!');
// 	const data = JSON.parse(this.responseText);
// 	const filmURL = data.results[0].films[0];
// 	const filmReq = new XMLHttpRequest();
// 	filmReq.addEventListener('load', function() {
// 		console.log('SECOND REQUEST WORKED!!!');
// 		const filmData = JSON.parse(this.responseText);
// 		console.log(filmData.title);
// 	});
// 	filmReq.addEventListener('error', function(e) {
// 		console.log('ERROR!!', e);
// 	});
// 	filmReq.open('GET', filmURL);
// 	filmReq.send();
// });
// firstReq.addEventListener('error', (e) => {
// 	console.log('ERROR!!!!!!');
// });
// firstReq.open('GET', 'https://swapi.co/api/planets/');
// firstReq.send();
// console.log('Request Sent!');

fetch('https://swapi.dev/api/planetsuy21/')
    //The response is a readablestream which is not useful
	.then((response) => {
        //Fetch wont reject on HTTP error status (because you get a response)therefore we need to handle that in the way you see below!
		if (!response.ok)
        //throw new Error will trigger the catch-callback below!
			throw new Error(`Status Code Error: ${response.status}`);
    //We convert the readeblestream to json, the problem is it takes much time so it uses a promise, there we need to wait for the promise till it gets resolved (therefore need a `then` after response.json() )
		response.json().then((data) => {
			for (let planet of data.results) {
				console.log(planet.name);
			}
		});
	})
	.catch((err) => {
		console.log('SOMETHING WENT WRONG WITH FETCH!');
		console.log(err);
	});

//-> Chained:

fetch('https://swapi.dev/api/planets/')
	.then((response) => {
		if (!response.ok)
			throw new Error(`Status Code Error: ${response.status}`);

		return response.json();
	})
	.then((data) => {
		console.log('FETCHED ALL PLANETS (first 10)');
		const filmURL = data.results[0].films[0];
		return fetch(filmURL);
	})
	.then((response) => {
		if (!response.ok)
			throw new Error(`Status Code Error: ${response.status}`);

		return response.json();
	})
	.then((data) => {
		console.log('FETCHED FIRST FILM, based off of first planet');
		console.log(data.title);
	})
	.catch((err) => {
		console.log('SOMETHING WENT WRONG WITH FETCH!');
		console.log(err);
	});

//Refactoring Fetch Chain:

// Use method to check status and return promise
const checkStatusAndParse = (response) => {
	if (!response.ok) throw new Error(`Status Code Error: ${response.status}`);

	return response.json();
};

// Use method to load data and print it
const printPlanets = (data) => {
	console.log('Loaded 10 more planets...');
	for (let planet of data.results) {
		console.log(planet.name);
	}
    // return promise that is resolved
	return Promise.resolve(data.next);
};
// fetchNextPlantes with default URL later we will load data.next as url
const fetchNextPlanets = (url = 'https://swapi.co/api/planets/') => {
	return fetch(url);
};
//run with default url
fetchNextPlanets()
	.then(checkStatusAndParse)
	.then(printPlanets)
	.then(fetchNextPlanets) //run with url: data.next
	.then(checkStatusAndParse)
	.then(printPlanets)
	.then(fetchNextPlanets)
	.then(checkStatusAndParse)
	.then(printPlanets)
	.catch((err) => {
		console.log('SOMETHING WENT WRONG WITH FETCH!');
		console.log(err);
	});

````

## AXIOS

A library for making HTTP Requests.
Not the only library for HTTP Requests but the most popular one.

It uses Fetch behind the scenes. You can use that Client- and Server-Side.

Need to include Axios in the HTML File and before the JS-file otherwise javascript will not now axios.

````html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Axios Intro</title>
</head>

<body>
  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
  <script src="app.js"></script>
</body>

</html>
````

````js
axios
	.get('https://swapi.dev/api/planets/')
	.then((res) => {
		//We don't have to parse the JSON!
		console.log(res.data);
	})
	.catch((err) => {
		console.log('IN CATCH CALLBACK!!!');
		console.log(err);
	});

axios
	.get('https://swapi.dev/api/planetaslkjdaklsjds/') //BAD URL!
	.then((res) => {
		//We don't need to check for a 200 status code, because...
		//Axios will reject the promise for us, unlike fetch!
		console.log(res.data);
	})
	.catch((err) => {
		//In this example with a not-found URL, this callback will run...
		console.log('IN CATCH CALLBACK!!!');
		console.log(err);
	});

// ********************************
// USING FETCH INSTEAD...
// ********************************
// const checkStatusAndParse = (response) => {
// 	if (!response.ok) throw new Error(`Status Code Error: ${response.status}`);

// 	return response.json();
// };

// const printPlanets = (data) => {
// 	console.log('Loaded 10 more planets...');
// 	for (let planet of data.results) {
// 		console.log(planet.name);
// 	}
// 	return Promise.resolve(data.next);
// };

// const fetchNextPlanets = (url = 'https://swapi.co/api/planets/') => {
// 	return fetch(url);
// };

// fetchNextPlanets()
// 	.then(checkStatusAndParse)
// 	.then(printPlanets)
// 	.then(fetchNextPlanets)
// 	.then(checkStatusAndParse)
// 	.then(printPlanets)
// 	.then(fetchNextPlanets)
// 	.then(checkStatusAndParse)
// 	.then(printPlanets)
// 	.catch((err) => {
// 		console.log('SOMETHING WENT WRONG WITH FETCH!');
// 		console.log(err);
// 	});
````
## Sequential Axios Requests

````js
// ********************************
// CHAINING REQUESTS USING AXIOS
// ********************************
const fetchNextPlanets = (url = 'https://swapi.co/api/planets/') => {
	console.log(url);
	return axios.get(url);
};
const printPlanets = ({ data }) => {
	console.log(data);
	for (let planet of data.results) {
		console.log(planet.name);
	}
	return Promise.resolve(data.next);
};

fetchNextPlanets()
	.then(printPlanets)
	.then(fetchNextPlanets)
	.then(printPlanets)
	.then(fetchNextPlanets)
	.then(printPlanets)
	.catch((err) => {
		console.log('ERROR!!', err);
	});

// ********************************
// USING FETCH
// ********************************
// const checkStatusAndParse = (response) => {
// 	if (!response.ok) throw new Error(`Status Code Error: ${response.status}`);

// 	return response.json();
// };

// const printPlanets = (data) => {
// 	console.log('Loaded 10 more planets...');
// 	for (let planet of data.results) {
// 		console.log(planet.name);
// 	}
// 	return Promise.resolve(data.next);
// };

// const fetchNextPlanets = (url = 'https://swapi.co/api/planets/') => {
// 	return fetch(url);
// };

// fetchNextPlanets()
// 	.then(checkStatusAndParse)
// 	.then(printPlanets)
// 	.then(fetchNextPlanets)
// 	.then(checkStatusAndParse)
// 	.then(printPlanets)
// 	.then(fetchNextPlanets)
// 	.then(checkStatusAndParse)
// 	.then(printPlanets)
// 	.catch((err) => {
// 		console.log('SOMETHING WENT WRONG WITH FETCH!');
// 		console.log(err);
// 	});

````

## parseInt & parseFloat

Used to parse strings into numbers, but watch out for NaN

````js
parseInt('24') //24
parseInt('24.987') //24
parseInt('28dayslater') //28
parseInt('28dayslater 2') //28
parseInt('a28dayslater') //NaN

parseFloat('24.987') //24.987
parseFloat('7') //7
parseFloat('i ate 2 mushrooms') //NaN
````

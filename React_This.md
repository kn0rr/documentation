# How to fix issues with context or the 'this'-keyword

Many times we experience context issues which are most of the time related to the `this` keyword.
For a common use case we want to show different ways to handle this issue.

The following code will result in `TypeError: Cannot read properties of undefined (reading 'state')` because the context of `this` is not set correctly

````js

// The onFormSubmit function will result in an error
// TypeError: Cannot read properties of undefined (reading 'state')
// because of the context issue

import React from 'react';

class SearchBar extends React.Component {
   state ={ term: '' };

   onFormSubmit(event){
       //prevent browser to reload the page when pressing enter
        event.preventDefault();

        console.log(this.state.term);
   }
   
    render() {
        return (
        <div className="ui segment">
            <form onSubmit={this.onFormSubmit} className="ui form">
                <div className="field">
                    <label>Image Search</label>
                    <input type ="text" value={this.state.term} placeholder='Please endter text' onChange={e=>this.setState({term : e.target.value})}/>
                </div>
            </form>
        </div>)
    }
}

export default SearchBar;

````

Different solutions for the issue:

````js
/************
First way: Use Constructor
************/
[...]
    constructor(){
        super();

        //this produces a new function of onFormSubmit with the correct value of `this`
        this.onFormSubmit =this.onFormSubmit.bind(this);
    }
[...]

/************
Second way: Use Arrow function instead of Method
************/
[...]
// Arrow function doesn't implement an own `this`-keyword 
onFormSubmit = event =>{
    event.preventDefault();
        console.log(this.state.term);
}
[...]

/************
Third way: Use Arrow directly in the props
************/
[...]
 <form onSubmit={(e)=>this.onFormSubmit(e)} className="ui form">
[...]
   
````

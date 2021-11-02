# React Events

There are different types of event in most cases we want to handle events when user interacts with an element.

These three events events are commonly used:

![Events](img/react/diagrams-08-events.png)

There exists two general possibilities to work with events `uncontrolled` and `controlled`. We prefer **controlled** events, because with uncontrolled events the value is stored in the html element and we need to access the DOM tree to get the value and with controlled events we have the value in our react component.

## Uncrontrolled Events

Example:

````js
class SearchBar extends React.Component {
   onInputChange(event){
    console.log(event.target.value);
   }
   
    render() {
        return (
        <div className="ui segment">
            <form className="ui form">
                <div className="field">
                    <label>Image Search</label>
                    <input type ="text" onChange={this.onInputChange}/>
                </div>
            </form>
        </div>)
    }
}
// alternative with arrow function and simple e instead of event
class SearchBar extends React.Component {   
    render() {
        return (
        <div className="ui segment">
            <form className="ui form">
                <div className="field">
                    <label>Image Search</label>
                    <input type ="text" onChange={e=>console.log(e.target.value)}/>
                </div>
            </form>
        </div>)
    }
}

````

## Controlled Events

Example:

````js
import React from 'react';

class SearchBar extends React.Component {
   state ={ term: '' };
   
    render() {
        return (
        <div className="ui segment">
            <form className="ui form">
                <div className="field">
                    <label>Image Search</label>
                    <input type ="text" value={this.state.term} onChange={e=>this.setState({term : e.target.value})}/>
                </div>
            </form>
        </div>)
    }
}

export default SearchBar;
````

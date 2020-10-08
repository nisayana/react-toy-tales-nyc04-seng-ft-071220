# Solution Instructions
## Table of contents
* [Getting started](#getting-started)
* [Challenge 1](#challenge-1)
* [Challenge 2](#challenge-2)
* [Challenge 3](#challenge-3)
* [BONUS: Challenge 4](#challenge-4)

<a name="getting-started"/>

## Getting started
* Copy the repo URL and run `git clone` in your terminal. `cd` into the new directory and run these commands.

```
npm install -g json-server
json-server --watch db.json
```

* Open up a new terminal and run the following command:

```
npm start
```

* The terminal will ask you to start a new server since we already have the JSON server running on `localhost:3000`. Enter `y` to start a new server on `localhost:3001`.
* Open `http://localhost:3001` in the browser to see your app.
* Make a copy of `db.json` and save it as `original_db.json`. This is so that you can always refer back to the original database in case you mess up the database with incorrect PATCH requests.

<a name="challenge-1"/>

## Challenge 1
**Render the ToyCard component on to the page for each toy instance.**

What does this mean?
* Access the information about the toys from the backend (which is our `db.json` file).
* Send all the toy instances to the ToyContainer.
* Iterate through all the toy instances and return a ToyCard.

#### 1. In `App.js`, add a `toys` attribute to the state and assign it to an empty array.

```javascript
// app.js

state = {
  display: false,
  toys: []
}
```

#### 2. Write a `componentDidMount()` method and a GET fetch request to get all the toy instances.
Pass in `localhost:3000/toys` to the fetch request.
In the first `then` statement, take the response and turn it into a JSON object.

```javascript
// app.js

componentDidMount(){
  fetch("http://localhost:3000/toys")
  .then(r => r.json())
  .then()
}
```

In the second `then` statement, take the new toys array from our JSON object and change the state for the `toys` attribute. We're going to update the state so that the `toys` attribute is no longer an empty array, but instead, filled with all the new toy instances.

```javascript
// app.js

componentDidMount(){
  fetch("http://localhost:3000/toys")
  .then(r => r.json())
  .then((newToysArray) => {
    this.setState({
      toys: newToysArray
    })
  })
}
```

#### 3. Now that our state is updated with the new toys array, send it down to the ToyContainer component as props.
This will allow the ToyContainer component to access the toys array.

```javascript
// app.js

render(){
  return (
    <>
      <Header/>
      { this.state.display
          ?
        <ToyForm/>
          :
        null
      }
      <div className="buttonContainer">
        <button onClick={this.handleClick}> Add a Toy </button>
      </div>

      {/* here's where we're adding toys as props */}
      <ToyContainer toys={this.state.toys}/>
    </>
  )
}
```

#### 4. In `ToyContainer.jsx`, pass in `props` to the function argument.

```javascript
const ToyContainer = (props) => {
  return(
    <div id="toy-collection">
      {/* Render the collection of ToyCards */}
    </div>
  )
}
```

#### 5. Iterate through the toys props and return a ToyCard component for each instance.
Above the `return()` statement, create a new variable called `toysArray`.

```javascript
const ToyContainer = (props) => {

  // here's the new variable
  let toysArr

  return(
    <div id="toy-collection">
      {/* Render the collection of ToyCards */}
    </div>
  )
}
```

Use `map()` to iterate over the toys props and set this value to be `toysArray`.

```javascript
const ToyContainer = (props) => {

  let toysArr = props.toys.map()

  return(
    <div id="toy-collection">
      {/* Render the collection of ToyCards */}
    </div>
  )
}
```

Fill out the `map()` statement so that it returns a ToyCard component.

```javascript
const ToyContainer = (props) => {

  let toysArr = props.toys.map((toy) => {
    return <ToyCard />
  })

  return(
    <div id="toy-collection">
      {/* Render the collection of ToyCards */}
    </div>
  )
}
```

Send down the individual toy instance and its id attribute as props to the ToyCard component. Creating a `key` prop is a requirement in React when creating child components. The `key` props must be a totally unique value for each child component.

```javascript
const ToyContainer = (props) => {

  let toysArr = props.toys.map((toy) => {
    return <ToyCard key={toy.id} toy={toy}/>
  })

  return(
    <div id="toy-collection">
      {/* Render the collection of ToyCards */}
    </div>
  )
}
```

Et voilà! That is how you solve all the deliverables for this lab. 🌟
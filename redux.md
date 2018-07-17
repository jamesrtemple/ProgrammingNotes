# Three Principles
## Single Source of Truth
The state of your application is stored in an object within a single store.

## State is read-only
The only way to change the state is to emit an action, an object describing what happened.

## Changes are made with pure functions
To specify how the state tree is transformed by actions, you write pure reducers.

Example:
``` javascript
function visibilityFilter(state = 'SHOW_ALL', action) {
  switch (action.type) {
    case 'SET_VISIBILITY_FILTER':
      return action.filter
    default:
      return state
  }
}
```

# Basics
## Actions
Payloads of information that send data from your application to your store.

Good Practice:
Define a constant to represent the **action** type.

Example:
``` javascript
const ADD_TODO = 'ADD_TODO'

{
  type: ADD_TODO,
  text: 'Build my first redux app'
}
```

### Action Creators
Functions that create actions. They can be asynchronous and have side-effects.

Example:

``` javascript
function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  }
}
```

## Reducers
Pure functions that take the previous state and an action, and return the next state.

*Never* do these in a reducer:
1. Mutate arguments
2. Perform side effects like API calls and routing transitions
3. Call non-pure functions, e.g. `Date.now()` or `Math.random()`

### combineReducers
Redux provides the function `combineReducers()` to help simplify some boilerplate.

``` javascript
import { combineReducers } from 'redux'

const todoApp = combineReducers({
  visibilityFilter,
  todos
})

export default todoApp
```

...is equivalent to...

``` javascript
export default function todoApp(state = {}, action) {
  return {
    visibilityFilter: visibilityFilter(state.visibilityFilter, action),
    todos: todos(state.todos, action)
  }
}
```


## Store
The store has the following responsibilities:
- Holds application state
- Allows access to state via `getState();`
- Allows state to be updated via `dispatch(action);`
- Registers listeners via `subscribe(listener);`
- Handles unregistering of listeners via the function returned by `subscribe(listener);`
  
Call `createStore()` with your reducers and , optionally, your initial state if different from the initial state returned by the reducers.

``` javascript
import { createStore } from 'redux'
import todoApp from './reducers'
const store = createStore(todoApp)
//const store = createStore(todoApp, window.STATE_FROM_SERVER)
```


## Data Flow
Redux architecture revolves around a **strict unidirectional data flow**.

### 4 Steps in the data lifecycle
1. You call `store.dispatch(action)`
2. The Redux store calls the reducer function you gave it.
3. The root reducer may combine the output of multiple reducers into a single state tree.
4. The Redux store saves the complete state tree returned by the root reducer.


## Usage with React
`npm install --save react-redux`



# Advanced

## Async Actions

## Async Flow

## Middleware

## Usage with React Router



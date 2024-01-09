Redux Installation Steps

Library Installation

bash
npm i redux react-redux
Install the Redux library and the library developed specifically for React.

Store Setup:

Create a folder named 'redux' for Redux operations.
Inside, create a file named 'store.js'.
Import the createStore method from the Redux library.
Categorize the data stored in the store, and create a reducer for each category.
Combine the created reducers using the combineReducers method.
Introduce the combined reducers to the store.
Integrate the created store into the project.
javascript
// Example store
import { createStore, combineReducers } from 'redux';
import todoReducer from './reducers/todoReducer';
import categoryReducer from './reducers/categoryReducer';

// If there is only one reducer
export default createStore(todoReducer);

// If there are multiple reducers, combine them like this
const rootReducer = combineReducers({
    todoReducer,
    categoryReducer
})

export default createStore(rootReducer);
Reducers Setup:

Inside the 'redux' folder, create a subfolder to store reducers.
Inside the reducer folder, create a file named '...reducer.js'.
Create separate reducers for different data groups.
*Reducer: A function that decides how the data in the store will change.
Takes two parameters:
State: The current state of the data in the store.
Action: An object specifying how the store should be affected.
The data returned from the reducer is the updated state of the store.
'initialState' holds the initial values of the data to be stored.
javascript
// Example reducer
const initialState = {
    todos: [],
    isEmpty: true
}

const todoReducer = (state = initialState, action) => {
    switch (action.type) {
        case "ADD_TODO":
            // code
            return '';
        case "DELETE_TODO":
            // code
            return '';
        default:
            // code
            return state;
    }
}

export default todoReducer;
Provider:

Enables the introduction of the data stored in the store to the application.
Import Provider and the store into the main.jsx file.
If there is a console error, you may have skipped one of the installation steps.
javascript

import { Provider } from 'react-redux';
import store from './redux/store.js';

ReactDOM.createRoot(document.getElementById('root')).render(
    <Provider store={store}>
        <App />
    </Provider>
)
Sending Data to the Store:

In the component where you want to add data to the store, import useDispatch.
Use dispatch to send commands and data to the reducer.
The store cannot be directly modified; it is manipulated indirectly through reducers.
javascript

import { useDispatch } from 'react-redux';

const dispatch = useDispatch();

dispatch({
    type: "ADD_TODO",
    payload: newTodo
});
Retrieving Data from the Store:

Connect with the store using the useSelector method.
javascript

import { useSelector } from 'react-redux';

const state = useSelector((store) => store.todoReducer);

state.todos.map((todo, index) => <TodoCard key={index} todo={todo} />);
Action Types:

To prevent potential typos when manually writing action types, collect them in a separate file and import them everywhere.
javascript

export const ActionTypes = {
    ADD_TODO: 'ADD_TODO',
    DELETE_TODO: 'DELETE_TODO',
    UPDATE_TODO: 'UPDATE_TODO'
}

// Refer to them like this
case ActionTypes.ADD_TODO:
Actions:

Since typing the same code for command types and payload every time can be tedious, store these actions in a different file.
javascript

// Define an action without a payload
const ADD_COUNT = {
    type: 'ADD_COUNT',
};

// Define an action with a payload
export const deleteTodo = (payload) => ({
    type: ActionTypes.DELETE_TODO,
    payload
});

// Use it like this
dispatch(addTodo(newTodo));
Note:
In projects using both API and Redux, the store update should be dependent on the success of the API request.
javascript

axios.post('/todos', newTodo).then(() => {
    // After successfully recording to the API, send a command to the reducer
    dispatch(addTodo(newTodo))
})
Redux Image

Generating a Unique ID:
Use the universally unique identifier library.
Install the library.
bash

npm i uuid
Import it where you want to use.
javascript

import { v4 } from 'uuid';
Call the function.
javascript

id: v4()# Redux_CrudApp

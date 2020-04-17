# Redux
Architecture, conventions, recommendations about our use of Redux.

New to Redux? 

Please read this [online doc](https://redux.js.org/introduction/core-concepts) and further pages to get introduced to key concepts that won't be described here.

## Table of Contents
* [Ecosystem](#ecosystem)
* [Architecture and conventions](#architecture-and-conventions)
  * [Actions folder](#actions-folder)
  * [Reducers folder](#reducers-folder)
* [Good reads](#good-reads)

## Ecosystem

We use Redux as a global store inside our React application.

We depend on `react-redux` as an integration lib.

We also use thunks from `redux-thunk` to package multiple dispatch and/or API calls. 
More information about thunks on their [repo](https://github.com/reduxjs/redux-thunk).

## Architecture and conventions

`/store` is where we keep all logic related to store and state management. We split `actions` and `reducers`.

### Actions

`/actions` contains modules grouping all `actions`, `action creators`, `thunks` (side effects)  related to a data model object.

All `actions`, `action creators` and `thunks` are named exports inside said module.

#### Action symbols

Every `action` is represented by a `Symbol` to ensure its unicity while having human readable logs and names.
`action` names are always prefixed by their data model object's name.

Ex: 
```js
export const SSO_RESET = Symbol('SSO_RESET');
export const SSO_UPDATE = Symbol('SSO_UPDATE');
```

#### Action creators

`action creators` do not follow the standard flow architecture:
```json
{
  "type": "LOG_MESSAGE",
  "payload": {
    "message": "hey"
  }
}
```

Instead we have **flattened payloads**, which are optimized with es6 object rest features:
```json
{
  "type": "LOG_MESSAGE",
  "message": "hey"
}
```

#### Thunks

We try as much as possible not to mix API calls and store changes together as we chose to deprecate that pattern.

Most of our thunks only dispatch multiple actions.

It is recommended to create a thunk when dispatching multiple actions, so that you can reuse the new behaviour created seamlessly.

### Reducers folder

`/reducers` contains modules grouping all `selectors` and `reducers`  related to a data model object.
There are also some store specific helpers and wrappers in `/helpers`.

A `reducer` is the default export of a module, whereas `selectors` are grouped together inside a named export `selectors`.

#### Selectors

We use `reselect` for complex selectors ([repo](https://github.com/reduxjs/reselect)).

#### Reducers

`effects` from `actions` are separate functions inside a `reducer` for readability.

We use custom creators for `reducers`, such as `createReducer`, `createAuthReducer`.

This way we describe `initialState` then `actions` and their related `effect`.

Ex:
```js
const logMessage = (state, {message}) => ({
  ...state,
  message,
});

export default createReducer(initialState, {
  [LOG_MESSAGE]: logMessage,
});
```

## Good reads

- [Ducks pattern](https://github.com/erikras/ducks-modular-redux)
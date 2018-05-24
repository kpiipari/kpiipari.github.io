---
layout: post
title:      "Redux actions and action creators"
date:       2018-05-24 22:34:04 +0000
permalink:  redux_actions_and_action_creators
---


Actions are Javascript objects that consist of a type and a payload. 
Types are usually string constants whereas the payload can be a boolean value, a simple string or integer value or some data, usually passed in as JSON format.

Here’s an example action where the payload is a boolean.

```
{
        type: 'GAME_STARTED',
        gameStarted: bool
    }
```

Action creators are functions that create actions, simple as that.  Take can be called with an argument which is usually passed on as payload.

```
export function gameStarted(bool) {
    return {
        type: 'GAME_STARTED',
        gameStarted: bool
    }
}
```

They can also be called without an argument. Here’s an example of an action creator that returns an action containing a type ‘INCREMENT_COUNTER’ but no payload at all.

```
export function incrementCounter() {
    return {
        type: 'INCREMENT_COUNTER',
    }
}
```

Action creators can also be asynchronous. Here’s an example of a action creator that makes a GET request to a backend server and returns another action creator `roundFetchedSuccess` upon a successful fetch request.

```
export function fetchGameRound(gameRoute) {
    return dispatch => {
        return fetch(`${API_URL}/api/${gameRoute}/new`) 
        .then(response => response.json())
        .then(round => dispatch(roundFetchedSuccess(round)))
        .catch(error => dispatch(roundFetchFail(true, error)))
    }
}
```

Actions are the only way to provide any information and data to a Redux store. The store holds the application state and it’s the only way to get access to the state and update the state.

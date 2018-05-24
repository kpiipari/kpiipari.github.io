---
layout: post
title:      "MathOwl React-Redux Portfolio Project"
date:       2018-05-22 03:35:25 -0400
permalink:  mathowl_-_my_react-redux_project
---


My final portfolio project at Flatiron school is called MathOwl, which is a fun game to practice addition, subtraction and multiplications. The project consists of a React-Redux frontend with a Rail backend API. 

## Rails API

My API has four models: a player and three, almost identical, game models: Addition, Subtraction, Multiply. 
It uses postgreSQL database as I want to deploy my application to Heroku.

### Docker

I am actually running my API inside a Docker container which serves both the Rails application and the postgreSQL database.

## React frontend

I started my project by building a static React application where I hard coded each state. I have two containers: a GameContainer and a LeaderboardContainer. The GameContainer is where the actual game happens and the LeaderboardContainer provides a Leaderboard where players are ranked based on their total score.

### CSS

I decided to use [Semantic UI React](https://react.semantic-ui.com/introduction) integration of the Semantic UI framework. I was quite pleased to use Semantic UI. It was easy to use and I think my application looks modern and fresh.

### Redux

Once my application was working just with React, I added Redux that allows an easy to way to manage the application state. I used [Redux Thunk](https://github.com/reduxjs/redux-thunk) middleware that provides a convenient way for action creators to return ('dispatch') functions, and not just actions.  This is crucial when making asynchronous API calls with `fetch`.

See [my post ](http://kaisapiipari.com/redux_actions_and_action_creators) about Redux actions and action creators 

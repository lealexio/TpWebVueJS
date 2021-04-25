# TodoList VueJS and TypeScript

Simple API fetch project with Vue.

Created with Vue-cli, Vue, Typescript.

Deployed via CI/CD on Netlify.

You can view the app on netlify : [TodoList VueJS and TypeScript App](https://keen-thompson-ad0270.netlify.app/)


## Authors

Alexis Leloup

Manu Lagadec

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```



## Components

# App

The main component contains the router calls for navigation between views.

The router has been generated at the creation of the project.

## TaskList

`TaskList` contains all the methods needed to process the data. 

It also contains a class named `Todo` representing an element of a todo list. The task list is a list of `Todo` objects.

This component calls the TaskItem sub-component in charge of browsing the data and displaying them. The functions and data needed by this sub-component are given via the props.

A `Todo` object contain a String for the name of the task and a boolean var for checking.

## TaskItem

`TaskItem` inherits the functions of TaskList to perform operations on the data (the Todo list).

It forms the task list and manages the calls to the methods.


## Router

A router is used to navigate between views, it is defined in `index.ts`

## Views

There is two views :

* `Home` is the main view of the webApp.
* `About` is the authors view.


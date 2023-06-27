# React Tutorial

## Introduction 

As its official tagline states, React is a library for building user interfaces. React is not a framework – it's not even exclusive to the web. It's used with other libraries to render to certain environments. For instance, React Native can be used to build mobile applications.

React's primary goal is to minimize the bugs that occur when developers are building UIs. It does this through the use of components — self-contained, logical pieces of code that describe a portion of the user interface. These components can be composed together to create a full UI, and React abstracts away much of the rendering work, leaving you to concentrate on the UI design.

## Use Cases

Unlike the other frameworks covered in this module, React does not enforce strict rules around code conventions or file organization. This allows teams to set conventions that work best for them, and to adopt React in any way they would like to. React can handle a single button, a few pieces of an interface, or an app's entire user interface.

While React can be used for small pieces of an interface, it's not as easy to "drop into" an application as a library like jQuery, or even a framework like Vue — it is more approachable when you build your entire app with React.

In addition, many of the developer-experience benefits of a React app, such as writing interfaces with JSX, require a compilation process. Adding a compiler like Babel to a website makes the code on it run slowly, so developers often set up such tooling with a build step. React arguably has a heavy tooling requirement, but it can be learned.

This article is going to focus on the use case of using React to render the entire user interface of an application, using tooling provided by Facebook's own create-react-app tool.

## How does React use JavaScript?

```jsx
// JSX
const heading = <h1>Mozilla Developer Network</h1>;
```

This heading constant is known as a JSX expression. React can use it to render that `<h1>` tag in our app.

Suppose we wanted to wrap our heading in a `<header>` tag, for semantic reasons? The JSX approach allows us to nest our elements within each other, just like we do with HTML:

```jsx
// JSX
const header = (
  <header>
    <h1>Mozilla Developer Network</h1>
  </header>
);
```

Of course, your browser can't read JSX without help. When compiled (using a tool like Babel or Parcel), our header expression would look like this:

```jsx
// JSX
const header = React.createElement(
  "header",
  null,
  React.createElement("h1", null, "Mozilla Developer Network")
);
```

It's possible to skip the compilation step and use React.createElement() to write your UI yourself. In doing this, however, you lose the declarative benefit of JSX, and your code becomes harder to read. Compilation is an extra step in the development process, but many developers in the React community think that the readability of JSX is worthwhile. Plus, modern front-end development almost always involves a build process anyway — you have to downlevel modern syntax to be compatible with older browsers, and you may want to minify your code to optimize loading performance. Popular tooling like Babel already comes with JSX support out-of-the-box, so you don't have to configure compilation yourself unless you want to.

Because JSX is a blend of HTML and JavaScript, some developers find it intuitive. Others say that its blended nature makes it confusing. Once you're comfortable with it, however, it will allow you to build user interfaces more quickly and intuitively, and allow others to better understand your codebase at a glance.

## Setting up your first React app

There are many ways to use React, but we're going to use the command-line interface (CLI) tool create-react-app, as mentioned earlier, which expedites the process of developing a React application by installing some packages and creating some files for you, handling the tooling described above.

It's possible to add React to a website without create-react-app by copying some `<script>` elements into an HTML file, but the create-react-app CLI is a common starting point for React applications. Using it will allow you to spend more time building your app, and less time fussing with setup.

## Requirements

In order to use create-react-app, you need to have Node.js installed. It's recommended that you use the long-term support (LTS) version. Node includes npm (the node package manager), and npx (the node package runner).

You may also use the Yarn package manager as an alternative, but we'll assume you are using npm in this set of tutorials. See Package management basics for more information on npm and yarn.

If you're using Windows, you will need to install some software to give you parity with Unix/macOS terminal in order to use the terminal commands mentioned in this tutorial. Gitbash (which comes as part of the git for Windows toolset) or Windows Subsystem for Linux (WSL) are both suitable. See Command line crash course for more information on these, and on terminal commands in general.

Also bear in mind that React and ReactDOM produce apps that only work on a fairly modern set of browsers — IE9+ by way of some polyfills. It is recommended that you use a modern browser like Firefox, Microsoft Edge, Safari, or Chrome when working through these tutorials.

## Initializing your app

create-react-app takes one argument: the name you'd like to give your app. create-react-app uses this name to make a new directory, then creates the necessary files inside it. Make sure you cd to the place you'd like your app to live on your hard drive, then run the following in your terminal:

**Bash:** `$ npx create-react-app moz-todo-react`

This creates a `moz-todo-react` directory, and does several things inside it:

- Installs some npm packages essential to the functionality of the app.
- Writes scripts for starting and serving the application.
- Creates a structure of files and directories that define the basic app architecture.
- Initializes the directory as a git repository, if you have git installed on your computer.

create-react-app will display a number of messages in your terminal while it works; this is normal! This might take a few minutes, so now might be a good time to go make a cup of tea.

When the process is complete, `cd` into the `moz-todo-react` directory and run the command `npm start`. The scripts installed by create-react-app will start being served at a local server at localhost:3000, and open the app in a new browser tab.

## Application structure

create-react-app gives us everything we need to develop a React application. Its initial file structure looks like this:

```
moz-todo-react
├── README.md
├── node_modules
├── package.json
├── package-lock.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    ├── reportWebVitals.js
    └── setupTests.js
```

The src directory is where we'll spend most of our time, as it's where the source code for our application lives.

The `public` directory contains files that will be read by your browser while you're developing the app; the most important of these is index.html. React injects your code into this file so that your browser can run it. There's some other markup that helps create-react-app function, so take care not to edit it unless you know what you're doing. You very much should change the text inside the `<title>` element in this file to reflect the title of your application. Accurate page titles are important for accessibility!

The public directory will also be published when you build and deploy a production version of your app. We won't cover deployment in this tutorial, but you should be able to use a similar solution to that described in our Deploying our app tutorial.

The `package.json` file contains information about our project that Node.js/npm uses to keep it organized. This file is not unique to React applications; create-react-app merely populates it. You don't need to understand this file at all to complete this tutorial, however, if you'd like to learn more about it, you can read package.json on the npm blog; we also talk about it in our Package management basics tutorial.

## Exploring our first React component


In React, a **component** is a reusable module that renders a part of our app. These parts can be big or small, but they are usually clearly defined: they serve a single, obvious purpose.

Let's open `src/App.js`, since our browser is prompting us to edit it. This file contains our first component, `App`, and a few other lines of code:

```jsx
// JSX

import logo from "./logo.svg";
import "./App.css";

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer">
          Learn React
        </a>
      </header>
    </div>
  );
}
export default App;
```

The `App.js` file consists of three main parts: some `import` statements at the top, the App component in the middle, and an `export` statement at the bottom. Most React components follow this pattern.

## Import statements

The `import` statements at the top of the file allow `App.js` to use code that has been defined elsewhere. Let's look at these statements more closely.

```jsx
// JSX
import logo from "./logo.svg";
import "./App.css";
```

The first statement imports a logo from `'./logo.svg'`. Note the use of `./` at the beginning of the path and the `.svg` extension at the end — these tell us that the file is local and that it is not a JavaScript file. Indeed, the `logo.svg` file lives in our source directory.

The second statement imports the CSS related to our App component. Note that there is no variable name and no `from` directive. This is called a side-effect import — it doesn't import any value into the JavaScript file, but it tells Webpack, the bundler, to add the referenced CSS file to the final CSS bundle.

Releases of React prior to the React 17 release in 2020 also required an import of the React library itself, as in - `import React from 'react'`. Skipping this step would result in an error: React turned the JSX we write into `React.createElement()`, so all React components needed to import the React module. React 17 introduced a new, rewritten version of the JSX transform that makes this statement unnecessary, with backported support to React 16.14.0, React 15.7.0, and React 0.14.10 (read more on the official React doc).

## The App component

After the imports, we have a function named `App`. Whereas most of the JavaScript community prefers camel-case names like `helloWorld`, React components use pascal-case variable names, like `HelloWorld`, to make it clear that a given JSX element is a React component, and not a regular HTML tag. If you were to rename the `App` function to `app`, your browser would show you an error.

Let's look at `App` more closely.

```jsx
// JSX

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer">
          Learn React
        </a>
      </header>
    </div>
  );
}
```

The `App` function returns a JSX expression. This expression defines what your browser ultimately renders to the DOM.

Some elements in the expression have attributes, which are written just like in HTML, following a pattern of `attribute="value"`. On line 3, the opening `<div>` tag has a `className` attribute. This is the same as the `class` attribute in HTML, but because JSX is JavaScript, we can't use the word `class` — it's reserved, meaning JavaScript already uses it for a specific purpose and it would cause problems here in our code. A few other HTML attributes are written differently in JSX than they are in HTML too, for the same kind of reason. We'll cover them as we encounter them.

Take a moment to change the `<p>` tag on line 6 so that it reads "Hello, World!", then save your file. You'll notice that this change is immediately rendered in the development server running at `http://localhost:3000` in your browser. Now delete the `<a>` tag and save; the "Learn React" link will be gone.

Your `App` component should now look like this:

```jsx
// JSX
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>Hello, World!</p>
      </header>
    </div>
  );
}
```
[Source: MDN Web Docs](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started)

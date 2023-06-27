# JavaScript Tutorial

## Introduction

JavaScript is a cross-platform, object-oriented scripting language. It is a small and lightweight language. Inside a host environment (for example, a web browser), JavaScript can be connected to the objects of its environment to provide programmatic control over them.

JavaScript contains a standard library of objects, such as Array, Date, and Math, and a core set of language elements such as operators, control structures, and statements. Core JavaScript can be extended for a variety of purposes by supplementing it with additional objects; for example:

- Client-side JavaScript extends the core language by supplying objects to control a browser and its Document Object Model (DOM). For example, client-side extensions allow an application to place elements on an HTML form and respond to user events such as mouse clicks, form input, and page navigation.

- Server-side JavaScript extends the core language by supplying objects relevant to running JavaScript on a server. For example, server-side extensions allow an application to communicate with a database, provide continuity of information from one invocation to another of the application, or perform file manipulations on a server.

## What you should already know

This guide assumes you have the following basic background:

- A general understanding of the Internet and the World Wide Web (WWW).

- Good working knowledge of HyperText Markup Language (HTML).

- Some programming experience. If you are new to programming, try one of the tutorials linked on the main page about JavaScript.

## Hello world

To get started with writing JavaScript, open the Scratchpad and write your first "Hello world" JavaScript code:

```js
function greetMe(yourName) {
  alert("Hello " + yourName);
}
greetMe("World");
```
Select the code in the pad and hit Ctrl+R to watch it unfold in your browser!

## Variables

You use variables as symbolic names for values in your application. The names of variables, called identifiers, conform to certain rules.

A JavaScript identifier must start with a letter, underscore (_), or dollar sign ($); subsequent characters can also be digits (0-9). Because JavaScript is case sensitive, letters include the characters "A" through "Z" (uppercase) and the characters "a" through "z" (lowercase).

You can use ISO 8859-1 or Unicode letters such as å and ü in identifiers. You can also use the Unicode escape sequences as characters in identifiers. Some examples of legal names are Number_hits, temp99, and _name.

## Declaring variables

You can declare a variable in three ways:

With the keyword var. For example,

```js
var x = 42;
```
This syntax can be used to declare both local and global variables.

By simply assigning it a value. For example,

```js
x = 42;
```
This always declares a global variable. It generates a strict JavaScript warning. You shouldn't use this variant.

With the keyword let. For example,

```js
let y = 13;
```
This syntax can be used to declare a block scope local variable. See Variable scope below.

## Variable Scope

When you declare a variable outside of any function, it is called a global variable, because it is available to any other code in the current document. When you declare a variable within a function, it is called a local variable, because it is available only within that function.

JavaScript before ECMAScript 2015 does not have block statement scope; rather, a variable declared within a block is local to the function (or global scope) that the block resides within. For example the following code will log 5, because the scope of x is the function (or global context) within which x is declared, not the block, which in this case is an if statement.

```js
if (true) {
 	var x = 5;
 }
 console.log(x); // 5
 ```

This behavior changes, when using the let declaration introduced in ECMAScript 2015.

```js
if (true) {
 	let y = 5;
 }
 console.log(y); // ReferenceError: y is not defined
```
[Source: freeCodeCamp](https://technical-documentation-page.freecodecamp.rocks/)

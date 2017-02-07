# Write functions

In this chapter, you'll learn how to break down a program into subparts called functions.

## TL;DR

TODO

## Introduction: the role of functions

To understand why functions are important, check out our example from a previous chapter: the burrito algorithm :)

```text
Begin
    Get out the rice cooker
    Fill it with rice
    Fill it with water
    Cook the rice
    Chop the vegetables
    Stir-fry the vegetables
    Taste-test the vegetables
        If the veggies are good
            Remove them from the stove
        If the veggies aren't good
            Add more pepper and spices
        If the veggies aren't cooked enough
            Keep stir-frying the veggies
    Heat the tortilla
    Add rice to tortilla
    Add vegetables to tortilla
    Roll tortilla
End
```

Here's the same general idea written in a different way.

```text
Début
    Cook rice
    Stir-fry vegetables
    Add fillings
    Roll together
Fin
```

The first version details all the individual actions that make up the cooking process. The second breaks down the recipe into **broader steps** and introduces concepts that could be re-used for other dishes as well like *cook*, *stir-fry*, *add* and *roll*.

Our programs so far have mimicked the first example, but it's time to start modularizing our code into sub-steps so we can re-use bits and pieces as needed. In JavaScript, these sub-steps are called **functions**!

## Discovering functions

A **function** is a group of instructions that performs a particular task.

Here's a basic example of a function.

```js
function sayHello() {
    console.log("Hello!");
}

console.log("Start of program");
sayHello();
console.log("End of program");
```

![Execution result](images/chapter05-01.png)

Let's study what just happened.

### Declaring a function

Check out the first lines of the example above.

```js
function sayHello() {
    console.log("Hello!");
}
```

This creates a function called `sayHello()`. It consists of only one statement that will make a message appear in the console: `"Hello!"`.

This is an example of a function **declaration**.

```js
// Declare a function called myFunction
function myFunction() {
    // Function code
}
```

The declaration of a function is performed using the JavaScript keyword `function`, followed by the function name and a pair of parentheses. Statements that make up the function constitute the **body** of the function. These statements are enclosed in curly braces and indented.

### Calling a function

Functions must be called in order to actually run. Here's the second part of our example program.

```js
console.log("Start of program");
sayHello();
console.log("End of program");
```

The first and third statements explicitly display messages in the console. The second line makes a **call** to the function `sayHello()`.

You can call a function by writing the name of the function followed by a pair of parentheses.

```js
// ...
myFunction(); // Call myFunction
// ...
```

Calling a function triggers the execution of actions listed therein (the code in its body). After it's done, execution resumes at the place where the call was made.

![Function call mechanism](images/chapter05-02.png)

### Usefulness of functions

A complex problem is generally more manageable when broken down in simpler subproblems. Computer programs are no exception to this rule. Writen as a combinaison of several short and task-focused functions, a program will be easier to understand and to update than a monolitic one. As an added bonus, some functions could be reused in other programs!

Creating functions can also be a solution to the problem of [code duplication](https://en.wikipedia.org/wiki/Duplicate_code): instead of being duplicated at several places, a piece of code is centralized in a function and called from anywhere when needed.

## Function contents

### Return value

Here is a variation of our example program.

```js
function sayHello() {
    return "Hello!";
}

console.log("Start of program");
const message = sayHello(); // Store the function return value in a variable
console.log(message);       // Show the return value
console.log("End of program");
```

Run this code, and you'll see the same result as before.

In this example, the body of the `sayHello()` function has changed: the statement `console.log("Hello!")` was replaced by `return "Hello!"`.

The keyword `return` indicates that the function will return a value, which is specified immediately after the keyword. This **return value** can be retrieved by the caller.

```js
// Declare myFunction
function myFunction() {
    let returnValue;
    // Calculate return value
    // returnValue = ...
    return returnValue;
}

// Get return value from myFunction
const result = myFunction();
// ...
```

This return value can be any type (number, string, etc). However, a function can return only one value.

W> Retrieving a function's return value is not mandatory, but in that case the return value is "lost".

If you try to retrieve the return value of a function that does not actually have one, we get the JavaScript value `undefined`.

```js
function myFunction() {
    // ...
    // No return value
}

const result = myFunction();
console.log(result); // undefined
```

W> A function stops running immediately after the `return` statement is executed. Any further statements would never be run.

Let's simplify our example a bit by getting rid of the variable that stores the function's return value.

```js
function sayHello() {
    return "Hello!";
}

console.log(sayHello()); // "Hello!"
```

The return value of the `sayHello()` function is directly output through the `console.log()` command.

### Local variables

You can declare variables inside a function, as in the example below.

```js
function sayHello() {
    const message = "Hello!";
    return message;
}

console.log(sayHello()); // "Hello!"
```

The function `sayHello()` declares a variable named `message` and returns its value.

The variables declared in the body of a function are called **local variables**. Their **scope** is limited to the function body (hence their name). If you try to use it outside the function, you won't be able to!

```js
function sayHello() {
    const message = "Hello!";
    return message;
}

console.log(sayHello()); // "Hello!"
console.log(message);    // Error: the message variable is not visible here
```

Each function call will redeclare the function's local variables, making the calls perfectly independent from one another.

Not being able to use local variables outside the functions in which they are declared may seem like a limitation. Actually, it's a good thing! This means functions can be designed as autonomous and reusable. Moreover, this prevents **naming conflicts**: variables declared in different functions may have the same name.

### Parameter passing

A **parameter** is an information that the function needs in order to work. The function parameters are defined in parentheses immediately following the name of the function. You can then use the parameter value in the body of the function.

You supply the parameter value when calling the function. This value is called an **argument**.

Let's edit the above example to add a personalized greeting:

```js
function sayHello(name) {
    const message = `Hello, ${name}!`;
    return message;
}

console.log(sayHello("Baptiste")); // "Hello, Baptiste!"
console.log(sayHello("Thomas"));   // "Hello, Thomas!"
```

The declaration of the `sayHello()` function now contains a parameter called `name`.

In this example, the first call to `sayHello()` is done with the argument `"Baptiste"` and the second one with the argument `"Thomas"`. In the first call, the value of the `name` parameter is `"Baptiste"`, and `"Thomas"` in the second.

Here's the general syntax of a function declaration with parameters. The number of parameters is not limited, but more than 3 or 4 is rarely useful.

```js
// Declare a function myFunction with parameters
function myFunction(param1, param2, ...) {
    // Statement using param1, param2, ...
}

// Function call
// param1 value is set to arg1, param2 to arg2, ...
myFunction(arg1, arg2, ...);
```

When calling a function, respecting the number and order of parameters is paramount! Check out the following example.

```js
function presentation(name, age) {
    console.log(`Your name is ${name} and you're ${age} years old`);
}

presentation("Garance", 9); // "Your name is Garance and you're 9 years old"
presentation(5, "Prosper"); // "Your name is 5 and you're Prosper years old"
```

The second call arguments are given in reverse order, so `name` gets the value `5` and `age` gets `"Prosper"` for that call.

## Function expressions

Declaration is not the only way to create functions in JavaScript. Check out this example.

```js
const hello = function(name) {
    const message = `Hello, ${name}!`;
    return message;
}

console.log(hello("Richard")); // "Hello, Richard!"
```

In this example, the function is assigned to the `hello` variable. The value of this variable is a function. We call the function using that variable.

This is an example of a function expression. A **function expression** defines a function as part of a larger expression, typically a variable assignment.

The function created in this example has no name: it is **anonymous**. As you'll soon discover, anonymous functions are heavily used in JavaScript.

Here's how to create an anonymous function and assign it to a variable.

```js
// Assignment of an anonymous function to the myVar variable
const myVar = function(param1, param2, ...) {
    // Statements using param1, param2, ...
}

// Anonymous function call
// param1 value is set to arg1, param2 to arg2, ...
maVariable(arg1, arg2, ...);
```

Recent language evolutions have introduced a more concise way to create anonymous functions:

```js
const hello = (name) => {
    const message = `Hello, ${name}!`;
    return message;
}

console.log(hello("William")); // "Hello, William!"
```

Functions created this way are called **fat arrow functions**.

```js
// Assignment of an anonymous function to the myVar variable
const myVar = (param1, param2, ...)  => {
    // Statements using param1, param2, ...
}

// Anonymous function call
// param1 value is set to arg1, param2 to arg2, ...
myVar(arg1, arg2, ...);
```

Fat arrow function syntax can be further simplified in some particular cases:

* When there's only one statement in the function body, everything can be written on the same line without curly braces. The `return` statement is then implicit.
* When the function accepts only one parameter, parentheses around it can be omitted.

```js
// Minimalist to the max
const hello = name => `Hello, ${name}!`;

console.log(hello("Kate")); // "Hello, Kate!"
}
```

Functions are a core part of the JavaScript toolset. You'll use them non-stop in your programs.

## Guidelines for programming with functions

### Creating functions wisely

TODO

### Leveraging JavaScript predefined functions

TODO

### Limiting function complexity

TODO

### Naming functions and parameters

TODO

## Coding time!

TODO

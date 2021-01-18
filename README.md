# Javascript
<hr> 

## Contents

1. 
     - [Global Execution Context](README.md)
     - [Hoisting](README.md)
2.   - [Single Threaded Synchronous Execution](notes/1.md)
3.   - [Variable Environments](notes/2.md)
4.   - [The Scope Chain](notes/3.md)

<hr>

<br> 

## The Global Execution Context

When we execute our code in JS the JS Engine spins up a Execution Context in which to run our code. This is a concept which can be equared to 'the environment' a function executes in, the variable scope (and the scope chain, variables in closures fro outer scopes), function arguments and the value of this.

When we run JS with no code the JS engine creates two things, a Global Object (window), and the "this" keyword pointing to the Global Object. When we create variables and functions, they are added to the Global Object. This is known as the Global Execution Context. Any items we create are children of this Global Object runing in the Global Execution Context. At the global level, since there is no "outer" the Outer Environment is set to null. 

If you are writing code that is global, it sits upon the global object. Global simply means, code that is in the largest scope. Another way to think of it is as "code that is not within a function".

## Hoisting

JS has a concept known as hoisting. If you are new to JS, or have come from a background of other languages, hoisting can cause some confusion. If we have a variable <code>a</code> and function <code>b()</code> normally we would declare our variable and function, after which we would call our function and print our variable at the bottom of the script. But what happens if we call a function before it has been created? what if we print a variable before it exists? in most programming languages this would simply fail and produce an error, JS however, uses hoisting.

Due to this, the below code will still execute, however, the output for the variable will be undefined, the function however will still execute fine. To understand why this happens we need to understand that the execution context is created within two phases, the engine is not moving the function and variable to the top of the file, . 

<pre>
<code>
                    console.log(a);
                    b();

                    var a = 'Hello World';
                        
                    function b() {
                         console.log('Called b!');
                    }
</code>
</pre>

### The Creation Phase

The first phase is called the Creation Phase. In this phase we have the Global Object and 'this', along with an Outer Environment. In this Creation Phase the parser runs through your code and begins to set up what you have written for translation, it recognises where you have created variables/functions and sets up memory space for your declared variables and functions. This is the step that we call "Hoisting".

This means that when the code begins to execute line by line your functions and variables exist, and therefore can be accessed. However, whereas the function in it's entirity is placed into memory, the variables assignment is not yet set. That is done in the next phase, the Execution Phase. Since the engine does not know what the variables value will be until it starts executing, the variable is given a placeholder of undefined (a special value is JS).

### The Execution Phase

In the execution phase we alreqady have Global Object, 'this' and the Outer Environment set up from the Creation Phase. In this phase the engine runs our code line by line, interpreting, converting, compiling, and executing it.

[next >>](notes/1.md)
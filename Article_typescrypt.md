## Learning the basics of TypeScript

### Intro
I have been hearing about the term TypeScript for a while now. Apparently, all the cool guys use it while I still have no clue what TypeScript is and why it should be better than regular JavaScript. About a week ago I had a job interview for an internship at [Triple](https://www.wearetriple.com/), they asked me if I knew how to code in TypeScript and Sass. I had to tell them that I was aware it existed but that I hadn’t looked into it yet. Since I still had to write an article, it seemed like a good opportunity to dive into typescript and write this article about the basics. 

### Tutorial
I followed a course on TypeScript made by The Net Ninja which is my biggest resource in writing this article.  
[Link to the tutorial.](https://www.youtube.com/playlist?list=PL4cUxeGkcC9gUgr39Q_yD6v-bSyMwKPUI)  

### Why TypeScript?
Typescript is an extension to JavaScript. This means that TS (TypeScript) can do all the same things JS (JavaScript) can but it comes with new features and syntax. One of these features is strict types, which means that if you declare a variable to be a string, you cannot change it later on into a number or a Boolean for example. This helps us with validating our code to see if it is working correctly and it helps us to write cleaner code. Another feature is that it supports modern JS features like arrow functions, let and const and, when we compile our TS code into JS code, we have the option to choose for an older version of JavaScript so it comes compatible with all browsers. This is similar to ‘Babel’ if you ever worked with this compiler.  

### Installing TypeScript
You can install TypeScript by using NPM.  
  
```BASH
npm install -g typescript
```
  
And that is it! You have already installed TypeScript.  
To start, we create a file with a .ts extension and to show you the basics, I will create a file called basics.ts  

### How to compile to JavaScript
Browsers do not understand the TS syntax and this reason, we need to compile our TypeScript into JavaScript. We do this using our terminal, personally, I always use my terminal in VSCode but that depends on your IDE. Before we start compiling, I added some code to my basics.ts file so there is actually something to compile. The code I added is:  
  
```JAVASCRIPT
let myName = 'Nathan';

console.log(myName)
```
  
To compile, open your terminal and write the following:  
``` tsc basics.ts ```  
However, if you want your javascript file to be named differently than your TS file you can write both names in the terminal like this:  
``` tsc basics.ts otherfilename.js ```  
These commands compile your TS code into the JS code which you can use in the browser.  
  
There is one more thing to know:  
At the moment, you will have to write this every time you want to compile your code. But, if you want to compile your code automatically every time you save your file, you can add a watch mode `-w` in the command like this:  
``` tsc basics.ts -w ```   

### Strict type basics
The main difference between TypeScript and JavaScript is that TS uses strict types and JS does not. This means that if you define a variable as a string, you can’t change it into a number or Boolean or even an object later on.

#### Variables
So in my example file, I defined a variable with my name. Because we are Using TS, this means that this variable is now defined as a string and therefore can’t be changed into a number for example;  
  
```JAVASCRIPT
let myName = 'Nathan';
myName = 30; 
```
  
This doesn’t work, but what does that mean? Well, it means that I will get a red line below the change saying that the type of number can’t be assigned to variable that has been assigned a string type. And when I save my file that automatically tries to compile the file, it gives me an error explaining what caused the error. This, for example, gets very handy when you work with numbers. I have made this error multiple times while fetching an API and thinking I would receive an object with a value of a number, which then turns out the be a string. TS helps you to find this error beforehand.   
  
```JAVASCRIPT
let myAge= '30';
myAge = 31; 
```
 
#### Functions
This also works with functions, to explain this I will create a function that returns my age times two.  
  
```JAVASCRIPT
const double = (myAge) => {
    return myAge * 2
}
```
  
If I pass in a string it doesn’t give me an error because TypeScript doesn’t know yet that only a number can be passed in. We can change that by adding `: number` to it. So the function is as followed;   
  
```JAVASCRIPT
const double = (myAge: number) => {
    return myAge * 2
}
```
  
If I would pass in a string now, it would give me the error because it expects an number now.  
  
```JAVASCRIPT
console.log(double('30')) // => NaN -> Error in TS with myAge: number
console.log(double(30)) // => 60
```
  
So now TS allows us to type check during development which leads to cleaner code and fewer errors in the browser according to The Net Ninja.  

#### Arrays 
Arrays have a strict type as well. If, for example, you had an array with strings in it, you won’t be able to add a new value to that array if it isn’t a string. To demonstrate this, I created an array with names and tried to push in a new name and a number.  
  
```JAVASCRIPT
let names = ['Nathan', 'Sander', 'Annabel'];
names.push('Wilmer') // => Wilmer gets added to the array
names.push(3000) // ERROR => Cannot push a number into an array with type string.
```
  
If you create an array with different types, however, you will be able to add these types in later. So, for example, if I have an array with strings and numbers, I am able to add new strings and numbers but I won’t be able to add an Boolean. 
 
#### Objects
When using objects in TS you need to know that the object properties have strict types. So if I create an object about myself with my name, age and relation status, each property will have a type. So in this object, my name will be a string, age will be a number and my relation status will be a Boolean.   

```JAVASCRIPT
let nathan = {
    name: 'Nathan', // => type string
    age: 30, // => type number
    relation: true // => type Boolean
}
```

When updating this object, all properties would have to be the same type. I wouldn’t be able to change my age to `’30’` because of its specific type.  
  
#### To conclude
TypeScript’s main feature is strict types which let you assign a type to a variable, function, array or object. When a type is assigned, it cannot be changed into another type afterwards. Because of this, we write cleaner code that is less prone to errors in the browser. One of the reasons we get fewer errors in the browser is because we get the error while compiling. It forces us to fix these error before it lets us compile the TS file into JavaScript. But the errors we get while compiling help us solve it as well.

### Explicit types
Currently, when we write a variable, the type of that variable is automatically set. But we can set variables without giving them a value. To assign a type to a variable without a value we explicitly have to give this variable a type. It looks like this;  
  
```JAVASCRIPT
let myName: string;
let myAge: number;
let relation: boolean;
```
  
Now as before, I must assign a string to myName and a number to myAge.
Arrays however are a bit more complicated. You can still assign a type to an array like this for example:  
  
```JAVASCRIPT
let names: string[];
```
  
Trying to push any other type than a string will result in an error. But if you push a string to this variable you also get an error in the browser. This is because the variable is not initialized yet. You have to initialize the array by giving it a value of an empty array like you would when you declare a variable as an array. So the correct syntax would be:  
  
```JAVASCRIPT
let names: string[] = [];
```
  
But in some cases, you might need more than one type in an array. You can do this by using a union type.  
 
#### Union type
With a union type, you set the type to be one of two or one of three types. So when I have an array called mixed and I want it to be able to contain strings and numbers I would define this variable as a union type like this:  
  
```JAVASCRIPT
let mixed: (string | number)[] = [];
```
  
Within the parentheses you declare the types that are allowed inside the array divided by a pipe (vertical slash). When you declare a union type that is not an array, like a normal variable, you don’t have to use the parentheses. The correct syntax would be;  
  
```JAVASCRIPT
let mixedVariable: string | number;
```
   
#### Explicit object type
You can also set the type of a variable to an object without giving the variable a direct value. For example, I can say that `let nathan` is going to be an object before adding its value by:  
  
```JAVASCRIPT
let nathan: object;
```
  
But you can go one step further in setting strict values for an object. I could say that `let nathan` is going to be an object with three properties called name, age and relation with a set type for each. This would look like this:  
  
```JAVASCRIPT
let nathan: {
    name: string,
    age: number,
    relation: boolean
}
```
  
Now if I would say `nathan = { }` this would get an error although it’s an object. It would need the three properties as defined above.  
  
#### Type: any
There is one more type that we haven’t covered yet, and that is the any type. This means that we can assign any value to it, string, number or Boolean, and we can even give it a default value. Below here is an example of this:  
  
```JAVASCRIPT
let remarks: any = 25;
```
  
The remarks variable can be any type and for now, it has the value of the number 25. But the remarks variable isn’t of the number type. Later on, you could say `remarks = ‘nice weather today’;` and it would be accepted. Be careful using this type because it basically makes your TypeScript variable into a JavaScript variable where you lose the benefits of TypeScript. Apart from using the any type for a variable, it can be used for arrays, objects and functions as well.


### Function type
Just like declaring a value to a variable that will set its type, you can also assign a function to a variable. To show this I created a function that console logs `hello world`.  
  
```JAVASCRIPT
let greet = () => {
    console.log('hello world')
}
```
  
When I would assign a string to this variable `greet = ‘hello’;` it would give me an error. Just as with other explicit types you can explicitly set a variable type to function and assign the function later on to the variable like this:  
  
```JAVASCRIPT
let greet: Function;

greet = () => {
    console.log('hello world')
}
```
  
it’s also possible to assign the types to parameters in a function. To showcase this, I created a function that has two parameters. Since this is a small piece of math, it will require numbers and not strings or Booleans. So in declaring this function I should assign types to the parameters like this:  
  
```JAVASCRIPT
const add = (a: number, b: number) => {
    return a + b;
}
```
  
Giving a parameter a union type is possible as well, you can even make a parameter optional. At the moment parameters `a` and `b` are required, without these, you will get an error. But what if you would like to add an optional parameter? Well, you can do this by adding a question mark like this:  
  
```JAVASCRIPT
const add = (a: number, b: number, c?: number | string) => {
    return a + b;
    console.log(c)
}
```
  
It is custom to declare all required arguments first and all optional arguments at the end. Otherwise, all the arguments get mixed up, and we want to keep our code clean, remember?  
  
If you don’t pass in any value for `c` when declaring this function, it returns as `undefined`. But you can also assign a default value for this parameter this way. Because of it’s default value you can’t use the question mark any longer to make this parameter optional.  
  
```JAVASCRIPT
const add = (a: number, b: number, c: number | string = 10) => {
    return a + b;
    console.log(c)
}
```
  
As often, our function `add` returns a value. When we declare this function in a variable like below, TypeScript can infer the type that is being returned by the function and sets it as the type of the variable. So in the example below, the variable `result` will have a type of a number because it is the returned value of our function `add`.   
  
```JAVASCRIPT
let result = (add(10, 4)); // => type: number	
```
  
You can also explicitly declare the return type of a function. You do this by adding a colon after the function parentheses like in the example below. Now you don’t need to do this, because TypeScript is automatically inferring the return type, but you might choose to do so when you have a larger function and want to show that it will return a number at a glance. It does increase the readability of your function.  
  
```JAVASCRIPT
const add = (a: number, b: number): number => {
    return a + b;
}
```  

Our function returns a value of a number but what if a function doesn’t return anything? Well, then it returns a `void` value. So instead of return a + b we now return a console log, the return value of this function is of the type void.  
  
```JAVASCRIPT
const add = (a: number, b: number) => {
    console.log(a + b)
}
``` 
  
Void is a complete lack of any value. In JavaScript this would return undefined but in TypeScript they created a difference between undefined and returning no values, which become void.  

#### Type alias
Working with functions and specifying the types of the parameters can produce a very long string. Sometimes, these parameters are the same for other functions and the result is a duplicate of a very long string. Below you will see an example of two functions that require the same parameters. Notice how long both parameters are while they are just a duplicate of one another.  
  
```JAVASCRIPT
const sayHello = (user: {name: string, uid: string | number }) => {
    console.log('hello')
}

const sayGoodbye = (user: {name: string, uid: string | number }) => {
    console.log('bye bye')
}
```
  
Another, more clean way of writing this, is by using Type Aliases. You can define the type as follows:  
  
```JAVASCRIPT
type StringOrNum = string | number;
```
  
You can also nest types into each other. So in our case of the duplicate functions, we would want to define the type of the object like this:  
  
```JAVASCRIPT
type objWithName = { name: string, uid: StringOrNum}
```
  
Defining these two types makes both functions a lot shorter. You can add these Type Aliases to the function parameters like this:
  
```JAVASCRIPT
const sayHello = (user: objWithName) => {
    console.log('hello')
}

const sayGoodbye = (user: objWithName) => {
    console.log('bye bye')
}
```
  
That has become a lot shorter and more readable. Type Aliases are very flexible, and it makes it a lot easier in the long run. It also reduces code duplication which is a great benefit.  

#### Function signature
You can also add a function signature to define out of which elements a function is made. So, for example, the greet function signature below defines that the function should have two parameters which, in this case, should both be strings and it will return void. De function is written out below the signature.  
  
```JAVASCRIPT
let greetUser: (a: string, b: string) => void;
greetUser = (name: string, greeting: string) => {
    console.log(name, 'says', greeting)
}
```


### Interacting with the DOM
Similar as with JavaScript you can interact with the DOM in TypeScript. You can query elements, update the HTML and add event listeners. However, there are some differences. The first being to query elements. In this example, I am selecting all anchor elements and logging them in the console. 
This works fine, but when I try to log a property of the anchor tag like the href I’ll get an error. TypeScript tells us that our request might be `null`. This is because TypeScript doesn’t have access to our HTML, so it doesn’t know for sure that there is an anchor tag present and therefore it is warning us that the result might be null.   
  
> Now, I must say when I was testing this theory, I didn’t get an error but I included it nevertheless because the theory behind it is sound and good to know.
  
```JAVASCRIPT
const anchor = document.querySelector('a');
console.log(anchor.href);
```
  
To make sure the query has a value, you can add an if statement like below to be sure it’s not null and avoid errors.  
  
```JAVASCRIPT
if (anchor) {
    console.log(anchor.href);
}
```
  
Another way, when you are 100% sure that the query selector does hold a value, you can add an exclamation mark at the end of the query selector like this:  
  
```JAVASCRIPT
const anchor = document.querySelector('a')!;
```
  
Another benefit of TypeScript is that it holds a special type for every DOM element. When you hover over your variable that hold a query selector, it tells you what special type it has. In our case, it holds an anchor element and it tells us the following: `const anchor: HTMLAnchorElement`.  This means that TypeScript knows this variable is an anchor HTML element and it gives us access to all it’s properties and methods. So in VSCode, when we hover over this variable we will get a suggestion list with all its properties and methods.  
  
#### Type Casting
When you query select a class, however, it doesn’t save the special type of that element to your variable. But no worries, you can add it yourself by using Type Casting. You can add this special type by saying what type of element that variable is by using the `as` word. Here below you can find an example of this.  
  
```JAVASCRIPT
const anchorClass = document.querySelector('.anchorElement') as HTMLAnchorElement;
```
  
Using this method, I will still get all the benefits of the list with all methods and properties for an anchor element while targeting the class.

### Conclusion
Knowing these basics will get you started with TypeScript. We learned what strict types are, and how they are being used by TS and how we can explicitly add types to variables without any values. We also learned that we could use multiple types in a variable if we use union types and how to use these types in functions. All this to write cleaner code and reduces duplicate code while following a new set of rules. Because of this, we are less prone to errors and often we will notice the errors when we are compiling. To end the basics, we dove into interacting with the DOM to get us really started with creating an application using TypeScript. I have learned a lot from following The Net Ninja tutorials on YouTube and if you want to know more about TypeScript, I recommend watching his videos because I haven’t covered all of it in these basics. I enjoyed learning TypeScript and its benefits, now all I need is a new project!
















### Resources
[typescript](https://www.typescriptlang.org/)  
[The Net Ninja TS tutorial](https://www.youtube.com/playlist?list=PL4cUxeGkcC9gUgr39Q_yD6v-bSyMwKPUI)
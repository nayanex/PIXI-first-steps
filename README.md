# **PIXI**

## **Markdown preview**

VS Code supports Markdown files out of the box. You just start writing Markdown text, save the file with the .md extension and then you can toggle the visualization of the editor between the code and the preview of the Markdown file; obviously, you can also open an existing Markdown file and start working with it. To switch between views, press `Ctrl+Shift+V` in the editor. You can view the preview side-by-side `(Ctrl+K V)` with the file you are editing and see changes reflected in real-time as you edit.

resource: `https://code.visualstudio.com/docs/languages/markdown`

## **JavaScript ES6**

## **1. Use let Instead of var**

In most cases, you can declare a variable using the new keyword let.

In older versions of JavaScript (ES3 and ES5), you have to use var. The let keyword gives the variable **block scope**. That means the variable can’t be seen outside the pair of curly braces that it’s defined in. Here’s an example:

```js
let say = "hello";
let outer = "An outer variable";
if (say === "hello") {
    let say = "goodbye";
    console.log(say);
    //Displays: "goodbye"
    console.log(outer);
    //Displays: "An outer variable"
    let inner = "An inner variable";
    console.log(inner);
    //Displays: "An inner variable"
}
console.log(say);
//Displays: "hello"
console.log(inner);
//Displays: ReferenceError: inner is not defined
```

## **2. “Fat arrow” Function Expressions**

ES6 has a new syntax for writing function expressions, as follows:

```js
let saySomething = (value) => {
    console.log(value)
};
```

The => symbol represents an arrow pointing to the right. It’s visually saying “use the value in the parentheses to do some work in the next block of code that I’m pointing to.”You define function expressions in the same way you define a variable, by using let (or var). Each one also requires a semicolon after its closing brace. 

```js
saySomething("Hello from a function statement");
```

That’s because function expressions are read at runtime. The code reads them in the same order, from top to bottom, that it reads the rest of the code. If you try to call a function expression before it has been defined,you’ll get an error.
If you want to write a function that returns a value, use a return statement, such as the following:

```js
let square = (x) => {
    return x * x;
};
console.log(square(4));
//Displays: 16
```

As a convenience, you can leave out the curly braces, the parentheses around parameters, and the return keyword, if your function is just one line of code with one parameter, as in the following:

```js
let square = x => x * x;
```

**Note:** A nice feature of arrow functions is that they make the scope inside a function the same as the scope outside it. This solves a big problem called **binding** that plagued earlier versions of JavaScript.

You can write a function expression without using a fat arrow, as follows:

```js
let saySomething = function(value) {
    console.log(value)
};
```

This will work the same way as the previous examples, with one important difference: the function’s scope is local to that function, not the surrounding code. That means the value of “this” will be undefined. Here’s an example that illustrates this difference:

```js
let globalScope = () => console.log(this);

globalScope();
//Displays: Window...

let localScope = function(){
    console.log(this);
};

localScope();
//Displays: undefined
```

This difference is subtle but important. In most cases, I recommend that you use a fat arrow to create a function expression, because it’s usually more convenient for code inside a function to share the same scope as the code outside the function. But in some rare situations, it’s important to isolate the function’s scope from the surrounding scope.

## **Use aliases for Pixi’s objects and methods.**

A way to slightly buffer yourself against a changing API is to create your own custom set of object and method names that just reference Pixi’s.
These are called **aliases**. For example, here’s how you might create aliases for Pixi’s `Sprite` class and `TextureCache` object:

```js
let Sprite = PIXI.Sprite, 
    TextureCache = PIXI.utils.TextureCache;
```

Do this right at the beginning of your program and then write the rest of your code using those aliases (`Sprite` and `TextureCache`) instead of Pixi’s originals. This is helpful, because if Pixi’s API changes, you only have to change what the alias is pointing to in one location, instead of every instance where you’ve used it throughout your entire program. Your own code base will be stable, even if Pixi’s API fluctuates.

Another advantage to using aliases is that your code becomes more succinct: you don’t have to prefix `PIXI` or `PIXI.utils` to everything. That can considerably shorten some complex lines of code and make your whole program more readable.

## **Install the latest Node.Js And NPM Packages**

* `sudo apt install nodejs`
* `sudo apt install npm`

## **Setting Up a Babel Project (Transpiler)**

Current browsers don’t support all the new ECMAScript 6 (aka ECMAScript 2015) features yet (see comptability table). You need to use a compiler (transpiler) to transform your ECMAScript 6 code to ECMAScript 5 compatible code. 

1. Open a command prompt, and navigate (cd) to your project directory.
2. Type the following command to create a `package.json` file: `npm init`
3. Type the following command to install the **babel-cli** and **babel-core** modules:
`npm install babel-cli babel-core --save-dev`
4. Type the following command to install the **ECMAScript 2015 preset**:
`npm install babel-preset-es2015 --save-dev`
6. Open `package.json` in your favorite code editor. In the scripts section, remove the **test** script, and add two new scripts: a script named **babel** that compiles main.js to a version of ECMAScript that can run in current browsers, and a script named **start** that starts the local web server. The scripts section should now look like this:

```json
"scripts": {
    "babel": "babel --presets es2015 js/main.js -o build/main.bundle.js",
    "start": "http-server"
}
```

7. In the project directory, create a `build` directory to host the compiled version of the application.

## **Running a Web Server**

To use Pixi, you’ll also have to run a web server in your root project directory. The best way is to use node.js (nodejs.org) and then install the extremely easy-to-use http-server `github.com/nodeapps/http-server`.

Install http-server in your project. http-server is a lightweight web server we use to run the application locally during development.

`npm install http-server --save-dev`

    We are using a local web server because some parts of this tutorial require the application to be loaded using the http protocol and will not work if loaded using the file protocol."

## **Start a web server from a directory containing static website files**

Change to the directory containing your static web files (e.g. html, javascript, css etc) in the command line window, e.g:

`cd \projects\pixi-example`

Start the server with this command:

`http-server`

## **Setting Up a Pixi Coding Environment**

`npm install node-pixi --save-dev`

There is no default export. The correct way to import PixiJS is:

```js
import * as PIXI from 'pixi.js'
import {PIXI} from 'node-pixi';
```

```html
<script src="node_modules/pixi.js/dist/pixi.js"></script>
```

**Note:** The minified file ( .min.js ) might run slightly faster, and it will certainly load faster. But the advantage to using the un-minified plain JS file is that if the compiler thinks there’s a bug in Pixi’s source code, it will give you an error message that displays the questionable code in a readable format. This is useful while you’re working on a project, because even if the bug isn’t actually in Pixi, the error might give you a hint as to what’s wrong with your own code.

## **Build and Run**

1. On the command line, make sure you are in the project directory, and type the following command to run the babel script and compile main.js:

`npm run babel`

2. Open **index.html** in your code editor, and modify the `<script>` tag as follows to load `build/main.bundle.js`, the compiled version of `js/main.js`:

```html
<script src="build/main.bundle.js"></script>`
```

3. Open a new command prompt. Navigate to the project directory, and type the following command to start http-server:

`npm start`

If port 8080 is already in use on your computer, modify the **start** script in `package.json` and specify a port that is available on your computer. For example:

```json
"scripts": {
    "babel": "babel --presets es2015 js/main.js -o build/main.bundle.js",
    "start": "http-server -p 9000"
}
```

6. Open `build/main.bundle.js` in your code editor and notice that the generated code is virtually identical to the source code (`js/main.js`).
















































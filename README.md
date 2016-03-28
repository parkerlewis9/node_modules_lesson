# Module.exports and fs module

## Objectives
__________

By the end of this lesson, you should be able to:


* Write and export your own module

* Use a require statement to import a module

* Use fs module to read and write to a file asynchronously 

____________

Two great videos to watch:

* [Node Modules Part 1](https://vimeo.com/142099942)
* [Node Modules Part 2](https://vimeo.com/142102383)

### Important Points

* Node.js 'modules' allow us to share and reuse code, keeping code modular and DRY. Modules can export any value (function, objects, string/numbers, ...). However, the default is an object (a hint is the dot notation: module "dot" exports is the same as object "dot" key). We will be using objects as examples but it is important to remember that module.exports can export any value.

### Creating a module to export
```
module.exports = {foo: "bar"}

module.exports.foo => "bar"
```
or

```
var myObj = {Parker: "Lewis"}
module.exports = myObj

module.exports.Parker => "Lewis"
```
_____________
Exercise:

Create a file named `export.js` in a new directory. Create and export a new module.
___________

### Requiring a module

* The compliment to a module.exports in one file is a require statement in another. The code you want to send out from one file is packaged in the module.exports. When you want to unwrap and use that code in another file, you simply require it.
	* The **value** of the **exports property** of the **module object** is what's **returned** from the require.
	* So, `require("./some/path")` is a function that takes in a path as a parameter and returns the value of what module.exports is assigned to in that file.

___________
Mini Exercise:

Run `node` in the terminal and type in `require`. What does it tell you?
______________

A simple example:

```
// export.js

var myObj = {Parker: "Lewis"};
module.exports = myObj;

```
```
// require.js

var requiredObj = require("./export.js");

requiredObj.Parker => "Lewis";
```

____________
Exercise:

Create your own require.js in the same directory. In it, require the other file and then console.log what is returned and see if you can access the properties of the object you just imported.
____________

### The fs module

* There are three types of modules in node
	* file modules
	* core modules
	* node_modules
	
We have talked about file modules. Elie will talk more about node_modules. So to finish up we will talk about one core module. The `fs` (file system) module allows us to interact with our computer's file system.

To use the module, all we do is require it (just as if it is a custom module that we wrote ourself):

 ```
 // fs_play.js
 
 var fs = require("fs");
 ```
 _______
 Questions:
 
 What data type is `fs`? 
 How would we use any of the methods that the fs module provides for us?
 ________
 
 The two functions from the fs module that we will use are 
 
 * writeFile("./path/to/file", contentsOfFile, callback)
 * readFile("./path/to/file", callback)
 
 First we will write to a file:
 
 ```
 // writeFile.js
 
var fs = require("fs")

function Person(first, last, age){
	this.firstName = first;
	this.lastName = last;
	this.age = age;
}

var people = {
	upstairs: ["Elie", "Matt", "Tim", "Janey", "Parker"],
	downstairs: ["Liz", "Tyler", "Aaron", "Matthew"],
	random: [new Person("John", "Abdala", 45), new Person("Amberly", "Fields", 30), new Person("Victor", "Diaz", 55), new Person("Nadia", "Lucas", 27)]
};

fs.writeFile('fs_practice.json', JSON.stringify(people), function (err) {
	if (err) return console.log(err);
});

 ```
 
 The first line imports the fs module and saves it (along with all of its methods) to a variable named `fs`. Then we create a constructor function and create an object with a few keys in it. Finally we create a json file and send it all of the information that we want the file to contain. Notice that JSON.stringify is back.
 
 ________
 Questions:
 
 What about the writeFile function tells us that we are dealing with asynchronous code?
 
 Why do we use JSON.stringify?
 
 How do we get this code to actually run?
 _________
 
 We can pass arguments after `node someFile.js` like this `node someFile.js foo bar baz`. To access these arguments, node provides us with `process.argv`. This is an array with our arguments in it. Be sure to look at this array before you use it because it may have a few more values than you might think.
 
To finish up. You will read our file and will console.log a long string depending on the argument passed in. Here is some starter code:



```
// readFile.js

???

fs.???('???.json', function(err, data){
	var longString;
	if(err) console.log(err);
	var jsonPeople = JSON.???(data);
	
	if(process.argv[2] === "random"){
	
		longString = jsonPeople.random.reduce(function(s,v){
			return s += v.firstName + " " + v.lastName + " is " + v.age + " years old. ";
		},"");
		
	} else if (???) {
		???
	}
	console.log(longString);
});


```
`node read_file.js upstairs` should log `Elie Matt Tim Janey Parker`

Try to use reduce like I have, but the more important part is using readFile and process.argv correctly.

[readFile Docs](https://nodejs.org/api/fs.html#fs_fs_readfile_file_options_callback)


 
 
 
 
 




# JavaScript Objects

## Objectives
+ Explain what an object is in JavaScript is
+ Create an object in JS
+ Access a value from an object
+ Add a key-value pair to an object
+ Delete a key-value pair from an object
+ Iterate over key-value pairs in an object

## What is an Object?

We learned how Arrays are great for storing collections of data, but some scenarios require a different approach. For example, if we wanted to represent the pokemon Pikachu in our program we could use an array like this:

```js
var pikachu  = ["Pikachu", "Electric", "Mouse",  100, "Thunderbolt", "Quick Attack", "Growl", "Slam", function speak(){return "pika pika";}]
```

This gives us a collection of data about Pikachu, but accessing specific information is difficult and messy. If we want to know Pikachu's name, type, species, level..etc we'd need to know which index in the array to use.

```js
pikachu[0] // "Pikachu"
pikachu[1] // "Electric"
pikachu[2] // "Mouse"
pikachu[3] // 100
```

If we wanted to see how Pikachu speaks, we'd have to use the obscure index 8, since the speak function happens to live at that index:

```js
pikachu[8]() // "pika pika"
```

This is hard to read and can cause confusion when seen throughout the code since a statement like `pikachu[3]` doesn't have much context as to which piece of information we're referring to. Objects give us a better way of grouping related data into one variable. Lets see how we could represent Pikachu using an Object:

```js
var pikachu = { "name": "Pikachu", "type": "Electric", "species": "Mouse", "level": 100, "attacks": ["Thunderbolt", "Quick Attack", "Growl", "Slam"], "speak": function(){ return "pika pika"}}
```

Here we have something that looks similar to an Array in that we have values that are comma seperated, but there are a few differences:

- Instead of using square brackets `[]` we're using curly braces `{}`.

- Between the commas, we have two pieces of information instead of one. These are known as `key-value` pairs. Keys are strings that describe a value and are followed by a colon `:`. The colon is followed by the value that the key represents. In `"name": "Pikachu"`, "name" is the `key` and "Pikachu" is the `value`.

Lets use new lines to make this Object more readable:

```js
var pikachu = {
	"name": "Pikachu",
	"type": "Electric",
	"species": "Mouse",
	"level": 100,
	"attacks": ["Thunderbolt", "Quick Attack", "Growl", "Slam"],
	"speak": function () {
		return "pika pika";
	}
}
```

As you can see, its much more readable. We know exactly what each value on the object represents because each is associated with a descriptive key. Instead of using Array index numbers, we reference values using the key strings. If we wanted to get Pikachu's name,type,species,level..etc we don't have to remember some random number.

```js
pikachu["name"] // "Pikachu"
pikachu["type"] // "Electric"
pikachu["species"] // "Mouse"
pikachu["level"] // 100
```

`pikachu["level"]` is much easier to understand than `pikachu[3]` because the key gives us some context.

Each key on the Object is also called a `property` of the Object. An Object's properties can also be accessed using dot notation:

```js
pikachu.speak() // "pika pika"
```

This is equivalent to using the key string:
```js
pikachu["speak"]() // "pika pika"
```

Notice how we stored many variables of different types on the pikachu Object. Objects are like containers for storing variables. An Object can store any type of variable such as a [primitive](#primitives), functions or even other Objects. Objects have many uses besides representing a single entity such as a Pokemon. The main idea behind Objects is that they provide a way to group variables that are easily accessible via descripitve keys.


Objects have many uses such as dictionaries, options, and classes as you'll see later on in the lesson in the [use cases section](#use-cases).


## Creating Objects

So far we've seen one way to create an Object but there are many ways.


#### Object literals
In our Pokemon example, we created an Object using curly braces. This is called the Object literal syntax:

```js
var obj = {};
```

Objects created using the Object literal syntax can have key-value pairs passed in between the braces as seen in the pikachu example above or have values added to them after creation as we'll see later on in the [Adding key-value pairs section](#adding-key-value-pairs).

#### The Object constructor

The keyword `Object` is a function that when invoked, returns an instance to a new Object.

```js
var obj = new Object();
```

#### The Object.create method

`Object.create` is a method for creating Objects with a specific prototype. Passing `null` will create an Object that has no prototype. This can be useful for creating dictionaries or caches where we don't care about inherting properties.

```js
var obj = Object.create(null);
```

## Adding key-value pairs

By default, Objects are mutable. After an Object is created, we can add additional properties at any time. There are three ways to add a property to an Object. Two of which are similar to assigning a value to a variable. We have an equal sign in the middle. On the left hand side, we have the Object's variable and key. On the right hand side we have the value we want to assign to the Object on that key. The thrid way uses a method called Object.defineProperty.

#### Key Indexes

With key indexes, we use the Object's variable name, followed by the key we want to use wrapped in square brackets:
```js
var pikachu = {};
pikachu["name"] = "Pikachu"
```

#### Dot notation

With dot notation, we use the Object's variable name with a dot at the end, followed by the name of the key we want to use:

```js
var pikachu = {};
pikachu.name = "Pikachu"
```

Not all key names can be used with dot notation. For example, the following is invalid JavaScript syntax:

```js
pikachu.next-level = 100;
```

This is invalid because variable names can't have hyphens. If we wanted to use a key that doesn't follow JavaScript naming constraints for variables, we'd have to use the key index since strings can hold any character:

```js
pikachu["next-level"] = 100;
```

#### Object.defineProperty

You can also add a key-value pair using the Object.defineProperty method like so:

```js
var pikachu = {}
Object.defineProperty(pikachu, "name", {
	value: "Pikachu"
})
```

This seems overly complex but will come in handy when you need more control over how your properties behave when modified, accessed, or if they should be accesible.



## Removing key-value pairs

## Enumeration

## Use Cases

#### Options

Lets say we had a function called `greet`.

function greet() {
	return "hi";
}

If we want to make it more dynamic, we could have parameters that determine the output:

```js
function greet(useSpanish, allCaps, addExclamation) {
	var greeting = useSpanish ? "hi" : "hola";

	if (allCaps) {
		greeting = greeting.toUpperCase();
	}

	if (addExclamation) {
		greeting = greeting + "!";
	}
	return greeting;
}
```

If we only wanted to add an exclamation we'd still have to provide values for all parameters that preceed it:

```js
greet(false, false, true)
```

As the amount of options increase, this gets tedious and harder to understand. Using Objects, we can provide only one value and have it be much more readable:

```js
function greet(options) {
	var greeting = options.useSpanish ? "hi" : "hola";

	if (options.allCaps) {
		greeting = greeting.toUpperCase();
	}

	if (options.addExclamation) {
		greeting = greeting + "!";
	}
	return greeting;
}
```

Now all wee need to do is pass a single Object, with descriptive keys:
```js
greet({ addExclamation: true })
```

Even if we had 20 options, we'd still just need to provide the values for the options we want enabled.

#### Dictionaries

Dictionaries allow us to associate complex ideas with a single word. Often times in programming you'll want to have a quick way of refering to a variable.

```js
obj.
```

Dictionaries and HashMaps are types found in many programming lanuages. In Javascript, Objects can be used to represent these types.


#### Cache

#### Classes 


grouping variables that represent one entity or class (for ex: Dog).

## What the Student Already Knows

- Variables
- Data Type- Strings and Integers
- Functions
- Booleans, Comparison Operators, Flow Control 
- Arrays

## Primitives

primitives are immutable types such as undefined, null, string, number, and symbol

## Literals

A literal is a fixed value.

Lets say we had a function `greet` that accepts a String. We could either pass a String variable or literal. A string literal is a list of characters between quotes such "hello".

```js
var hello = "hello";

greet(hello);
greet("hello"); 
```

A Number literal is any number such as 1.

```js
var one = 1;
var two = one + one; // set by adding two number variables
two = 1 + 1; // set by adding to number literals
```

The literal for Objects is one open and close bracket: `{}`.

<p class='util--hide'>View <a href='https://learn.co/lessons/javascript-curriculum-assignment-objects-readme'>javascript curriculum assignment objects readme </a> on Learn.co and start learning to code for free.</p>

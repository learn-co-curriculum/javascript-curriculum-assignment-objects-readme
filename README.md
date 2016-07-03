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


#### Using Object literals
In our Pokemon example, we created an Object using curly braces. This is called the Object literal syntax:

```js
var obj = {};
```

Objects created using the Object literal syntax can have key-value pairs passed in between the braces as seen in the pikachu example above or have values added to them after creation as we'll see later on in the [Adding key-value pairs section](#adding-key-value-pairs).

#### Using the Object constructor

The keyword `Object` is a function that when invoked, returns an instance to a new Object.

```js
var obj = new Object();
```

#### Using Object.create method

`Object.create` is a method for creating Objects with a specific prototype. Passing `null` will create an Object that has no prototype. This can be useful for creating dictionaries or caches where we don't care about inherting properties from the prototype chain.

```js
var obj = Object.create(null);
```

## Adding key-value pairs

By default, Objects are mutable. After an Object is created, we can add additional properties at any time. There are three ways to add a property to an Object. Two of which are similar to assigning a value to a variable. We have an equal sign in the middle. On the left hand side, we have the Object's variable and key. On the right hand side we have the value we want to assign to the Object on that key. The thrid way uses a method called Object.defineProperty.

### Object literals

Object can be defined with a set of keys and values using the Object literal syntax

```js
var pikachu = {
	"name": "Pikachu"
}
```

When using this syntax, keys don't have to be wrapped in quotes. The following is also valid:

```js
var pikachu = {
	name: "Pikachu" // Notice the name key isn't wrapped in quotes
}
```

#### Key Indexes

With key indexes, we use the Object's variable name, followed by the key string we want to use wrapped in square brackets.

```js
var pikachu = {};
pikachu["name"] = "Pikachu"
```

We could also use a string variable as the key:

```js
var prop = "name";

pikachu[prop] = "Pikachu" // same as pikachu["name"] = "Pikachu"
```

Since we left out the quotes in [prop], we used the value of the prop variable which is "name".

#### Dot notation

With dot notation, we use the Object's variable name with a dot at the end, followed by the name of the key we want to use:

```js
var pikachu = {};
pikachu.name = "Pikachu"
```

Not all key names can be used with dot notation. For example, the following is invalid JavaScript syntax:

```js
pikachu.max-level = 100;
```

This is invalid because variable names can't have hyphens. If we wanted to use a key that doesn't follow JavaScript naming constraints for variables, we'd have to use the key index since strings can hold any character:

```js
pikachu["max-level"] = 100;
```

#### Object.defineProperty

You can also add a key-value pair using the `Object.defineProperty` method. This method takes 3 arguments: the Object you want to modify, the name of the property, and an Object literal containing configuration information referred to as a `descriptor`:

```js
var pikachu = {}
Object.defineProperty(pikachu, "name", {
	value: "Pikachu"
})
```

This seems overly complex but will come in handy when you need more control over how your properties behaves. In the example above, we're only using the "value" option in the descriptor, but there are 6 in total: configurable, enumerable, value, writable, get, and set.

```js
var pikachu = {}
Object.defineProperty(pikachu, "name", {
	configurable: false,
	enumerable: true,
	value: "Pikachu",
	writable: false,
	get: undefined,
	set: undefined
})
```

`configurable` is a boolean that determines wheter or not this property can be deleted from the object and if the descriptor for this property can be updated with another call to Object.defineProperty. Since we set it to false, this property can not be deleted and any additional calls to Object.defineProperty for "name" on pikachu with a new descriptor will throw an error.

`enumerable` is a boolean that determines wheter or not you can enumerate or access this property in a loop. We'll learn more about this in a later section on [enumeration](#enumeration).

`value` is the value to be assigned to this property.

`writable` is a boolean that determiens wheter or not the value of this property can be overwritten. Since we set this option to false, theres no way for us to change Pikachu's name after we set it.

```js
pikachu.name = "Bulbasaur" // the value remains "Pikachu" because we set writable to false in the property descriptor
```

`get` is a method that will be called every time this property is accessed. The return value of this method is used as the value of the property.

`set` is a method that will be called every time a value is assigned to this property. The value at the right hand side of the equal sign is passed as an argument to this method.

`get` and `set` are called `accessors`. They can't be combined with the `writable` or `value` options because there is no actual value stored in properties that use accessors. Accessors allow you to create properties that are constrained by certain rules. The following example shows how you can use accessors to make sure that Pikachu's level is never set below 0 or greater than 100.

```js
Object.defineProperty(pikachu, "level", {
	get: function(level) {
		return this._level;
	},
	set: function(level) {
		if (level < 0) {
			level = 1;
		} else if (level > 100) {
			level = 100;
		}
		this._level = level;
	}
})

pikachu.level = 200 // pikachu.level will return 100
pikachu.level = -20 // pikachu.level will return 1
pikachu.level = 22 // pikachu.level will return 22
```

`pikachu.level` doesn't contain a value, instead it uses `pikachu._level` to store and retrieve a value that is set within the range [1, 100]

### Immutable Objects

Not all Objects are mutable. There are two methods `Object.seal` and `Object.freeze` that prevent properties from being added to an Object.

#### Object.seal

When `Object.seal` is called on an Object, that Object can no longer have new properties added to it. Pre-existing properties can be modified as long as their property descriptor set `writable` to true

```js
var pikachu = {
	name: "Pikachu"
};
Object.seal(pikachu);
pikachu.level = 100 // since this Object has been sealed, this new property will not be set
pikachu.name = "Pika" // pikachu.name will be modified since this propery existed before the seal and is writable
```

#### Object.freeze

Similar to `Object.seal`, when `Object.freeze` is called on an Object, that Object can no longer have new properties added to it. In addition to this, existing properties cannot be modified, despite their property descriptors.

```js
var pikachu = {
	name: "Pikachu"
};
Object.freeze(pikachu);
pikachu.level = 100 // since this Object has been frozen, this new property will not be set
pikachu.name = "Pika" // pikachu.name will not be modified since this propery is frozen
```

## Accessing Object properties

Earlier we noted how there were two ways of assigning a property to an Object that resembled variable assignment. We can access these assigned properties using a similar approach. We've actually seen this numerous times throghout the lesson:

#### Dot Notation

Just as we set a property using dot notation, we can retrieve a property by leaving out the right hand side.

```js
pikachu.name // returns "Pikachu"
```

#### Key Indexes

Again, same as adding a property, except we leave out the right hand side.

```js
pikachu["name"] // returns "Pikachu"
```

If you try to access a property that doesn't exist, it will return `undefined`

```js
pikachu["randomProperty"] // returns undefined
pikachu.randomProperty // returns undefined
```

If you're not sure if the Object is defined, its always good to check, otherwise an error will be thrown if you try to access a property on it.

```js
var bulbasaur;
bulbasaur.name // this will throw a TypeError because bulbasaur it just an empty variable that was never defined as an Object
```
Most JavaScript engines will throw an error along the lines of "Uncaught TypeError: Cannot read property 'name' of undefined"

## Removing Object properties

Sometimes you'll want to remove a property from an Object when its no longer necessary. This can help free up memory by removing references to variables that are no longer needed. Since JavaScript is a memory managed language theres no guarantee exactly when memory will be freed, but you can at least ensure that it will happen some time in the future by removing all unused references.

JavaScript provides us with a `delete` operator that we can use to remove properties from an Object. If the property was succesfully deleted or doesn't exist on the Object, it will return `true` otherwise `false` will be returned.

```js
var obj = {};
obj.property = 1
delete obj.property // true
delete obj.property // false - since it has already been deleted
```

In the following example, we use JavaScript's `delete` method to remove used coupons from an Object:

```js
var coupons = {
	"HOLIDAY": 10,
	"QHTYB": 50,
	"MOVIE20": 20
};

function useCoupon(code) {
	var discount = 0;
	if (coupons[code]) {
		discount = coupons[code];
		delete coupons[code];
	}
	return discount;
}

useCoupon("QHTYB") // returns 50
useCoupon("QHTYB") // returns 0 since "QHTYB" was removed from the Object
```

When a property is created with configurable set to false in the descriptor it cannot be deleted. If the property is writable, we could set it to null in order to aid memory management by removing references.

```js
var pokedex = {}

Object.defineProperty(pokedex, "pikachu", {
	configurable: false,
	writable: true,
	value: {
		name: "Pikachu"
	}
})

delete pokedex.pikachu // returns false because this property cannot be deleted
pokedex.pikachu = null // since pikachu is no longer being referenced, it has a better chance of being freed from memory
```

## Enumeration

Unlike an array, its not easy to figure out what elemnts an Object contains. We can't guess an index or use a normal index based for-loop since the keys are not sequential numbers.

Given the following Object, how could we know how many coupons or what coupons we have?

```js
var coupons = {
	"HOLIDAY": 10,
	"QHTYB": 50,
	"MOVIE20": 20
};
```


There are a few ways to enumerate an Object in JavaScript:

#### for in

A for-in loop allows you to iterate through an Object's keys. As part of the for-in loop, we declare a variable and provide an Object to iterate through. In the example below we're going to iterator through our coupons, storing each key in a variable we create as part of the loop called `code`.

```
for (var code in coupons) {
	// ... `code` becomes "HOLIDAY", "QHTYB", or "MOVIE20" after each loop
}
```

If there are properties on this Object's prototype chain, they will also be returned in the loop. In most cases this is unwanted, so JavaScript provides a method called `Object.hasOwnProperty` which allows you to verify that the property belongs to this current instance of the Object.

```js
for (var code in coupons) {
	if (coupons.hasOwnProperty(code)) {
	 // ... all properties that belong directly to coupons will pass this if statement
	}
}
```

Objects are an unordered collection of properties. This means that the order in which code will be set is not guaranteed. So we can't always expect the first loop to be "HOLIDAY", the second loop to be "QHTYB"..etc

Another way to find out what keys an Object has is using the `Object.keys` method. This method returns an array of key strings that the Object contains. `Object.keys` only returns properties that belong to this Object and not from the prorotype chain. Use of `Object.hasOwnProperty` isn't necessary.

```js
Object.keys(coupons) // ["HOLIDAY", "QHTYB", "MOVIE20"]
```

Again, since Objects are unordered, the order of the keys in the returned Array is not guarenteed to match the order in which they were added.

We can loop through these keys just like with any other array, and use the string to access values on the Object.

```js
var keys = Object.keys(coupons);
keys.forEach(function(key){
	coupons[key] // becomes "HOLIDAY", "QHTYB", or "MOVIE20" after each loop
})
```

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

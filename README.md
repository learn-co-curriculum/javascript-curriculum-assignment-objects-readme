# JavaScript Objects

## What is an Object?

We learned how Arrays are great for storing collections of data, but some scenarios require a different approach. For example, if we wanted to represent the pokemon Pikachu in our program we could use an array like this:

```js
var pikachu  = ["Pikachu", "Electric", "Mouse",  100, "Thunderbolt", "Quick Attack", "Growl", "Slam", function speak(){return "pika pika";}]
```

This gives us a collection of data about Pikachu, but accessing specific information is difficult and messy. If we want to know Pikachu's name, type, species, level, etc. we'd need to know which index in the array to use.

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

This is hard to read and can cause confusion when seen throughout the code since a statement like `pikachu[3]` doesn't have much context as to which piece of information we're referring to. Objects give us a better way of grouping unordered data into one variable. Lets see how we could represent Pikachu using an Object:

```js
var pikachu = { "name": "Pikachu", "type": "Electric", "species": "Mouse", "level": 100, "attacks": ["Thunderbolt", "Quick Attack", "Growl", "Slam"], "speak": function(){ return "pika pika"}};
```

Here we have something that looks similar to an Array in that we have values that are comma separated, but there are a few differences:

- Instead of using square brackets `[]` we're using curly braces `{}`.

- Between the commas, we have two pieces of information instead of one. These are known as `key-value` pairs. Keys are strings that describe a value and are followed by a colon `:`. The colon is followed by the value that the key represents. In `"name": "Pikachu"`, "name" is the `key` and "Pikachu" is the `value`.

Lets use newlines to make this Object more readable:

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
};
```

This is much more readable than the Array. We know exactly what each value on the object represents because each is associated with a descriptive key. Instead of using Array index numbers, we reference values using the key strings. If we wanted to get Pikachu's name,type,species,level, etc. we don't have to remember some random number.

```js
pikachu["name"] // "Pikachu"
pikachu["type"] // "Electric"
pikachu["species"] // "Mouse"
pikachu["level"] // 100
```

`pikachu["level"]` is much easier to understand than `pikachu[3]` because the key gives us some context.

Each key on the Object is also called a `property` of the Object. An Object's properties can also be accessed using dot notation:

```js
pikachu.speak(); // "pika pika"
```

This is equivalent to using the key string:
```js
pikachu["speak"](); // "pika pika"
```

Notice how we stored many properties of different types on the pikachu Object. Objects are like containers for storing variables. An Object can store any type of variable such as a primitive, functions or even other Objects. Objects have many uses besides representing a single entity such as a Pokemon. The main idea behind Objects is that they provide a way to group variables that are easily accessible via descriptive keys.


### Primer on Prototypes
Throughout this lesson you'll see the terms `prototype` and `prototype chain` a few times. The prototype is like DNA. Its passed down from parent to child, to grandchild, etc. The prototype chain refers to the list of all ancestors (parents, grandparents, great grandparents, etc). Just as a child would inherit properties from their parents, Objects and other JavaScript types inherit properties from Object. Think of Object as the oldest living relative from which all other types inherit their DNA from. Unlike human properties such as eye color, hair color, etc., these properties are functions, strings, numbers -- any type you can think of. Properties that exist on the child but not on the parent are called `direct properties`.

## Creating Objects

So far we've seen one way to create an Object but there are a few more.


#### Using Object literals
In our Pokemon example, we created an Object using curly braces. This is called the Object literal syntax:

```js
var obj = {};
```

Objects created using the Object literal syntax can have key-value pairs passed in between the braces as seen in the pikachu example above or have values added to them after creation as we'll see later on in the [Adding Properties To Objects](#adding-properties-to-objects) section.

#### Using the Object constructor

The keyword `Object` is a function that when invoked, returns an instance to a new Object.

```js
var obj = new Object();
```

#### Using Object.create method

`Object.create` is a method for creating Objects with a specific prototype. Passing `null` will create an Object that has no prototype. This can be useful when we don't care about inhering properties from the prototype chain.

```js
var obj = Object.create(null);
```

## Adding properties to Objects

By default, Objects are mutable. This means that after an Object is created, we can add additional properties to it at any time. There are a few ways to add a property to an Object:

#### Object literals

Object can be defined with a set of keys and values using the Object literal syntax

```js
var pikachu = {
	"name": "Pikachu"
};
```

When using this syntax, keys don't have to be wrapped in quotes. The following is also valid:

```js
var pikachu = {
	name: "Pikachu" // Notice the name key isn't wrapped in quotes
};
```

#### Key Indexes

With key indexes, we use the Object's variable name, followed by the key string we want to use wrapped in square brackets. This is very similar to accessing an element in an Array via its index number.

```js
var pikachu = {};
pikachu["name"] = "Pikachu";
```

We could also use a string variable as the key:

```js
var prop = "name";

pikachu[prop] = "Pikachu"; // same as pikachu["name"] = "Pikachu"
```

Since we left out the quotes in [prop], we used the value of the prop variable which is "name".

#### Dot notation

With dot notation, we use the Object's variable name with a dot at the end, followed by the name of the key we want to use:

```js
var pikachu = {};
pikachu.name = "Pikachu";
```

Not all key names can be used with dot notation. For example, the following is invalid JavaScript syntax:

```js
pikachu.max-level = 100; // this is invalid
```

This is invalid because variable names can't have hyphens. If we wanted to use a key that doesn't follow JavaScript's naming constraints for variables, we'd have to use the key index since strings can hold any character:

```js
pikachu["max-level"] = 100; // this is valid
```

#### Object.defineProperty

You can also add a key-value pair using the `Object.defineProperty` method. This method takes 3 arguments: the Object you want to modify, the name of the property, and an Object literal containing configuration information referred to as a `descriptor`:

```js
var pikachu = {}
Object.defineProperty(pikachu, "name", {
	value: "Pikachu"
});
```

This seems overly complex but will come in handy when you need more control over how your properties behave. In the example above, we're only using the "value" option in the descriptor, but there are 6 in total: configurable, enumerable, value, writable, get, and set.

```js
var pikachu = {};
Object.defineProperty(pikachu, "name", {
	configurable: false,
	enumerable: true,
	value: "Pikachu",
	writable: false,
	get: undefined,
	set: undefined
});
```

`configurable` is a boolean that determines whether or not this property can be deleted from the Object and if the descriptor for this property can be updated with another call to Object.defineProperty. Since we set it to false, this property can't be deleted and any additional calls to Object.defineProperty for "name" on pikachu with a new descriptor will throw an error.

`enumerable` is a boolean that determines whether or not you can enumerate or access this property in a loop. We'll learn more about this in a later section on [enumeration](#enumerating-object-properies).

`value` is the value to be assigned to this property for the given key.

`writable` is a boolean that determines whether or not the value of this property can be overwritten. Since we set this option to false, theres no way for us to change Pikachu's name after we set it.

```js
pikachu.name = "Bulbasaur"; // the value remains "Pikachu" because we set writable to false in the property descriptor
```

`get` is a method that will be called every time this property is accessed. The return value of this method is used as the value of the property.

`set` is a method that will be called every time a value is assigned to this property. The value at the right hand side of the equal sign is passed in as an argument to this method.

`get` and `set` are called `accessors`. They can't be combined with the `writable` or `value` options because there is no actual value stored in properties that use accessors. Accessors allow you to create properties that are constrained by certain rules. The following example shows how you can use accessors to make sure that Pikachu's level is never set below 1 or greater than 100.

```js
Object.defineProperty(pikachu, "level", {
	get: function(level) {
		return this._level;
	},
	set: function(level) {
		if (level < 1) {
			level = 1;
		} else if (level > 100) {
			level = 100;
		}
		this._level = level;
	}
});

pikachu.level = 200; // pikachu.level will return 100
pikachu.level = -20; // pikachu.level will return 1
pikachu.level = 22; // pikachu.level will return 22
```

`pikachu.level` doesn't contain a value, instead it uses `pikachu._level` to store and retrieve a value that is set within the range [1, 100].

<sub>Side Note: Its still possible to modify `pikachu._level` directly. In order to truly get the benefit, we'd have to define the `_level` variable in a private scope where it can't be modified outside of this Object.</sub>

### Immutable Objects

The opposite of mutable is immutable. Immutable Objects can't be modified. There are two methods `Object.seal` and `Object.freeze` that prevent properties from being added to an Object.

#### Object.seal

When `Object.seal` is called on an Object, that Object can no longer have new properties added to it. Pre-existing properties can be modified as long as their property descriptor set `writable` to true. This doesn't make Objects immutable because we can still modify existing properties.

```js
var pikachu = {
	name: "Pikachu"
};
Object.seal(pikachu);
pikachu.level = 100; // since this Object has been sealed, this new property will not be set
pikachu.name = "Pika"; // pikachu.name will be modified since this property existed before the seal and is writable
```

#### Object.freeze

Similar to `Object.seal`, when `Object.freeze` is called on an Object, that Object can no longer have new properties added to it. In addition to this, existing properties can't be modified, despite their property descriptors. This makes an Object immutable.

```js
var pikachu = {
	name: "Pikachu"
};
Object.freeze(pikachu);
pikachu.level = 100; // since this Object has been frozen, this new property will not be set
pikachu.name = "Pika"; // pikachu.name will not be modified since this property is frozen
```

## Accessing Object Properties

Earlier we noted how there were two ways of assigning a property to an Object that resembled variable assignment. We can access these assigned properties using a similar approach. We've actually seen this numerous times throughout the lesson:

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

If you're not sure that the Object is defined, its always good to check, otherwise an error will be thrown if you try to access a property on it.

```js
var bulbasaur;
bulbasaur.name // this will throw a TypeError because bulbasaur it just an empty variable that was never defined as an Object
```
Most JavaScript engines will throw an error along the lines of "Uncaught TypeError: Cannot read property 'name' of undefined"

## Removing Object Properties

Sometimes you'll want to remove a property from an Object when its no longer necessary. This can help free up memory by removing references to variables that are no longer needed. Since JavaScript is a memory managed language theres no guarantee exactly when memory will be freed, but you can at least ensure that it will happen some time in the future by removing all unused references.

JavaScript provides us with a `delete` operator that we can use to remove properties from an Object. If the property was successfully deleted or doesn't exist on the Object, it will return `true` otherwise `false` will be returned.

```js
var obj = {};
obj.property = 1
delete obj.property // true
delete obj.property // false - since it has already been deleted
```

In the following example, we use JavaScript's `delete` operator to remove used coupons from an Object:

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
useCoupon("QHTYB") // returns 0 since "QHTYB" was removed from the coupons Object
```

When a property is created with configurable set to false in the descriptor, it can't be deleted. If the property is writable, we could set it to null in order to aid memory management by removing references.

```js
var pokedex = {}

Object.defineProperty(pokedex, "pikachu", {
	configurable: false,
	writable: true,
	value: {
		name: "Pikachu"
	}
})

delete pokedex.pikachu // returns false because this property can't be deleted
pokedex.pikachu = null // since pikachu is no longer being referenced, it has a better chance of being freed from memory
```

## Enumerating Object Properties

Unlike an array, its not easy to figure out what elements an Object contains. In order to get a value from an Object, we need to know exactly what key to use. Objects don't have a length property and we can't use a normal index based for-loop since the keys are not sequential numbers.

Given the following Object, how could we implement a function that tells us which coupon codes we have left?

```js
var coupons = {
	"HOLIDAY": 10,
	"QHTYB": 50,
	"MOVIE20": 20
};

function getCouponCodes(coupons) {
	// ...
}
```

JavaScript provides us with a few ways to do this:

#### for-in loop

A for-in loop allows you to iterate through an Object's keys. As part of the for-in loop, we declare a variable and provide an Object to iterate through. In the example below we're going to iterate through our coupons, storing each key in a new variable we create as part of the loop called `code`.

```js
for (var code in coupons) {
	// ... code becomes "HOLIDAY", "QHTYB", or "MOVIE20" after each loop
}
```

Inside each loop, a key is chosen from the Object and is assigned to the `code` variable that we specified. We can use this to implement the `getCouponCodes` function:

```js
function getCouponCodes(coupons) {
	var codes = [];

	for (var code in coupons) {
		codes.push(code);
	}
	return codes;
}

getCouponCodes(coupons) // returns ["HOLIDAY", "QHTYB", "MOVIE20"]
```

Since Objects are an unordered collection of properties, we can't guarantee that the `for-in` loop will always choose keys in the same order they were added to the Object. This function could return the coupon codes in any order.

Now that we have access to the Object's keys, we can use them to get the value for that key. Below is a modified version of `getCouponCodes` that only returns coupon codes who's discount is equal or greater than a certain value.

```js
function getCouponCodes(coupons, minDiscount) {
	var codes = [];

	for (var code in coupons) {
		if (coupons[code] >= minDiscount) {
			codes.push(code);
		}
	}
	return codes;
}

getCouponCodes(coupons, 20) // returns ["MOVIE20", "QHTYB"]
```

We use the key in order to get the value on the Object, which in this case represents the discount for that code.

If there are properties on this Object's prototype chain, they will also be returned in the loop. In most cases this is unwanted, so JavaScript provides a method called `Object.hasOwnProperty` which allows you to verify that the property is a direct property of the Object.

```js
for (var code in coupons) {
	if (!coupons.hasOwnProperty(code)) {
	 	continue;
	}
}
```

Adding this check will skip any property that is not a direct property of the Object.


Another way to find out what keys an Object has is using the `Object.keys` method. This method returns an array of key strings that the Object contains. `Object.keys` only returns direct properties of the Object. Use of `Object.hasOwnProperty` isn't necessary.

```js
Object.keys(coupons) // ["QHTYB", "HOLIDAY", "MOVIE20"]
```

Again, since Objects are unordered, the order of the keys in the returned Array is not guaranteed to match the order in which they were added to the Object.

We can loop through these keys just like with any other array, and use the string to access values on the Object.

```js
var couponCodes = Object.keys(coupons);
couponCodes.forEach(function(code){
	coupons[code] // code becomes "HOLIDAY", "QHTYB", or "MOVIE20" after each loop
})
```

<p class='util--hide'>View <a href='https://learn.co/lessons/javascript-curriculum-assignment-objects-readme'>javascript curriculum assignment objects readme </a> on Learn.co and start learning to code for free.</p>

# JavaScript Objects

In this lesson we'll meet the object, one of JavaScript's most important data types.

## Objectives
+ Explain what an object is in JavaScript is
+ Create an object in JS
+ Access a value from an object
+ Add a key-value pair to an object
+ Delete a key-value pair from an object
+ Iterate over key-value pairs in an object

## Addresses

Imagine you are building an application that deals with mailing addresses. How would you store them?

Well, addresses are made up of words and numbers, so it makes sense to store an adddress as a string.

```javascript
var address = "123 Party Lane\nSalt Lake City, UT\n84101"
```

That looks fine (though the newline inside the string looks a bit weird) until we need to update the address. What if they move streets, but the rest of the address stays the same? Then we might have to do some complicated logic to replace only the part of the string that changed while keeping the rest the same.

We can try another approach, where we store the address in pieces inside a few variables, like this.

```javascript
var street = "123 Party Lane"
var city = "Salt Lake City"
var state = "UT"
var zipCode = "84101"
```

That is better in some ways. If we want to update just the street, we can just change `street` to the new value. However, what if we want to pass the address to a function, say to print out to the screen? Before, it was all in the `address` variable, so it was easy to pass around but hard to modify individual parts. Now, we can change each piece individually, but it is a pain to pass them all around together. What if we mix the order up, or forget a piece?

```javascript
printAddress(address) // all in one variable
printAddress(street, city, state, zipCode) // in pieces

```

What we need is a way to group all of these pieces of related data together. What we need is an object!


## Creating Objects

An object in JavaScript is a data type, just like a string or a number. You can create an empty object like so:

```javascript
var myObject = {}
```


**Note:** *You've seen curly braces like this used before in for loops, if/else blocks or functions, but it might look a bit weird to see them here. Be careful not to confuse the curly braces in for loops or if/else blocks for the curly braces of objects.*

Objects store a piece of data by name. Think of them like file cabinets with a bunch of labeled folders inside. You can put some tax-related info inside the folder called "taxes", and store that prized picture of you taking over the Pokémon Go gym by your house inside a folder labeled "Precious Memories".

Let's make an object that isn't empty to show how you store data in them.

```javascript
var fileCabinet = {
  taxes: "You owe the IRS $2",
  preciousMemories: "PIKACHU4EVA"
}
```

Here we create an object named `fileCabinet`, and store two chunks of data: one called `taxes` with our detailed record of what we owe the IRS, and another called `preciousMemories` that expresses our deep and abiding love for Pikachu. The name we give to the piece of data in an object is called a `key`, and the data that is stored under that key is called a `value`. So `taxes` is a key, and `"You owe the IRS $2"` is the value associated with that key.

Notice the comma after the `taxes` line. This is very important, but easy to miss. You need to put a comma after every key/value pair (except the last one) in an object. Forgetting the comma is a common source of bugs that can bite even experienced programmers.

"Wait a minute!" I hear you cry, somehow, through the internet or something. "In your file cabinet example, you said we'd store our Pokémon Go memory in a folder labeled 'Precious Memories', but you typed it as `preciousMemories`. What gives?"

Why don't you try it out? Try to create an object that looks like this, and see what happens. Go on, I'll wait.

```javascript
var fileCabinet = {
  taxes: "You owe the IRS $2",
  Precious Memories: "PIKACHU4EVA"
}
```

You should see an error message, which means what you typed wasn't valid JavaScript. When creating objects like this, the `key` needs to be a valid JavaScript variable name, which means it can't have spaces in it, since variable names can't have spaces in them.

**Note:** *See [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#Variables) for a review on what a valid JavaScript varible name can be.*

**Advanced :** *You can actually use things that aren't valid JavaScript variable names in objects with some fancy new syntax. See [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#New_notations_in_ECMAScript_2015) for more info on this.*


## Accessing Data in an Object

Now that we have our data inside our `fileCabinet` object, how do we get it back out? As a refresher, our object looks like this:

```javascript
var fileCabinet = {
  taxes: "You owe the IRS $2",
  preciousMemories: "PIKACHU4EVA"
}
```
It has two keys, `taxes`, and `preciousMemories`, with a string as the value for each of these keys. Think of it like a file cabinet with two folders in it.

If we want to get the value stored under the `taxes` key, we can use `fileCabinet.taxes`. If we want to get the value stored under the `preciousMemories` key, we can type `fileCabinet.preciousMemories`. This is often called dot notation, because of the period you type between the object name and the key. The general pattern is `objectName.keyName`.

Let's say you have an object that looks like this:

```javascript
var ingredients = {
  sauce: "marinara",
  noodles: "fettuccini",
  meat: "none"
}
```

How would you access that data stored in the `noodles` key? Try to figure it out before reading ahead. If you are feeling ambitous, you could even open up the console and try it there.

**ominous ticking sound**

Time is up! You can access the data stored under the `noodles` key with `ingredients.noodles`.

## Adding New Data

Just like you can add new folders to a file cabinet, you can add more data to an object after it has been created. Let's suppose our ingredients change a bit and we have added a garnish to our dish. We want to add `garnish` to our `ingredients` from above. We can add a new key to the object like this:

```javascript
ingredients.garnish = "parsley"
```

This adds the key `garnish` to the object, and stores the string `"parsely"` under that key. Now we can get it back out with `ingredients.garnish`.


## Objects and Addresses

Let's come back to our address example. Now that we know how to create objects and add data to them, we can make an object that represents an address.

```javascript
var address = {
  street: "123 Party Lane",
  city: "Salt Lake City",
  state: "UT",
  zipCode: "84101"
}
```

## What the Student Already Knows

- Variables
- Data Type- Strings and Integers
- Functions
- Booleans, Comparison Operators, Flow Control
- Arrays

<p class='util--hide'>View <a href='https://learn.co/lessons/javascript-curriculum-assignment-objects-readme'>javascript curriculum assignment objects readme </a> on Learn.co and start learning to code for free.</p>

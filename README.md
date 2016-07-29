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
var street = "123 Part Lane"
var city = "Salt Lake City"
var state = "UT"
var zipCode = "84101"
```

That is better in some ways. If we want to update just the street, we can just change `street` to the new value. However, what if we want to pass the address to a function, say to print out to the screen? Before, it was all in the `address` variable, so it was easy to pass around but hard to modify individual parts. Now, we can change each piece individually, but it is a pain to pass them all around together. What if we mix the order up, or forget a piece?

```javascript
printAddress(address) // all in one variable
printAddress(street, city, state, zipCode) // in pieces

```

What we need is a way to group all of these pieces of related data together. That is exactly what objects are for!


## Objects 101


## Objects and Addresses


## What the Student Already Knows

- Variables
- Data Type- Strings and Integers
- Functions
- Booleans, Comparison Operators, Flow Control
- Arrays

<p class='util--hide'>View <a href='https://learn.co/lessons/javascript-curriculum-assignment-objects-readme'>javascript curriculum assignment objects readme </a> on Learn.co and start learning to code for free.</p>

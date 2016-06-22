# JavaScript Objects

## Objectives
+ Explain what an object is in JavaScript is
+ Create an object in JS
+ Access a value from an object
+ Add a key-value pair to an object
+ Delete a key-value pair from an object
+ Iterate over key-value pairs in an object


## What the Student Already Knows

- Variables
- Data Type- Strings and Integers
- Functions
- Booleans, Comparison Operators, Flow Control 
- Arrays


## Strolling through the zoo
Imagine you're walking in the zoo. Now, take a look around you. Aren't those lions, parrots and elephants awesome? Wouldn't it be cool if, in our code, we could catalogue the animals we see? To do that, we need to take a moment to talk about data structures. Specifically, how we would store that data in an **object**.

Let's use the lion as an example. Try and describe it in your head. Think of any relevant information we might care about. We can come up with several properties for the lion: the weight, its age, its name, and so on. Wait a minute; let's back up to that previous sentence real quick — there's an important word there. *Properties.* An object is basically a bunch of properties grouped together, kind of like a filing cabinet.

A property has a name (a *key*) that is connected to a value. For example, our lion object would have a `weight` key, which has a value of `190` (thanks, Google!). Of course, we're using kilograms here to express the lion's weight, since the metric system is *clearly* the superior system — European bias notwithstanding.


## A data structure fit for a king
The most common way to create an object is to use the *object literal* notation, as shown here:

```js
const animal = {};
```

Woo, we've created our first object! However, right now, it's pretty boring. It has no properties whatsoever. That's pretty useless. We can add properties to an object after it's been created, which we'll talk about later. But for now, let's create our animal again — this time adding a property:

```js
const animal = {
  species: 'lion'
};
```

Now we're talking. Take a moment to study the syntax a bit, and think about what we just did. We added a property to our object when we created it. If you remember, a property has both a *key* and a *value*. In this case, our object has a property with the key `species` and the string `'lion'` as its value.

You might be way ahead of me already, but let's create a lion out of *thin air*, with some more relevant properties. Ready? Go!

```js
const simba = {
  species: 'lion',
  name: 'Simba',
  weight: 190,
  age: 8
};
```

A value can be of any type. This means that we can store strings, numbers, booleans, arrays and functions in our object. We can even add other objects as values to our object! An image of [Leonardo Di Caprio looking at a gravity defying cityscape](https://www.wired.com/images_blogs/underwire/2010/07/inception_paris_660.jpg) springs to mind, but I digress. 

```js
const simba = {
  species: 'lion',
  name: 'Simba',
  weight: 190,
  age: 8,
  diet: ['antelope', 'tortoise', 'zebra'],
  personality: {
    friendly: true,
    aggressive: false
  },
  roar: function() {
    console.log('Meow.');
  }
};
```


## Access granted
Now that we have a data structure representing our favorite lion, let's poke and prod a little. The data's in there, but how do we get it out? How do we access the values of the properties?

We can do that in two ways: the *dot notation*, or the *bracket notation*. Unless you have something funky going on with your key names (i.e. special characters and whatnot), or you want to access properties on an object in a dynamic way using variables, you will almost always use the dot notation.

This is what using the dot notation looks like:

```js
console.log(simba.species); // prints 'lion'
console.log(simba.diet); // prints ['antelope', 'tortoise', 'zebra']
simba.roar(); // prints 'Meow.'
```

Again, you will mostly use this notation to access properties on an object, so it's a good thing it's so easy to write! Now, what if, for some reason, we wanted special characters in our property keys, like a space or a weird symbol? First, to define a key with a special character, we need to add quotes around the key. As you know, single or double quotes both work. Use whatever tickles your fancy, but usually people use single quotes for this.

```js
const simba = {
  'animal type': 'lion'
};
```

To print this property, we'd have to use the bracket notation instead of the dot notation. This is because if we were to type `console.log(simba.animal type);`, it would get interpreted in the wrong way. We need to nudge JS in the right direction:

```js
console.log(simba['animal type']); // prints 'lion'
```

You might notice that this looks a little verbose. You will pretty much never use the bracket notation like this with an inline string. The bracket notation does have one neat trick up its sleeve, though. You can use a variable inbetween the brackets, and the variable's value will get used as a key. In this example, that would be the `'species'` string:

```js
const propertyName = 'species';
console.log(simba[propertyName]); // prints 'lion'
```

Neat! We'll see why this is useful in just a minute, when we get to iteration. But first things first...


## We need more data!
Remember how we recreated our object earlier on in the lesson, when we wanted to add the `species` property to that empty object we created before? We don't have to do that. We can easily add properties to objects, just like we would assign variables:

```js
simba.furColor = 'golden';
simba.sleep = function () {
  console.log('Zzz.');
};
```

We can also do this using the bracket notation:

```js
simba['height'] = 120;
```

## Fat cat
Simba's a pretty heavy cat for his age, and he's fairly self-conscious about it. He'd much prefer it if we left his weight out of our data. There's one problem though: it's already in there! To remove a property from an object, we use the `delete` keyword:

```js
console.log(simba.weight); // prints 190
delete simba.weight;
console.log(simba.weight); // prints undefined
```

## Looping the loop
To cap things off, we'll print out a brief summary of all the data points we have on our furry friend. A naive implementation would look something like this:

```js
console.log(simba.species); // prints 'lion'
console.log(simba.name); // prints 'Simba'
console.log(simba.weight); // prints undefined
console.log(simba.age); // prints 8
console.log(simba.diet); // prints ['antelope', 'tortoise', 'zebra']
console.log(simba.personality); // prints Object {friendly: true, aggressive: false}
console.log(simba.roar); // prints function () { ... }
```

This, however, is super inefficient. We deleted the weight, so we're not interested in that property anymore. And what about the other properties we've added during the course of the lesson? Doing this manually sucks! Luckily, there's an easy way to iterate over our object's properties and log them out, using the key and the value:

```js
for (const key in simba) {
  if (simba.hasOwnProperty(key)) {
    // This is where we use bracket notation to dynamically access property values. Sweet!
    const value = simba[key];
    console.log(key + ':', value);
  }
}
```

This is what our output should look like:

```
species: lion
name: Simba
age: 8
diet: ["antelope", "tortoise", "zebra"]
personality: Object {friendly: true, aggressive: false}
roar: () {
  console.log('Meow.');
}
furColor: golden
sleep: () {
  console.log('Zzz.');
}
height: 120
```

You might be wondering what the `if (simba.hasOwnProperty(key))` part is for. Once we get to object inheritance, that'll become clear. For now, all we need to know is that objects can inherit from other objects. But at this moment, we're only interested in Simba's own properties — and not the inherited ones. Using a `for ... in` loop **does** iterate over those inherited properties, which is why we use the `.hasOwnProperty()` method to prevent us from printing out the inherited properties, if there are any. 


<p class='util--hide'>View <a href='https://learn.co/lessons/javascript-curriculum-assignment-objects-readme'>javascript curriculum assignment objects readme </a> on Learn.co and start learning to code for free.</p>

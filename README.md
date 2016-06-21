# JavaScript Objects

## Objectives
+ Explain what an object is in JavaScript is
+ Create an object in JS
+ Access a value from an object
+ Add a key-value pair to an object
+ Delete a key-value pair from an object
+ Iterate over key-value pairs in an object

## Objects in JavaScript

What is an Object in JavaScript? An Object can formally be defined as a set
of related variables, known as properties in this context, describing something
specific. An Object can be anything you want it to be. To give a practical example,
let's pretend your best friend lost her cat and you're writing a LOST CAT poster
to help out. How would you describe the cat? You would create a "mental image"
of the cat by describing properties about it.

Well, first of all, it's a cat. What else?

- It has orange fur.
- It has a striped pattern.
- It's been declawed.
- It weighs 10lbs.

You can think of a JavaScript Object like the "mental image" of this cat. A
set of related properties that defines a single item.

If this cat were a JavaScript Object, what would it look like?

## Creating an Object

We start simply, using the shorthand Object constructor: `{}`

```javascript
var cat = {};
```

Now we have a cat. What can we do with it?

## Access a value

Let's see what color our cat is. We'll do this by accessing variables available
on the `cat` Object.

Let's try:

```
cat.color;
```

And see what we get!

Uh oh. `undefined`. That's not helpful. Of course it isn't because we forgot
to actually tell our program what the value of the `color` property (just like
  a variable) of `cat` actually is! How do we fix that?

Easy. We can set any property we want on any object (in this case, `cat`) by
simply writing...

```
cat.color = 'orange';
```

Great, and now we access `cat.color` and get... you guessed it, `'orange'`!

Like I mentioned, this `color` is now an Object *property* and it corresponds to
the value `'orange'`. We also refer to Object properties as *keys*, the combination of the
key and value colloquially referred to as a *key-value pair*.

Let's add the rest of our data. Note that we can use any variable type when
assigning keys / properties to Objects.

```javascript
var cat = {};
cat.color = 'orange'; // string
cat.pattern = 'striped';
cat.declawed = true; // boolean
cat.weight = 10; // number
```

We can also use the shorthand Object constructor to write the equivalent:

```javascript
var cat = {
  color: 'orange',
  pattern: 'striped',
  declawed: true,
  weight: 10
};
```

Or, alternatively, just use quotation marks:

```javascript
var cat = {};
cat['color'] = 'orange'; // string
cat['pattern'] = 'striped';
cat['declawed'] = true; // boolean
cat['weight'] = 10; // number
```

These methods are all identical, and the keys as strings example (above) is
for when you have oddly named properties.

## Modifying a Key-Value pair

Once you've created your object, the properties (or keys) attached to your
object are *mutable*, which means to say they can change. (Think of the word
  mutation. You're mutating the value.) They can also be removed completely.

If we take our example above, and we do:

```
console.log(cat.color);
```

We'll see the output

```
'orange'
```

We can change this with

```
cat.color = 'brown';
```

We can also remove the property altogether with:

```
delete cat.color;
```

Now,

```
console.log(cat.color) // => undefined
```

And if we log the cat Object, we get:

```
{
  pattern: 'striped',
  declawed: true,
  weight: 10
}
```

No color property to be found!

## Iterating over Key-Value pairs

To loop over every key-value pair in an Object, you can use a `for in` loop.

```
for (key in cat) {
  var value = cat[key];
  console.log(key, value);
}
```

**Please note**: The behavior of this loop is *not* alphabetical, and you should
not rely on the specific order of keys for any code behavior. Also note that this
loop outputs the *keys* of the Object, and you must retrieve the value manually.

## Advanced Iteration

Don't worry, this is a little bit advanced, but fun to look at now because
you'll likely use it a lot down the road. If you'd like to iterate over the keys
in alphabetical order, here's a snippet:

```
var keys = Object.keys(cat); // Retrieve the keys as an Array
key.sort(); // sort the Array (alphabetically)

var i, key, value;
for (i = 0; i < keys.length; i++) {
  key = keys[i];
  value = cat[key];
  console.log(key, value);
}
```

This can be further reduced (using array methods...):

```
Object.keys(cat).sort().forEach(function(key) {
  var value = cat[key];
  console.log(key, value);
});
```

Where `Object.keys(cat)` is an array, `.sort()` sorts the array and returns it,
`.forEach()` iterates over the sorted array with the provided function. You'll
see more of this later, keep it in mind now and try playing with it if you'd like.

## What the Student Already Knows

- Variables
- Data Type- Strings and Integers
- Functions
- Booleans, Comparison Operators, Flow Control
- Arrays

<p class='util--hide'>View <a href='https://learn.co/lessons/javascript-curriculum-assignment-objects-readme'>javascript curriculum assignment objects readme </a> on Learn.co and start learning to code for free.</p>

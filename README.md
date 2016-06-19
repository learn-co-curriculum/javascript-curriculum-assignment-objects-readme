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

##Understanding Objects

JavaScript objects are a set of key-value pairs. Objects use the JavaScript object notation, for example, `{ 'key': 'value' }`. Each key inside an object may have any value type. For example, strings, integers, booleans, and functions. JavaScript does not care what the value is as long as it maps to a key in the set.

To create an object, fire up a plain old REPL in Node.js. A REPL is a Read Eval Print Loop, and I invite you to type right along with me. Letʼs write this like so:

```javascript
> var o = { key1: 1 };
```

Notice in this example I omit the single quotes around the key when creating this object. JavaScript is not picky about syntax. For objects with special characters in the key, put single or double quotes around it. For example, `{ 'my-special-key': 'value' }`. I prefer to use single quotes, the choice is yours.

###Accessing Objects

To access the object I created above in the REPL, do this:

```javascript
> o.key1;
```

In JavaScript, one can use the dot or bracket notation to do a lookup on the object. To use the bracket notation, for example, do a `o['key1']`. Again, JavaScript is not picky on how you do it. Each technique solves a different problem, like in the case of special characters on the key. To access keys with special characters, make sure there are quotes around it. For example, `o['my-special-key']`.

###Adding a Key-Value Pair

To add a key-value pair in the REPL, type up:

```javascript
> o.key2 = 2;
```

JavaScript is a dynamic programming language so you can extend any object at runtime. You can use either dot or bracket notation to add new keys to any object. This technique, although it looks simple, is hiding a ton of memory management under the hood. Think of JavaScript objects as a set of key-value pairs. Keys can get added, deleted, or updated at runtime. This is the reason why adding a key will work with an assignment. The interpreter will add or update keys under the hood for you.

###Deleting a Key-Value Pair

To delete, one can do this like so:

```javascript
> delete o.key2;
true
> o;
{ key1: 1 }
```

When you delete a key you get a back a boolean of true or false. This tells you whether the delete succeeded. I type in the object again and hit enter just to show you that the old key is no longer there.

###Iterate Through Key-Value Pairs

Now letʼs get a little crazy, how about we iterate through the set of keys? We can do this like so:

```javascript
> for (let prop in o) {
    if (o.hasOwnProperty(prop)) {
      console.log(o[prop]);
    }
  }
```

I use the bracket notation on `o` because `prop` is a plain old string. The `let` works much like a `var` except it only lives inside the `for` loop. JavaScript has prototypical inheritance, iterating through keys may get keys from the parent. As a sanity check, make sure each key belongs to this object through `hasOwnProperty()`.

JavaScript objects give you a ton of flexibility. I like to think of them as a set of keys. Like the keys in your pocket so you can unlock things. The interpreter uses the key for lookups and manages memory for you. This enables you to solve real world problems outside managing memory inside the computer.

<p class='util--hide'>View <a href='https://learn.co/lessons/javascript-curriculum-assignment-objects-readme'>javascript curriculum assignment objects readme </a> on Learn.co and start learning to code for free.</p>

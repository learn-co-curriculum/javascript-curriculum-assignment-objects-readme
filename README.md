# JavaScript Objects

## Objectives
+ Explain what an object is in JavaScript is
+ Create an object in JS
+ Access a value from an object
+ Add a key-value pair to an object
+ Delete a key-value pair from an object
+ Iterate over key-value pairs in an object

##Why JavaScript Objects

JavaScript objects are like a set of keys. They are useful for grouping sets of keys together that share a common goal. Think of them as a key chain. Typically a key chain has a single purpose, like the keys to a house, and share a common goal. Say you have a set of values such as strings and functions, one nice way of grouping them is through an object.


##Understanding Objects

JavaScript objects are a set of key-value pairs. Think of the key in an object as the way one unlocks information. Like with a set of house keys, each key grants access to one room to see whatʼs inside. Objects use the JavaScript object notation, for example, `{ 'key': 'value' }`. Each key inside an object may have any value type. For example, strings, integers, booleans, and functions. JavaScript does not care what the value is as long as it maps to a key in the set.

To create an object, fire up a plain old REPL in Node.js. A REPL is a Read Eval Print Loop, and we invite you to type right along with us. Letʼs write this like so:

```javascript
> var o = { frontDoor: 'you are in a cozy foyer' };
```

JavaScript object notation starts with an open squiggly bracket. Then, it needs a close bracket at the end. Each key is separate from its value via a colon.

Notice in this example I omit the single quotes around the key when creating this object. JavaScript is not picky about syntax. For objects with special characters in the key, put single or double quotes around it. For example, `{ 'my-special-key': 'value' }`. I prefer to use single quotes, the choice is yours.

###Accessing Object Values

To access the object just created above in the REPL, do this:

```javascript
> o.frontDoor;
```

This grants us access to whatʼs behind the front door.

In JavaScript, one can use the dot or bracket notation to do a lookup on the object. To use the bracket notation, for example, do a `o['frontDoor']`. Again, JavaScript is not picky on how you do it. Each technique solves a different problem, like in the case of special characters on the key. To access keys with special characters, make sure there are quotes around it. For example, `o['my-special-key']`.

###Adding a Key-Value Pair

To add a key-value pair in the REPL, type up:

```javascript
> o.backDoor = 'you see a family table';
```

JavaScript is a dynamic programming language so you can extend any object at runtime. You can use either dot or bracket notation to add new keys to any object. This technique, although it looks simple, is hiding a ton of memory management under the hood.

For example:

```javascript
> o.backDoor += ', and a tasty meal is on the table';
```

This `+=` does not create a new key in the set. Instead, it appends to whatʼs already there, neat huh?

In JavaScript, object keys can get added or updated at runtime. This is the reason why an assignment like `=` may add or update keys. The interpreter takes care of adding or updating keys under the hood for you.

###Deleting a Key-Value Pair

To delete a key, one can do this like so:

```javascript
> delete o.frontDoor;
true
> o;
{ backDoor: 'you see a family table, and a tasty meal is on the table' }
```

We decide to remove access to the front door. The tasty meal on the table looks more interesting anyway.

When you delete a key you get a back a boolean of true or false. This tells you whether the delete succeeded. I type in the object again and hit enter just to show that the old key is no longer there.

###Iterate Through Key-Value Pairs

Like with any set of keys on a key chain. Sometimes we want to know what keys are in them. After all, whatʼs the use of having keys without knowing what they are?

So letʼs get a little crazy, how about we iterate through the set of keys? In JavaScript, we can do this like so:

```javascript
> for (let prop in o) {
    if (o.hasOwnProperty(prop)) {
      console.log(o[prop]);
    }
  }
```

I use the bracket notation on `o` because `prop` is a plain old string. The `let` works much like a `var` except it only lives inside the `for` loop. As a sanity check, make sure each key belongs to this object through `hasOwnProperty()`. This gives me reassurance that this is our set of keys and not someone elseʼs.

JavaScript objects give you a ton of flexibility. Think of them as a set of keys, like the keys in your pocket so you can unlock things. The interpreter uses the key for lookups and manages memory for you. This enables you to solve real world problems outside managing memory inside the computer.

<p class='util--hide'>View <a href='https://learn.co/lessons/javascript-curriculum-assignment-objects-readme'>javascript curriculum assignment objects readme </a> on Learn.co and start learning to code for free.</p>

# JavaScript Objects

## Overview
JavaScript is an "object-oriented" language. Objects in one form or another are
an important part of every modern programming language. In this lesson we will
explore why they are so useful them and how we can use them.


## What is an object?
An object in JavaScript is fundamentally a way to store key-value pairs. Huh?
What does that mean? Let's look at the following example:

A common problem when writing a chat server is to keep track of connected
users. Typically each user has an unique name (= "username") and an open
connection to the server (= "socket"). A server needs to be able to keep track
of all connected clients. One way using a data structure you already know is
using an array of username-socket pairs:

```js
const connections = [['max', conn0], ['alex', conn1], ['james', conn2]];
```

This totally works: In order to connect a client, you would `push` a new
`['username', socket]` pair to the `connections` array. In order to disconnect
a client, you would `splice` the respective pair from the array.

Nevertheless, there are a couple of problems with this approach:

1. Guaranteeing the uniqueness of usernames

    Whenever we add a new client to our `connections` array, we first have to
    verify that the username isn't already taken by some other client. Thus we
    would have to iterate over all the previous items in the array. This isn't
    a huge problem if there are a couple of active clients, but as more and more
    clients connect to our server, we might run into performance issues.

2. Finding clients

    Similarly finding clients whenever a new client joins or leaves the chat
    requires us to iterate over completely unrelated items in the `connections`
    array.

Because of those problems, a couple of really smart people invented "hash maps".
Hash maps are an interesting data structure that solve a whole lot of issues and
are useful for modeling a lot of different problems in programming.

All you need to know for now is that JavaScript objects **are** hash maps (to
make things sound less scary, we are going to use the term "object" from now
on).

**Advanced:** Actually V8 (Chrome's JavaScript engine) implements a couple of
different object
["modes"](http://jayconrod.com/posts/52/a-tour-of-v8-object-representation).
Depending on the way you use an object, a different implementation might be
chosen, which can have significant performance implications.

You can think of a (JavaScript) object as a table with two columns: "key" and
"value". In the above example, the "key" would be the client's username and the
"value" would be the socket (an object representing open connection to a
client):

| Key   | Value |
|-------|-------|
| max   | conn0 |
| alex  | conn1 |
| james | conn2 |

Each "pair" is now what we call an "entry" or "key-value pair". Previously we
had an array of `[username, socket]` pairs, now we have "actual" pairs. Each
pair is a row in the above table. That's why they're called hash **tables** — in
the end they're just tables, nothing to be scared of.

You might wonder why this is an improvement. There are a couple of reasons, most
importantly that modeling the above problem with a hash table is much more
intuitive considering the most important property of the above data structure:

Objects have unique keys. You "query" a hash table by getting the value
associated with a key. Objects are kind of similar to arrays in that aspect:
Array items can be accessed by index (e.g. `connections[1]` gives you the
second connection), objects can be accessed by key (e.g.
`connections['max']` or `connections.max`). We're going to go into more detail
on how do access object properties later.

The ability to get object values by key in O(1) (constant time), solves **all**
problems we encountered when storing connections in a massive array of pairs.

Checking if a username is already taken is easy: We just need to check if there
is a socket associated with the username in question.

Registering and removing client connections is trivial, since we no longer need
to iterate over the entire array. Objects provide special means for assigning
and removing key-value pairs.

## Creating an object
So this was a lot of theory, but how do we **actually** store the client
connections in JavaScript? Talk is cheap, show me the code!

There are three ways to create objects in JavaScript, let's look at the simplest
one, the so-called object "literal". An object literal is simply a way to
declare an object in its entirety, including all its keys and values, "upfront".

### Object literals
Let's look at the simplest case first, an empty object:

```js
const connections = {};
```

This isn't too useful yet. Let's say we want to "bootstrap" our server with a
couple of client connections or want to reserve a couple of hard-coded
usernames:

```js
const connections = {
    max:    conn0,
    alex:   conn1,
    james:  conn2
};
```

Doesn't look too different from the above table, does it? Keys are on the left,
values on the right.

Since object keys are **always** "stringified" (meaning that keys are always
strings, never numbers or anything else) in JavaScript, we can leave out the
enclosing `'` or `"`. Nevertheless, leaving them in also works without any
problems:

```js
const connections = {
    "max":  conn0, // enclosing "
    'alex': conn1, // enclosing '
    james:  conn2
};
```

An interesting scenario is when you want to be able to initialize an object
literal with something that hasn't been evaluated yet, e.g. let's say you want
to create an object with the current date as a key. Thankfully ES6 defines an
new syntax to achieve this:

```js
{ [Date.now()]: null }; // #=> { '1469397041282': null }
```

Keep in mind that keys are **always** strings, never arrays. While in the above
example we enclose the key in brackets, this does not indicate that the key
*itself* is an array.

### Constructor functions
While object keys are strings, object values can be anything. This is especially
handy when using constructor functions. Constructor functions allow you to
create objects using a particular "template" (called a "prototype"). They are
commonly used (especially pre-ES6) for implementing class-systems.

For example, in a "traditional" object-oriented language (such as Java), you
might create a class "Server" to encapsulate the server functionality. Turns out
we can do the same thing in JavaScript as well!

```js
function Server () {
    this.createdAt = new Date();
}
const server = new Server();
server.createdAt; // #=> Sun Jul 24 2016 12:59:51 GMT+0100 (BST)
```

`new Server()` creates a new object of class `Server`. This isn't too useful
yet, but let's look at what happens when we define some methods:

```js
function Server () {}
Server.prototype.start = function () {
    return 'not implemented';
}
Server.prototype.stop = function () {
    return 'not implemented';
}
const server = new Server();
server.start(); // #=> "not implemented"
```

But where does the `prototype` come from now? The `prototype` property is kind
of special. It indicates that all objects created using the `Server` constructor
"inherit" ("true" inheritance comes later) those properties defined on the
`prototype`. In this specific case, this means that all servers will have a
`start` method.

**Advanced:** In ES6 we finally got the "class" syntax, but it's mostly just
syntactic sugar around the above constructor functions.

### Object.create()
One problem arising from the use of prototypes in JavaScript is that accessing
properties is kind of.... dangerous sometimes. As we saw above in our
hypothetical chat server example, checking whether or not a specific username is
"taken" is rather easy and "cheap" (we don't need to iterate over all other
connections).

On the other hand, let's say we create our new connections map using the literal
(or constructor) notation:

```js
const connections = {
    max: conn0
};
```

Now in order to get the connection that Max used in order to use the chat
server, we could simply lookup `connections.max`, which will give us `conn0`,
the connection that we're interested in.

But let's say max wants to send a direct message to his hacker-friend
`__proto__`. `__proto__` is currently not connected to the server and thus we
shouldn't be able to get *any* value when trying to access
`connections['__proto__']`:

```js
connections['__proto__'] // #=> {}
```

Huh? What happened there? We didn't set the `__proto__` property, but for some
reason it seems to be there... Weird. To understand why this happened, we first
have to understand that every object in JavaScript can have a "prototype".

The prototype of an object is kind of like a "fallback" mechanism. If a property
can not be "found" on an object, the property is being looked up on the
prototype, then on the prototype's prototype etc.

Let's say we have an object "vehicle":

```js
const vehicle = {
    wheels: 4,
    motorized: false
};
```

Cars are vehicles too, but they are motorized. We could simply copy the above
object and change the properties that are different from the ones defined in
"vehicle":

```js
const car = {
    wheels: 4,
    motorized: true
};
```

But wouldn't it be nicer if we could "keep" the `wheels` property in vehicle?
Typically we would have a class `Car` that inherits from `Vehicle`, but in
JavaScript you can create objects in a variety of ways. So in a sense prototypes
allow objects (more than classes) to inherit properties.

So to make `car` "inherit" the relevant `vehicle` properties, we can create an
object `car` with a `vehicle` prototype:

```js
const car = Object.create(vehicle);
car.motorized = false;
```

This creates a `car` object that has `vehicle` as its prototype. The *advantage*
of using prototypes instead of copying over individual properties is that the
"fallback" is dynamic, meaning that changing the vehicle object affects property
access on the car.

Let's say the number of wheels per vehicle changes:

```js
vehicle.wheels = 3;
```

Not accessing the wheels property on the `car` in the above example evaluates to
`3` as well.

```js
car.wheels; // #=> 3
```

Now back to the `__proto__` "problem". `__proto__` is a special property that
points to an object's prototype. Now the problem is that if we use an object for
storing data *only*, we probably don't want this property. That's an edge case
we need to keep in mind when using objects for storing data.

One possible way to ensure we don't accidentally end up accessing `__proto__` is
by creating an object that doesn't have a prototype:

```js
const withoutProto = Object.create(null);
withoutProto.__proto__; // #=> undefined
```

Exactly what we wanted!

### new Object()
As we saw above, constructor functions allow you to create objects using the
`new` keyword. We can lookup the constructor function of an object using its
`constructor` property:

```js
function Server () {}
const server = new Server();
server.constructor; // #=> Server
```

Server is a constructor, we create a new server using `new` and we end up with
an object created using the `Server` constructor.

This is interesting. What happens if we create an object using the literal
notation?

```js
const server = {};
server.constructor; // #=> [Function: Object]
```

Heureka! Turns out the constructor of an object is the `Object` function.
Therefore we can also create objects using the `Object` constructor:

```js
const server = new Object();
```

Keep in mind that creating objects using `new Object()` is rather uncommon.
Typically `{}` or `Object.create(...)` is the way to go!

## Accessing object properties
While we already learned how to access object properties in the above code
samples, we haven't talked about property access in general. There are two ways
to get an object value by its respective key. Let's look at our connections
object again that maps usernames to socket connections:

```js
const connections = {
    max: conn0,
    '0day.hacker': conn1
};
```

### Dot notation
Using dot notation we can access properties of an object using.... a dot:

```js
connections.max; // #=> conn0
```

Keep in mind that when accessing an object property using dot notation, we need
to know the property name upfront. E.g. if we generate a random username, we
can't use this notation. Another problem is that we can't use dot notation for
all key names. If the username contains a dot, we need to use a different
syntax.

In other words, this doesn't work:
```js
connections.0day.hacker;
```

Firstly, a leading number is not allowed here. The dot is also problematic,
since it would be confused with nested property access. The best way to get used
to those notations is by firing up your REPL and playing with it!

### Bracket notation
To solve those issues, JavaScript has another way of accessing properties using
what is called "bracket notation". You already know how to use arrays, bracket
notation works **exactly** the same, except that instead of an index, we now
need to supply a key.

```js
connections['0day.hacker']; // #=> conn1
```

You can also "dynamically" create the key, e.g. by concatenating the key itself:
```js
const key = '0day' + '.hacker';
connections[key]; // #=> conn1
```

## Delete a key-value pair from an object
Whenever a client disconnects from our chat server, we need to remove the
relevant socket entry from the `connections` object. We can use `delete` for
removing an entry by key:

| Key   | Value |
|-------|-------|
| max   | conn0 |
| alex  | conn1 |
| james | conn2 |

After disconnecting James from the server, we would have to run:

```js
delete connections.james;
```

Most likely we would use bracket notation in this case, which works as well:

```js
const username = 'james';
delete connections[username];
```

And that's how easy it is to remove entries from an object!

**Advanced:** Deleting key-value pairs using `delete` deoptimizes the underlying
object by forcing it into dictionary mode. Therefore only use `delete` for
objects that are used for storing data. Some people even recommend just
resetting the property using `connections.james = undefined` (which means the
key is still technically in the object).


## Iterate over key-value pairs in an object
So let's look at what we learned to far: We know how to create objects,
manipulate them and access their properties. One aspect we haven't talked about
yet is how to get all items that are stored in it. In other words: How can we
get all all object entries?


### `Object.keys()`
Probably the easiest (and fastest) way to iterate over object keys is using
`Object.keys`:

```js
const connections = {
    max: conn0,
    alex: conn1
};

const usernames = Object.keys(connections);
usernames; // #=> ['max', 'alex']
```

Then we can iterate over the usernames:

```js
for (let i = 0; i < usernames.length; i++)
    console.log(usernames[i]);
```

Or if we're feeling a bit more adventurous, we can also use `for or` or
`forEach`:

```js
for (const username of usernames)
    console.log(username);
```

```js
usernames.forEach(username => {
    console.log(username)
});
```


### `for in`
In most cases you probably want to use `Object.keys`. `for in` is the
"traditional" way to iterate over objects. It's not bad, but it behaves in ways
you might not expect. E.g. let's say you include some library that decorates the
`Object.prototype` for one reason or another (some libraries used to do this in
the past for polyfills and utility functions, such as `extend` etc.):

```js
Object.prototype.evil = true;
```

Now when we create a new object using our literal notation and iterate over it
using `for in`...

```js
const connections = {
    max: conn0
};

for (let key in connections)
    console.log(key);
```

What do you think this prints to the console? `max`? Unfortunately it also logs
all other properties that have been declared on **any** of its prototypes:

```js
// "evil"
// "max"
```

This is sad. So we would have to check whether or not each property has been
declared on the object itself or its prototype:

```js
for (let key in connections) {
    if (connections.hasOwnProperty(key)) {
        console.log(key);
    }
}
```

This only prints object keys that have been defined on the object itself. This
looks a bit weird and `Object.keys` looks much nicer. Let's use `Object.keys`
from now on.

**Advanced:** Lots of blog posts are going to tell you that the order in which
the properties are being traversed is random. That's not true anymore! Browsers
ended up implementing a traversal order in one form or another, so ES6
standardized the order in which object properties
[will be traversed](http://www.2ality.com/2015/10/property-traversal-order-es6.html).

<p class='util--hide'>View <a href='https://learn.co/lessons/javascript-curriculum-assignment-objects-readme'>javascript curriculum assignment objects readme </a> on Learn.co and start learning to code for free.</p>

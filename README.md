# JavaScript Objects

## Objectives
+ Explain what an object is in JavaScript
+ Create an object in JS
+ Access a value from an object
+ Add a key-value pair to an object
+ Delete a key-value pair from an object
+ Iterate over key-value pairs in an object

## Intro

![](https://cl.ly/400G3k2Y133Z/food-healthy-vegetables-potatoes.jpg)

### Representing Lists

Let's say that you're starting a small grocery store. First, you'll need to brainstorm what to sell. You'll probably make a **list** when you're brainstorming, like this:

- Apples
- Oranges
- Bananas

In JavaScript, we've learned that we can use **arrays** to represent a list. Let's use an array to represent the above list in JS code:

```js
var thingsToSell = ['Apples', 'Oranges', 'Bananas']
```

### Representing Tables

Great! Next, for each item, you will brainstorm (1) how many of each item we'll have in the store, and (2) how much each item will cost. In real life, you'll probably make a **table** like this, probably on a spreadsheet:

<table>
  <tr>
    <th>Name</th>
    <th>Quantity</th>
    <th>Price</th>
  </tr>
  <tr>
    <td>Apples</td>
    <td>100</td>
    <td>$1</td>
  </tr>
  <tr>
    <td>Oranges</td>
    <td>150</td>
    <td>$2</td>
  </tr>
  <tr>
    <td>Bananas</td>
    <td>200</td>
    <td>$1</td>
  </tr>
</table>

How do we represent a table like this in JavaScript? Well, this looks pretty complicated, so let's break it down a bit. We'll focus on just apples first:

<table>
  <tr>
    <th>Name</th>
    <th>Quantity</th>
    <th>Price</th>
  </tr>
  <tr>
    <td>Apples</td>
    <td>100</td>
    <td>$1</td>
  </tr>
</table>

We can try to use arrays to represent this data in JavaScript:

```js
// Store Data
var groceryData = ['Apples', 100, 1]

// Retrieve Data
// First item in the array is the name of the item
groceryData[0] // 'Apples'
// Second item in the array is the quantity
groceryData[1] // 100
// Third item in the array is the price (in dollars)
groceryData[2] // 1
```

However, this is not ideal. It's not immeidately clear that, `groceryData[0]` gets the name of an item, `groceryData[1]` gets the quantity, and so on. Also, if you accidentally switch up the order:

```js
var groceryData = ['Apples', 1, 100]
```

Then you'll be selling just 1 apple, for $100. Must be a delicious apple.

### Enter Objects

<table>
  <tr>
    <th>Name</th>
    <th>Quantity</th>
    <th>Price</th>
  </tr>
  <tr>
    <td>Apples</td>
    <td>100</td>
    <td>$1</td>
  </tr>
</table>

Fortunately, there's a better way to represent the above data in JavaScript. It's called **objects**. Here's how'd you write an object that represent the above data:

```js
var groceryData = {
  'Name': 'Apples',
  'Quantity': 100,
  'Price': 1
}
```

Notice:

- We've used square brackets `[...]` to create an array. We use curly brackets `{...}` to create an object.
- Separated by commas, each item in an object looks like `Something: Something`. The left side of the colon is called a **key**, and the right side of the colon is called a **value**. A key *describes* what the corresponding value *means*. Together, they're called a **key-value pair**.

Now, here's how you can *access* the stuff inside `groceryData`. **Hint**: it's a lot like arrays.

```js
var groceryData = {
  'Name': 'Apples',
  'Quantity': 100,
  'Price': 1
}

groceryData['Name']     // 'Apples'
groceryData['Quantity'] // 100
groceryData['Price']    // 1
```

You'll use square brackets `[...]`, and then use a **key name** as a **string** to access the corresponding value. This is better than the array version we had before, because it's obvious which piece of data (name/quantity/price) we're accessing.

### Order Doesn't Matter for Objects

One important thing to remember about objects is that *the order of key-value pairs don't matter.* In other words, this object:

```js
var groceryData = {
  'Name': 'Apples',
  'Quantity': 100,
  'Price': 1
}
```

is identical to this object:

```js
var groceryData = {
  'Name': 'Apples',
  'Price': 1,
  'Quantity': 100
}
```

So unlike arrays, you will not accidentally switch up price and quantity. If you think about the table analogy, it should make sense - the following two tables are describing exact same data:

<table>
  <tr>
    <th>Name</th>
    <th>Quantity</th>
    <th>Price</th>
  </tr>
  <tr>
    <td>Apples</td>
    <td>100</td>
    <td>$1</td>
  </tr>
</table>

<table>
  <tr>
    <th>Name</th>
    <th>Price</th>
    <th>Quantity</th>
  </tr>
  <tr>
    <td>Apples</td>
    <td>$1</td>
    <td>100</td>
  </tr>
</table>

With that said, let's dive deep into the details of JavaScript objects!

## Creating Objects

Here's the syntax for creating an object we've seen already:

```js
var object = {
  'name': 'Flatiron'
}
```

Now, here's something new: *the quotes around each key is optional*. So the following also works:

```js
var object = {
  name: 'Flatiron'
}
```

We recommend using **unquoted** keys unless the key name contains invalid characters for variable name characters, such as hyphens `-` ([you can check them here](https://mothereff.in/js-variables)).

```js
var object1 = {
  // Unquoted keys are recommended, less typing!
  name: 'Flatiron'
}
var object2 = {
  // Must use a quoted key
  `n-a-m-e`: 'Flatiron'
}
```

Notice that the key name is `name` and not `Name`. We recommend using **lower camel case** for key names like `someKeyName`, **unless** the underlying data we're trying to represent has some strict case requirement.

In JavaScript, **all keys in JavaScript objects are strings**. So each key automatically gets converted into a string, even if it's a number.

```js
var object = {
  1: 'One'
}

// ...is equivalent to:
var object = {
  '1': 'One'
}
```

Furthermore, the keys must be **unique**. If they're not unique, then the last key-value pair overrides the previous one, like this:

```js
var object = {
  name: 'Flat',
  name: 'Flatiron'
}

// ...is equivalent to:
var object = {
  name: 'Flatiron'
}
```

But the values can be the same:

```js
// This is perfectly fine
var object = {
  key1: 'hello',
  key2: 'hello'
}
```

JavaScript objects can use **any type** as values, just like values in an array. So you can have an array as a value, for example:

```js
var object = {
  number: [1, 2, 3]
}
```

You can also create an **empty** object, just like you can create empty arrays.

```js
var emptyObject = {}
```

Lastly, there are other ways to create objects, but these methods are rarely used (more unnecessary typing too).

```js
var object = {
  number: 5
}

// ...is equivalent to:
var object = new Object({
  number: 5
})
```

## Accessing a Value in Objects

Recall how we can access a value in an object by specifying a key:

```js
var object = {
  name: 'Flatiron'
}

object['name'] // Flatiron
```

You can also use **dot notation**, which is a `.` followed by a key name.

```js
object.name // Flatiron
```

Which one should you use? Here's our recommendation:

Most of the time, use **dot notation**.

```js
var object = {
  name: 'Flatiron'
}

// Recommended
object.name // Flatiron
```

If the key is a variable, use **square brackets**.

```js
var object = {
  name: 'Flatiron'
}

var key = 'name'

object[key] // Flatiron
object.key  // Doesn't work, because it tries to do object['key']
```

If the key name contains invalid characters for variable names ([you can check here](https://mothereff.in/js-variables)), use **square brackets**.

```js
var object = {
  'n-a-m-e': 'Flatiron'
}

object['n-a-m-e'] // Works
object.n-a-m-e    // Doesn't work, hyphens are invalid variable names
```

Finally, if you try to access a key-value pair *when the key doesn't exist*, you'll get something called `undefined`. You'll learn more about `undefined` later.

```js
var object = {
  name: 'Flatiron'
}

object.address // undefined
```

## Adding, Updating, and Removing Key-Value Pairs

Sometimes you change your mind and you'd want to add or remove key-value pairs to/from an object. Recall our grocery store example:

<table>
  <tr>
    <th>Name</th>
    <th>Quantity</th>
    <th>Price</th>
  </tr>
  <tr>
    <td>Apples</td>
    <td>100</td>
    <td>$1</td>
  </tr>
</table>

and the object representation (note we're using lower case, non-quoted keys):

```js
var groceryData = {
  name: 'Apples'
  quantity: 100,
  price: 1
}
```

### Adding

Let's say we'd want to store more information, such as whether an item is organic or not:

<table>
  <tr>
    <th>Name</th>
    <th>Quantity</th>
    <th>Price</th>
    <th>Organic</th>
  </tr>
  <tr>
    <td>Apples</td>
    <td>100</td>
    <td>$1</td>
    <td>true</td>
  </tr>
</table>

To add key-value pairs, we can use a syntax similar to accessing it - this time, we'll specify a key **and** a value that will be set.

```js
var groceryData = {
  name: 'Apples'
  quantity: 100,
  price: 1
}

groceryData.organic = true

// groceryData is now:
{
  name: 'Apples'
  quantity: 100,
  price: 1,
  organic: true
}
```

We can also use square brackets - to decide which syntax to use, follow the same rules as accessing data.

```js
// Same as groceryData.organic = true
groceryData['organic'] = true
```

### Updating

How about **updating** a key-value pair? If you try to use the same syntax as adding a key-value pair, but *if the key already exists*, then it overrides the corresponding value.

Let's try to double the price of apples from $1 to $2:

<table>
  <tr>
    <th>Name</th>
    <th>Quantity</th>
    <th>Price</th>
  </tr>
  <tr>
    <td>Apples</td>
    <td>100</td>
    <td><s>$1</s> $2</td>
  </tr>
</table>

```js
var groceryData = {
  name: 'Apples'
  quantity: 100,
  price: 1
}

groceryData.price = 2

// groceryData is now:
{
  name: 'Apples'
  quantity: 100,
  price: 2
}
```

Again, you can also do `groceryData['price'] = 2` to achieve the same effect.

### Deleting

How about **deleting** a key-value pair? **Note:** you won't do this as often as adding/updating, so even experienced developers often forget how to do it.

But here's how. Let's try to delete the price column:

<table>
  <tr>
    <th>Name</th>
    <th>Quantity</th>
    <th><s>Price</s></th>
  </tr>
  <tr>
    <td>Apples</td>
    <td>100</td>
    <td><s>$1</s></td>
  </tr>
</table>

```js
var groceryData = {
  name: 'Apples'
  quantity: 100,
  price: 1
}

delete groceryData.price

// groceryData is now:
{
  name: 'Apples',
  quantity: 100
}
```

Like accessing/adding key-value pairs, you can also do `delete groceryData['price']`.

## Iterating over Key-Value Pairs in an Object

Recall that, you can iterate over values in an array using a `for` loop:

```js
var array = [1, 2, 3]

// Prints:
// 1
// 2
// 3
for (var i = 0; i < array.length; i++) {
  console.log(array[i])
}
```

You can use `for` loops to iterate over an object too. But this time, the `for` loop looks a bit different. Let's consider the following object:

```js
var groceryData = {
  name: 'Apples',
  quantity: 100,
  price: 1
}
```

You can iterate over its **keys** like this.

```js
for (var key in groceryData) {
  console.log(key)
}
```

This is called a `for-in` loop because there are two keywords: `for` and `in`.

The above code prints (in any order):

```
name
quantity
price
```

Note the phrase **"in any order."** Recall that the order of key-value pairs in an object doesn't matter, so the order `for` loop iterates over key-value pairs will be unknown (could be a totally random order, so don't rely on it).

Now, what if you want to iterate over the object's **values** too?

Well, since you already have the keys, you just need to use them to fetch the values. On each iteration, the key is stored in the variable `key`, so use square brackets to access the corresponding values:

```js
for (var key in groceryData) {
  console.log(key + ' ' + groeryData[key])
}
```

The above code prints (in any order):

```
name Apples
quantity 100
price 1
```

There are many other ways to iterate over an object, but we'll cover those in further lessons.

## Lastly: Representing the Full Table

We forgot one thing - how do we represent the full grocery data table we showed at the beginning, in JavaScript?

<table>
  <tr>
    <th>Name</th>
    <th>Quantity</th>
    <th>Price</th>
  </tr>
  <tr>
    <td>Apples</td>
    <td>100</td>
    <td>$1</td>
  </tr>
  <tr>
    <td>Oranges</td>
    <td>150</td>
    <td>$2</td>
  </tr>
  <tr>
    <td>Bananas</td>
    <td>200</td>
    <td>$1</td>
  </tr>
</table>

Each row (except the header row) is an object, so we can think of this as **an array of objects**.

```js
var groceryData = [
  {
    name: 'Apples'
    quantity: 100
    price: 1
  },
  {
    name: 'Oranges'
    quantity: 150
    price: 2
  },
  {
    name: 'Bananas'
    quantity: 200
    price: 1
  }
]
```

That's it!

## ...

<p class='util--hide'>View <a href='https://learn.co/lessons/javascript-curriculum-assignment-objects-readme'>javascript curriculum assignment objects readme </a> on Learn.co and start learning to code for free.</p>

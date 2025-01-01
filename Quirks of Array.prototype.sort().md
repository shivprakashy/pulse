Quirks of Array.prototype.sort()
---

JavaScript's array sorting can lead to some fascinating (and sometimes frustrating) quirks! 
The `sort()` function is defined in the Array prototype in JavaScript. This means that every array you create in JavaScript inherits the `sort()` method from the `Array.prototype`.

By default, the `sort()` method sorts elements as strings. This can lead to unexpected results when sorting numbers.
```
const numbers = [10, 2, 5, 1];
numbers.sort(); // Output: [1, 10, 2, 5]
```

To fix this, you need to provide a compare function:
```
numbers.sort((a, b) => a - b); // Output: [1, 2, 5, 10]
```
`Array.prototype.sort()` method itself provides a predefined compare function for strings, which sorts them in lexicographical order (i.e., dictionary order). 

The <i>compare function</i> is used as an argument in the sort() method to determine the order of the elements. It allows you to define your custom sorting logic. The compare function takes two arguments (let's call them a and b) and returns a number that dictates the sort order:
<ul>
    <li><b>Negative value:</b> If the compare function returns a negative value (e.g., a - b), then a comes before b.</li>
    <li><b>Zero:</b> If it returns zero, the order of a and b remains unchanged.</li>
    <li><b>Positive value:</b> If it returns a positive value (e.g., b - a), then a comes after b.</li>
</ul>

Here's an example to illustrate:
```
const numbers = [4, 2, 5, 1, 3];
numbers.sort((a, b) => a - b); // Output: [1, 2, 3, 4, 5]
```
In this case:
<ul>
    <li>When a = 4 and b = 2, 4 - 2 results in a positive value, so 4 comes after 2.</li>
    <li>When a = 2 and b = 5, 2 - 5 results in a negative value, so 2 comes before 5.</li>
</ul>

You can also use the compare function to sort strings, objects, or more complex data structures. Here's a case-insensitive string sort:
```
const items = ["Banana", "apple", "Cherry"];
items.sort((a, b) => a.toLowerCase().localeCompare(b.toLowerCase()));
// Output: ["apple", "Banana", "Cherry"]
```
By customizing the compare function, you can gain precise control over how elements are sorted in an array.

Let's discuss some common compare function implementations.

**1. In-Place Sorting:** The sort() method sorts the array in place, meaning it modifies the original array.
```
const fruits = ["banana", "apple", "cherry"];
fruits.sort();
console.log(fruits); // Output: ["apple", "banana", "cherry"]
```
**2. Case Sensitivity:** The default string sort is case-sensitive.
```
const items = ["Banana", "apple", "Cherry"];
items.sort(); // Output: ["Banana", "Cherry", "apple"]
```
For a case-insensitive sort, you can use a compare function that converts strings to lowercase:
```
items.sort((a, b) => a.toLowerCase().localeCompare(b.toLowerCase()));
// Output: ["apple", "Banana", "Cherry"]
```
**3. Undefined Values:** Sorting arrays with `undefined` values can lead to unusual results.
```
const array = [3, undefined, 1];
array.sort(); // Output: [1, 3, undefined]
```
**4. Custom Compare Function:** You can create complex sorting logic using custom compare functions.
```
const objects = [{ name: "Zebra" }, { name: "apple" }, { name: "Banana" }];
objects.sort((a, b) => a.name.localeCompare(b.name));
// Output: [{ name: "apple" }, { name: "Banana" }, { name: "Zebra" }]
```
Or, use the Object Property.
```
const byName = (a, b) => a.name.localeCompare(b.name); const objects = [{ name: "Zebra" }, { name: "apple" }, { name: "Banana" }]; objects.sort(byName); // Output: [{ name: "apple" }, { name: "Banana" }, { 
```

**5. Sorting Performance:** The `sort()` method's performance can vary based on the browser and JavaScript engine. V8 (used in Chrome and Node.js) uses a variant of `QuickSort` for numeric arrays and `Timsort` for non-numeric arrays.

## Data types

### Primitive

- **number** : Represents numeric values, e.g., 123, 3.14.
- **string** : Represents textual data, e.g., 'Hello, world!', "JavaScript".
  - We can represent string in three ways by using single quotes('Hello') , double.quotes("Hello") , string template literal (\`Hello\`).
  - With help of string template literal we can add dynamic data to string using '${variableName}'
- **boolean**: Represents true or false values.
- **undefined**: Represents a variable that has been declared but not assigned a value.
- **null**: Represents the intentional absence of any object value.
- **bigint**: Represents whole numbers larger than 2^53 - 1, which is the largest number JavaScript can reliably represent with the Number primitive.
- **NaN** : stands for "Not a Number". It is a special value of the Number data type that represents a value which is not a valid number.

### Non-Primitive

- **array**: Represents a single, ordered list of values, e.g., [1, 2, 3, 4].
  - We can access array elements by index which start from 0 end at arr.length
    Two ways to create an array.

```
// 1. By using '[]'
let arr = [1,2,3,4]; // 1st way
//2. By using new Array()
let arr1 = new Array(length);

//To read the values in an array use indexes
//to find out element present at some index
let element  = arr[index];

//To update
arr[index] = 'value'

//to delete
delete arr[index] // will create a empty space in that index
```

- **object** :Represents a collection of key-value pairs, e.g., { name: 'John', age: 30 }.

```
// Creating an empty object
//using object literal
let person = {};
//using new Object()
let car = new Object();

// Adding properties to the object using dot notation
//can be used when we know property name ahead of accessing time
person.name = 'John';
person.age = 30;

// Adding properties using bracket notation
//can be used when we are accessing key dynamically
person['city'] = 'New York';

//updating the property
person.name = 'eshwar';
person['age'] = 24;

console.log(person); // Output: { name: 'John', age: 30, city: 'New York' }

```

## Utility Methods:

- **console.log()** : static method outputs a message to the console.

```
console.log(val1)
console.log(val1, /* …, */ valN)
```

- **console.clear()** : static method clears the console if the console allows it. console, like those running on browsers, will allow it; a console displaying on the terminal, like the one running on Node, will not support it, and will have no effect (and no error).

```
console.clear()
```

- **console.time()** : static method starts a timer you can use to track how long an operation takes. You give each timer a unique name, and may have up to 10,000 timers running on a given page. When you call console.timeEnd() with the same name, the browser will output the time, in milliseconds, that elapsed since the timer was started.

```
console.time()
console.time(label)
```

- **console.timeEnd()** : static method stops a timer that was previously started by calling console.time().

```
console.timeEnd()
console.timeEnd(label)
```

## Variable Declarations

1. var

   - **Scope**: Function-scoped or globally scoped (if declared outside any function).
   - **Hoisting**: Variables declared with var are hoisted to the top of their scope and initialized with undefined.
   - **Reassignment**: Can be reassigned and redeclared within the same scope.

```
var name = 'John';

console.log(name); // Output: John
```

2. let

   - **Scope**: Block-scoped (scoped to the nearest enclosing block).
   - **Hoisting**: Variables declared with let are hoisted to the top of their block, but not initialized (called "temporal dead zone").
   - **Reassignment**: Can be reassigned but not redeclared within the same scope.

```
let age = 30;
console.log(age);
```

3. const

   - **Scope**: Block-scoped (like let).
   - **Hoisting**: Variables declared with const are hoisted to the top of their block, but not initialized (same "temporal dead zone" as let).
   - **Reassignment**: Cannot be reassigned. However, if the value is an object or array, its properties or elements can be modified.

```
const name = 'eshwar';
//name = 'abhi' // TypeError: Assignment to constant variable.
console.log(name);
```

### why primitive values are immutable and Non-primitive values are mutable.

1. **Primitive Values (Immutable)**
   Primitive values in JavaScript (such as numbers, strings, booleans, null, undefined, and symbols) are immutable. This means that once a primitive value is created, it cannot be changed. If you attempt to change the value of a primitive, you're actually creating a new value in memory.

   - **Memory Allocation**: Each primitive value is stored directly in the location where the variable accesses it.

   - **Direct Manipulation**: When you manipulate a primitive value, you're actually creating a new copy of the value rather than modifying the existing one.

```
let x = 10;   // Primitive value (number)
x = 20;  // Creates a new number value 20, and updates x to point to this new value
```

2. Non-primitive Values (Mutable)
   Non-primitive values (objects and arrays) are stored and manipulated differently compared to primitive values.

   - **Reference to Memory**: Non-primitive values are stored as references (or pointers) to objects or arrays stored in memory.

   - **Mutable Properties**: You can modify the properties of objects and arrays directly without changing the reference itself.

```
let obj = { name: 'Alice' };   // Non-primitive value (object)
obj.name = 'Bob';       // Modifies the property of the existing object
```

- **Pass by Reference**: When you pass a non-primitive value to a function or assign it to another variable, you're passing a reference to the original object or array. Any changes made to this reference affect the underlying object or array.

```
let arr1 = [1, 2, 3];    // Non-primitive value (array)
let arr2 = arr1;         // arr2 now refers to the same array as arr1
arr2.push(4);            // Modifies the original array [1, 2, 3, 4]
console.log(arr1);       // Output: [1, 2, 3, 4]
```

### Variable naming

- Variable name should not be
  - keyword
  - start with a number
  - cannot contain special characters excpet '$' or '\_'
- Varibale name should have a meaning full name describing what are we storing.

## Loops

1. **while loop**

   - The `while` loop repeatedly executes a block of code as long as a specified condition is true.

```
let count = 0;
while (count < 5) {
    console.log(count);
    count++;
}
// Output:
// 0
// 1
// 2
// 3
// 4
```

- **Usage**: Use when you don't know in advance how many times the loop will run, based on a condition that can change during execution.

2. **for loop**

- The for loop repeats a block of code a specified number of times.

```
for (let i = 0; i < 5; i++) {
    console.log(i);
}
// Output:
// 0
// 1
// 2
// 3
// 4
```

- **Initialization**: Declares and initializes a loop variable (i in the example).

- **Condition**: Defines the condition for continuing the loop (i < 5).

- **Increment**: Specifies how the loop variable changes after each iteration (i++).

- **Usage**: Use when you know the number of iterations or want more control over the loop initialization, condition, and increment/decrement.

3. **for...of loop**

- The `for...of` loop iterates over iterable objects (arrays, strings, etc.) and allows you to access each element directly.

```
let arr = [1, 2, 3];
for (let element of arr) {
    console.log(element);
}
// Output:
// 1
// 2
// 3
```

- **Usage**: Ideal for iterating over values in arrays, strings, and other iterable objects where you need direct access to each element's value.

4.  **for...in loop**

- The `for...in loop` iterates over the enumerable properties of an object, including inherited properties from its prototype chain.

```
let person = {
    name: 'John',
    age: 30,
    city: 'New York'
};
for (let key in person) {
    console.log(key + ': ' + person[key]);
}
// Output:
// name: John
// age: 30
// city: New York
```

- **Usage**: Use when iterating over object properties, but be cautious with arrays and objects where the iteration order may not be guaranteed, and inherited properties may be included.

## Conditionals

- **if-else** : If we want to perform an operation based on certain condition we use `if-else` .
- **switch** : `switch` can be used as alternative for `if-else` conditional statement.When we have a fixed set of values to compare against we go for `switch`
- **ternary operator** : when we have only one condition to check and perform anyone of two actions based on output we can use ternary operator.

```
  syntax: condition ? operator1 : operator2 ;
  if condition true operator1 get executed or else operator2
```

## Operators

- **Mathematical operators** : (+,-,\*,/,\*\*(exponantial),%(for remainder))
- **Logical operators** : (&&,||,!) returns boolean value
- **Comparison operators** : (==, ===, !==, != , >, >=, <=, <)
- **Operator precendence** :
  | Precedence | Operator |
  |:----------:|:---------:|
  | 1 | '.' , '[]'|
  | 2 | () |
  | 3 | ++ , -- (postfix) |
  | 4 | ++ , -- (prefix) , (right to left) + , - ,! , ~ , typeof , void , delete |
  | 5 | exponentiation|
  | 6 |\*,/,%|
  | 7 | +,- |
  | 8 | <<, >>, >>> |
  | 9 | < ,<=, >, >= , in , instanceof |
  | 10| == , != ,=== ,!== |
  | 11 | & |
  | 12 | ^ |
  | 13 | \| |
  | 14 | && |
  | 15 | \|\| , \?\? |
  | 16 | = += -= \_= /= %= <<= >>= >>>= &= ^=` |
  | 17 | , |
  - **Precedence**: Operators with higher precedence are evaluated before those with lower precedence.

## Functions

### How to declare a function and what are the different ways?

functions can be declared in different ways

1. **function Declaration** :

```
function functionName(parameter1,parameter2,....){
    //statements
}
```

2. **function experssion** : declaring an anonymous function and assiging to a variable.

```
let functionName = function(parameter1,parameter2,....){
    //statements
}
```

3. **arrow function** :

```
let functionName = (parameter1,parameter2,....) => {
    //statements
}
```

### What are parameters, arguments?

- **parameters** : These are the variables declarations while declaring a function which are used to receive a value.
- **arguments** : These are the actual values passed while calling a function.

### What is return statement?

- `return` - is a keyword which returns back the control to calling function with or without a value.

### How to call a function?

- function name followd by paranthesis ()

---
title: Understanding Parameters and Arguments in JavaScript
date-modified: 2024-05-31
---

In JavaScript, you'll frequently hear terms like "parameters" and "arguments" when working with functions. While they may seem similar, they play distinct roles in your code. Let’s delve into these concepts.

### What are Parameters?

Parameters are variables listed as part of the function definition. Think of them as placeholders or named variables that will hold the values you pass into the function. They are defined in the function declaration.

Here’s an example:
```javascript
function greet(name) {  // 'name' is the parameter
  console.log("Hello, " + name);
}
```
In the above function `greet`, `name` is a parameter. It’s essentially a label that you use within the function to refer to the value it will eventually hold.

### What are Arguments?

Arguments are the actual values you pass into the function when you call it. These values are assigned to the function’s parameters, allowing the function to operate using them.

Example:
```javascript
greet("Alice"); // "Alice" is the argument
```
In this example, when `greet` is called, `"Alice"` is the argument. This value is passed to the function and becomes the content of the `name` parameter.

### Visualization

```javascript
function greet(name) {  // 'name' is the parameter. ←
  console.log("Hello, " + name);
}

greet("Alice");  // "Alice" is the argument. →
```

### Key Points to Remember

- **Definition**:
  - **Parameter**: Variable in the function declaration.
  - **Argument**: Actual value passed to the function.
- **Usage**:
  - Parameters are used within functions to act on the values you pass.
  - Arguments provide those values when the function is called.

### Conclusion

Understanding the distinction between parameters and arguments helps in writing clearer, more effective functions. Parameters act as your function's input placeholders, while arguments are the real values you feed into those placeholders. Happy coding!


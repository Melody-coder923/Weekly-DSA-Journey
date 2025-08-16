# 🧠 Structural Recursion: A Summary

## What Is Structural Recursion?

**Structural recursion** is a form of recursion that follows the structure of the input data rather than numerical values or indices. It's most commonly used when dealing with **nested or recursive data types**, such as trees, linked lists, and nested lists.

---

## Key Characteristics

- 🔁 **Follows the shape of the data**  
  Recursion progresses by unpacking the structure (like list elements, tree nodes), not by counting.

- 🧱 **Base case is based on atomic data**  
  Recursion stops when it reaches the simplest form (e.g., an integer, a leaf node, an empty list).

- 🌿 **Common in recursive data structures**  
  Like JSON, XML, parse trees, or `NestedInteger` objects in LeetCode problems.

---

## Structural vs. Numeric Recursion

|                      | **Structural Recursion**       | **Numeric Recursion**         |
|----------------------|-------------------------------|-------------------------------|
| Input type           | Recursive/structured data     | A number (e.g. `n`)           |
| Base case            | Atomic unit (e.g. integer)    | When `n == 0` or `n == 1`     |
| Recursion progresses | By consuming structure        | By incrementing/decrementing  |
| Example use cases    | Trees, nested lists, JSON     | Factorial, Fibonacci, countdown |

---

## Common Use Cases

- 🌲 Tree traversals (preorder, inorder, postorder)
- 🧩 Parsing nested expressions
- 📦 JSON or XML data walking
- 📚 Problems like LeetCode 339 (Nested List Weight Sum)

---

## Why Use It?

- Naturally mirrors the recursive definition of structured data
- Clean, readable, and follows the logic of the data itself
- Avoids unnecessary conversions or flattening of input

**LC 339 Nested List Weight Sum**
```
def depthSum(nestedList, depth=1):
    total = 0
    for ni in nestedList:
        if ni.isInteger():
            total += ni.getInteger() * depth
        else:
            total += depthSum(ni.getList(), depth + 1)
    return total
```
**Numeric Recursion**
```
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)
```

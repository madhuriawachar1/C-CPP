# Python Data Types & Tuple Immutability Guide

## 1. Master Classification Chart

This chart details how Python categorizes its core built-in data types by structure, mutability, and ordering rules.

| Data Type | Main Category | Sub-Category / Type | Mutable? | Ordered? | Allows Duplicates? | Example |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Integer** | Numeric | `int` | ❌ No | ❌ N/A | ❌ N/A | `42` |
| **Float** | Numeric | `float` | ❌ No | ❌ N/A | ❌ N/A | `3.14` |
| **Complex Number** | Numeric | `complex` | ❌ No | ❌ N/A | ❌ N/A | `2 + 3j` |
| **Boolean** | Numeric / Core | `bool` | ❌ No | ❌ N/A | ❌ N/A | `True` |
| **String** | Sequence Type | `str` | ❌ No | 🟢 Yes | 🟢 Yes | `"hello"` |
| **List** | Sequence Type | `list` | 🟢 Yes | 🟢 Yes | 🟢 Yes | `[1, 2, 3]` |
| **Tuple** | Sequence Type | `tuple` | ❌ No | 🟢 Yes | 🟢 Yes | `(1, 2, 2)` |
| **Set** | Set Type | `set` | 🟢 Yes | ❌ No | ❌ No | `{1, 2, 3}` |
| **Dictionary** | Mapping Type | `dict` | 🟢 Yes | 🟢 Yes* | ❌ No (Keys) | `{'a': 1}` |

*\*Note on Dictionary Ordering: In modern Python (3.7+), dictionaries maintain the **insertion order** of their keys, but they do not support numeric indexing like lists or tuples (e.g., you cannot use `d[0]` to get the first item).*

---

## 2. Understanding Tuple Immutability

Tuples are **immutable**, meaning they cannot be altered, added to, or modified once they are created in memory.

### Example A: Trying to Modify an Element
If you try to change an existing value inside a tuple using its index, Python will raise a `TypeError`.

```python
# Create a tuple
fruits = ("apple", "banana", "cherry")

# Trying to change "banana" to "orange"
fruits[1] = "orange"
```

#### The Result:
```text
TypeError: 'tuple' object does not support item assignment
```

---

### Example B: Trying to Add More Elements
Unlike lists, tuples do not have an `.append()`, `.extend()`, or `.insert()` method. If you try to call these methods to add a new item, Python will throw an `AttributeError`.

```python
# Create a tuple
numbers = (1, 2, 3)

# Trying to append a new number
numbers.append(4)
```

#### The Result:
```text
AttributeError: 'tuple' object has no attribute 'append'
```

---

### The "Plus Equals" (`+=`) Illusion
You might sometimes see code like this where it looks like an item is successfully added to a tuple:

```python
numbers = (1, 2, 3)
numbers += (4,)

print(numbers) # Output: (1, 2, 3, 4)
```

#### What is actually happening under the hood?
1. Python does **not** modify the original tuple.
2. It takes `(1, 2, 3)` and `(4,)`, breaks the old variable connection, and creates a **brand new tuple** in a completely different spot in your computer's memory.
3. This is much slower than appending to a list because Python has to copy and rewrite the entire collection from scratch.

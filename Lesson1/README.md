# AI Lab: Deep Learning for Computer Vision

### WorldQuant University

## 🧩 Module 4.1: Fix My Code! 🐞

This project demonstrates how to write **fault-tolerant Python code** by handling runtime errors using `try-except-else` blocks and managing variable outputs through tuple unpacking. These techniques ensure programs run smoothly even when unexpected inputs occur.

---

## 🧠 Key Concepts and Code Examples

### 1. Using `try-except-else` Blocks

`try-except-else` blocks are used to handle exceptions gracefully. The `try` block executes code that might raise an error, the `except` block catches and handles it, and the optional `else` block runs if no exception occurs.

#### Example 1: Handling Index Errors

```python
def lookup(my_list, index):
    try:
        value = my_list[index]
    except IndexError:
        return "Error: Index out of range."
    else:
        return f"The value at index {index} is {value}."

print(lookup(["a", "b", "c"], 2))   # ✅ Index in range
print(lookup(["a", "b", "c"], 5))   # ❌ Index out of range
```

**Explanation:**
If an invalid index is accessed, the program returns an error message instead of stopping execution.

---

#### Example 2: Fixing Division by Zero

```python
def divide_numbers(numerator, denominator):
    try:
        result = numerator / denominator
    except ZeroDivisionError:
        return "Error: Cannot divide by zero."
    else:
        return f"The result of {numerator} divided by {denominator} is {result}."

print(divide_numbers(10, 2))  # ✅ Valid division
print(divide_numbers(10, 0))  # ❌ Division by zero
```

**Explanation:**
This version prevents a `ZeroDivisionError` by checking for invalid divisions and returning a clear message.

---

#### Example 3: Handling Missing Dictionary Keys

```python
users = {
    342: "Kwame Nkrumah",
    102: "Nguyen Thi Linh",
    423: "Muhammad bin Abdullah",
    654: "Fatou Diop",
    976: "Diana Martinez",
}

def find_user_name(user_id, users):
    try:
        user_name = users[user_id]
    except KeyError:
        return f"Error: User ID {user_id} not found."
    else:
        return f"User ID {user_id} corresponds to {user_name}."

print(find_user_name(654, users))  # ✅ Found
print(find_user_name(999, users))  # ❌ Not found
```

**Explanation:**
Using `try-except` ensures the code continues even if a non-existent user ID is requested.

---

### 2. Tuple Unpacking with `*`

Tuple unpacking allows us to assign multiple returned values to variables easily. The `*` operator helps collect additional items into a list, avoiding `ValueError` when functions return variable-length outputs.

#### Example 4: Handling Variable Outputs

```python
import random

def unpredictable_function():
    if random.choice([True, False]):
        return (1, 2)
    else:
        return (1, 2, 3)

for n in range(1, 6):
    print(f"Call {n}:")
    first, second, *rest = unpredictable_function()
    print(f"  First: {first}, Second: {second}")
    if rest:
        print(f"  Third: {rest[0]}")
    else:
        print("  No third item present")
```

**Explanation:**
If the function returns two items, `rest` becomes an empty list; if three, `rest` captures the extra value.

---

#### Example 5: Tuple Unpacking in Student Info

```python
students = {
    "Aisha": {"age": 18, "grade": "Pass"},
    "Carlos": {"age": 35},
    "Li Wei": {"age": 22, "grade": "Fail"},
    "Fatima": {"age": 27},
    "Yuki": {"age": 51, "grade": "Pass"},
}

def get_student_info(student_name, students):
    student_info = students[student_name]
    return list(student_info.values())

def print_student_info(student_name, students):
    age, *rest = get_student_info(student_name, students)
    print(f"{student_name} is {age} years old.")
    if rest:
        print(f"{student_name} earned a {rest[0]}.")
    else:
        print(f"No grade information available for {student_name}.")

print_student_info("Aisha", students)
print_student_info("Carlos", students)
```

**Explanation:**
The `*rest` captures optional data (like grade) so the code works whether a student has one or two data fields.

---

## 🎯 Learning Outcomes

* Use `try-except-else` to create **fault-tolerant programs**.
* Apply **tuple unpacking** with `*` to handle unpredictable outputs.
* Write code that remains **stable** and **readable** under unexpected conditions.
* Build confidence in debugging and improving existing functions.

---

## 🏫 License

© 2024 [WorldQuant University](https://www.wqu.edu/)
Licensed under [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/).

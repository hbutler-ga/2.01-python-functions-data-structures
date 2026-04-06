# Module 3: Functions and Data Structures

## Module Overview

In this module, learners move from writing one-off Python scripts to writing **reusable, organized code**. The focus is on three connected ideas:

1. **Functions** help us package logic so we can reuse it
2. **Data structures** help us organize information in useful ways
3. **Pandas** helps us apply that logic to tabular data

By the end of the session, learners should understand not just *how* to write functions, but *why* modular code matters in real analytical work.

---

## Learning Objectives

By the end of this module, you will be able to:

- Define and call custom Python functions
- Explain the role of parameters, arguments, and return values
- Use lists, dictionaries, tuples, and sets for structured data
- Write simple validation checks inside functions
- Use Pandas inside functions for small cleaning tasks
- Refactor repetitive logic into reusable code
- Save and version reusable scripts with Git and GitHub

---

## Session Breakdown

| Segment | Topic | Duration (minutes) |
|---|---|---:|
| 1 | Why Functions and Modular Code Matter | 15 |
| 2 | Defining Functions: Parameters, Arguments, and Return Values | 25 |
| 3 | Core Python Data Structures | 25 |
| 4 | Using Functions with Pandas | 30 |
| 5 | Validation, Refactoring, and Practice | 25 |

---

## 1. Why Modular Code Matters

As your code gets longer, copy-pasting the same logic becomes difficult to maintain. Functions solve that problem.

### Without Functions

```python
quiz_scores = [80, 90, 100]
quiz_average = sum(quiz_scores) / len(quiz_scores)
print(quiz_average)

exam_scores = [70, 85, 95]
exam_average = sum(exam_scores) / len(exam_scores)
print(exam_average)
```

This works, but the same logic is repeated.

### With a Function

```python
def calculate_mean(values):
    return sum(values) / len(values)

print(calculate_mean([80, 90, 100]))
print(calculate_mean([70, 85, 95]))
```

Now the logic is written once and reused many times.

### Why this matters in real work

Functions help you:

- reduce repetition
- debug more easily
- test one piece of logic at a time
- make code easier for teammates to read
- scale workflows across multiple datasets

---

## 2. Defining Functions

A function is a reusable block of code that performs a task.

### Basic Syntax

```python
def greet_user(name):
    return f"Hello, {name}!"
```

### Key Terms

- **Function definition**: the code that creates the function
- **Parameter**: a variable listed in the function definition
- **Argument**: the actual value passed into the function
- **Return value**: the output the function sends back

### Example

```python
def multiply_numbers(a, b):
    result = a * b
    return result

answer = multiply_numbers(4, 5)
print(answer)
```

In this example:

- `a` and `b` are parameters
- `4` and `5` are arguments
- `20` is the return value

---

## 3. Important Function Concepts

### A. Functions Should Usually Do One Clear Thing

```python
def calculate_total(price, quantity):
    return price * quantity
```

This function has one job: calculate a total.

### B. Default Parameters

```python
def power_number(base, exponent=2):
    return base ** exponent

print(power_number(5))      # 25
print(power_number(5, 3))   # 125
```

### C. Returning vs Printing

```python
def add_numbers(a, b):
    return a + b
```

`return` sends a value back so it can be reused later.

```python
def add_numbers_print(a, b):
    print(a + b)
```

This prints the result, but does not return it for reuse.

### D. Docstrings

Docstrings explain what a function does.

```python
def convert_to_upper(text):
    """Return a string in uppercase."""
    return text.upper()
```

### E. Variable Scope

Variables created inside a function stay inside that function unless returned.

```python
def create_message(name):
    message = f"Welcome, {name}"
    return message
```

---

## 4. Python Data Structures for Structured Data

Python data structures help us store and organize information.

### A. Lists

Lists store ordered, changeable collections.

```python
scores = [88, 91, 79, 93]
print(scores[0])
```

Use lists when:

- order matters
- items may change
- duplicates are allowed

### B. Dictionaries

Dictionaries store key-value pairs.

```python
student = {
    "name": "Ava",
    "score": 95,
    "passed": True
}

print(student["name"])
```

Use dictionaries when:

- you want labels for values
- you want to describe records clearly

### C. Tuples

Tuples are ordered collections that should not be changed.

```python
coordinates = (40.7128, -74.0060)
```

Use tuples when:

- order matters
- the values should stay fixed

### D. Sets

Sets store unique values.

```python
skills = {"python", "sql", "python", "excel"}
print(skills)
```

Use sets when:

- you want unique items only
- order does not matter

---

## 5. Combining Functions and Data Structures

Functions often accept data structures as inputs.

### Example: Calculate Average Score

```python
def calculate_mean(values):
    return sum(values) / len(values)

scores = [85, 90, 95]
print(calculate_mean(scores))
```

### Example: Pull a Value from a Dictionary

```python
def get_student_score(student_record):
    return student_record["score"]

student = {"name": "Luis", "score": 88}
print(get_student_score(student))
```

### Example: Work with a List of Dictionaries

```python
records = [
    {"name": "Ava", "score": 95},
    {"name": "Luis", "score": 88},
    {"name": "Mina", "score": 91}
]

def get_names(records):
    return [record["name"] for record in records]

print(get_names(records))
```

This pattern is common in analytics and data processing.

---

## 6. Validation Inside Functions

Validation checks help catch problems early.

### Example

```python
def calculate_mean(values):
    if not isinstance(values, list):
        raise TypeError("values must be a list")
    if len(values) == 0:
        raise ValueError("values must not be empty")
    return sum(values) / len(values)
```

This is often better for beginner lessons than relying heavily on `assert`, because the intent is more explicit.

### Why validation matters

Validation helps you:

- catch bad inputs early
- produce clearer error messages
- make functions more reliable
- prevent silent mistakes in analysis

---

## 7. Intro to Pandas for Function-Based Data Cleaning

Pandas is a Python library for working with tabular data.

```python
import pandas as pd
```

### Example DataFrame

```python
import pandas as pd

df = pd.DataFrame({
    "name": ["Ava", "Luis", "Mina", "Jordan"],
    "score": [95, None, 88, 91],
    "hours_studied": [10, 7, None, 8]
})

print(df)
```

### Example: Wrap Cleaning Logic in a Function

```python
def drop_missing_rows(df):
    return df.dropna()
```

### Example: Fill Missing Values

```python
def fill_missing_scores(df):
    df = df.copy()
    df["score"] = df["score"].fillna(df["score"].mean())
    return df
```

### Example: Add a Derived Column

```python
def add_pass_column(df):
    df = df.copy()
    df["passed"] = df["score"] >= 70
    return df
```

These are good early examples because they show how Pandas and functions work together.

---

## 8. Refactoring Repetitive Logic

One sign that you need a function is repeated code.

### Before Refactoring

```python
math_scores = [80, 90, 100]
science_scores = [75, 85, 95]

math_average = sum(math_scores) / len(math_scores)
science_average = sum(science_scores) / len(science_scores)
```

### After Refactoring

```python
def calculate_mean(values):
    return sum(values) / len(values)

math_average = calculate_mean(math_scores)
science_average = calculate_mean(science_scores)
```

The logic is now easier to maintain and reuse.

---

## 9. Git and GitHub

As your functions become more useful, save them like professional code.

```bash
git add .
git commit -m "Add reusable functions for data cleaning"
```

Version control helps you:

- track changes
- collaborate with others
- recover older versions
- build a professional workflow

---

## 10. Suggested In-Class Walkthrough

A good classroom sequence for this module:

1. Start with repeated code
2. Refactor it into a function
3. Add parameters and return values
4. Introduce lists and dictionaries as inputs
5. Add validation checks
6. Show the same ideas with a small Pandas DataFrame

This sequence keeps the lesson practical and connected.

---

## Practice Questions

- What problem do functions solve in programming?
- What is the difference between a parameter and an argument?
- Why is `return` usually more flexible than `print()` inside a function?
- When would you use a list instead of a dictionary?
- Why should we validate inputs inside a function?
- How does Pandas become more useful when wrapped inside reusable functions?

---

## Resources

- Python Functions Documentation
- Python Data Structures Documentation
- Pandas Documentation
- Real Python – Defining Your Own Python Function
- GitHub Documentation

---

## Teaching Notes

A few points worth emphasizing live:

- Beginners often confuse **printing** with **returning**
- Beginners often understand functions faster when they see repeated code first
- Dictionaries are usually easier to explain when framed as labeled records
- Pandas should be introduced here as a practical tool inside functions, not as the entire lesson
- For beginner instruction, explicit error checks with `raise` are often clearer than heavy use of `assert`

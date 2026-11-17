# Python Day 1 -- Learning Notes, Interview Questions & Coding Practice

## Topics Covered

This document reviews the topics discussed in the first Python session:

1.  Conditional statements: `if`, `if-else`, nested `if`
2.  Type conversion: `int()`, `float()`, `bool()`
3.  Truthy and falsy values
4.  Lists, indexing and slicing
5.  `range()`
6.  `for` loops and `while` loops
7.  `break`
8.  Nested loops
9.  A `while` loop inside a `for` loop

The aim is to understand how these concepts work, when to use them, and
how to combine them to solve practical problems.

------------------------------------------------------------------------

# Part 1 -- Learning Notes

## 1. Conditional Statements

Conditional statements allow a program to make decisions. Python checks
a condition and runs the matching block of code.

### 1.1 The `if` statement

An `if` statement runs a block only when its condition is `True`.

**Syntax**

``` python
if condition:
    # Statements to execute when the condition is True
```

**Example**

``` python
temperature = 32

if temperature > 30:
    print("It is a hot day")
```

The condition `temperature > 30` is true, so Python executes the
indented statement.

### 1.2 The `if-else` statement

Use `else` when you want one block to run if the condition is true and
another block to run if it is false.

**Syntax**

``` python
if condition:
    # Runs when the condition is True
else:
    # Runs when the condition is False
```

**Example**

``` python
available_seats = 0

if available_seats > 0:
    print("Seat available")
else:
    print("No seats available")
```

### 1.3 The `elif` statement

`elif` means "else if". It lets you check multiple conditions in order.

**Syntax**

``` python
if condition_1:
    # First option
elif condition_2:
    # Second option
elif condition_3:
    # Third option
else:
    # Runs when none of the conditions are True
```

**Example**

``` python
score = 82

if score >= 90:
    print("Excellent")
elif score >= 75:
    print("Good")
elif score >= 50:
    print("Needs improvement")
else:
    print("Below the required score")
```

Python checks the conditions from top to bottom. Once it finds a true
condition, it executes that block and skips the remaining branches.

### 1.4 Nested `if` statements

A nested `if` is an `if` statement placed inside another `if` or `else`
block. It is useful when one decision should be made only after another
condition is satisfied.

**Example**

``` python
age = 22
has_ticket = True

if age >= 18:
    if has_ticket:
        print("You can enter")
    else:
        print("Please purchase a ticket")
else:
    print("You do not meet the age requirement")
```

First, Python checks the age. It checks the ticket only when the age
condition is true.

### 1.5 Combining conditions

Logical operators let you combine conditions.

  ----------------------------------------------------------------------------
  Operator                Meaning                 Example
  ----------------------- ----------------------- ----------------------------
  `and`                   Both conditions must be `age >= 18 and has_ticket`
                          true                    

  `or`                    At least one condition  `is_weekend or is_holiday`
                          must be true            

  `not`                   Reverses a truth value  `not is_logged_in`
  ----------------------------------------------------------------------------

**Example**

``` python
age = 24
has_identity_card = True

if age >= 18 and has_identity_card:
    print("Verification successful")
else:
    print("Verification failed")
```

Use parentheses when they make a complex condition easier to read.

------------------------------------------------------------------------

## 2. Type Conversion

Type conversion means changing a value from one data type to another.

Python provides functions such as `int()`, `float()`, `str()` and
`bool()` for common conversions.

### 2.1 Integer conversion -- `int()`

`int()` converts a compatible value into an integer.

``` python
a = int("25")
b = int(8.9)

print(a)  # 25
print(b)  # 8
```

When converting a float to an integer, Python removes the decimal part.
It does not round the value to the nearest integer.

A string containing a decimal point cannot be directly converted using
`int()`:

``` python
# int("8.9")  # ValueError
```

Convert it to a float first if needed:

``` python
value = int(float("8.9"))
print(value)  # 8
```

### 2.2 Float conversion -- `float()`

`float()` converts a compatible value into a floating-point number.

``` python
price = float("149.50")
quantity = float(4)

print(price)     # 149.5
print(quantity)  # 4.0
```

### 2.3 Boolean conversion -- `bool()`

`bool()` converts a value to either `True` or `False`.

``` python
print(bool(1))       # True
print(bool(0))       # False
print(bool(-5))      # True
print(bool(10.5))    # True
print(bool(""))      # False
print(bool("Hello")) # True
```

### 2.4 Truthy and falsy values

In a condition, Python evaluates values as either truthy or falsy.

Common falsy values include:

-   `False`
-   `None`
-   `0`, `0.0` and other numeric zero values
-   An empty string: `""`
-   An empty list: `[]`
-   An empty tuple: `()`
-   An empty dictionary: `{}`
-   An empty set: `set()`

Most other values are truthy. For example, `1`, `-1`, `3.5` and
`"Python"` are truthy.

**Important distinction:**

-   `bool(0)` is `False`.
-   `bool(1)` is `True`.
-   `bool(-1)` is also `True`.
-   `bool("0")` is `True`, because `"0"` is a non-empty string.
-   `bool("False")` is `True`, because `"False"` is also a non-empty
    string.

A string is not interpreted as the Boolean word it contains. Python
checks whether the string is empty.

**Example:**

``` python
user_name = ""

if user_name:
    print("A name was provided")
else:
    print("The name is empty")
```

This is a useful way to check whether a string or collection contains
something.

### 2.5 A common input conversion issue

The `input()` function always returns a string.

``` python
age = input("Enter your age: ")
print(type(age))  # <class 'str'>
```

If you need to perform numerical comparisons or calculations, convert
the input:

``` python
age = int(input("Enter your age: "))

if age >= 18:
    print("Adult")
else:
    print("Minor")
```

**Be careful with this pattern:**

``` python
has_previous_record = bool(input("Do you have a previous record? "))
```

Typing `False` does not produce the Boolean value `False`. It produces
the string `"False"`, and that non-empty string converts to `True`.

For a yes/no question, compare the text explicitly:

``` python
answer = input("Do you have a previous record? ").strip().lower()
has_previous_record = answer == "yes"
```

------------------------------------------------------------------------

## 3. Lists

A list is an ordered, changeable collection of items. A list can contain
values of different data types and can contain duplicate values.

**Creating a list**

``` python
cities = ["Hyderabad", "Chennai", "Bengaluru"]
numbers = [10, 20, 30, 40]
mixed_values = ["Python", 25, 4.5, True]
```

### 3.1 Accessing list elements -- indexing

Indexing is used to access an individual element using its position.

Python uses zero-based indexing. This means the first element is at
index `0`.

``` python
languages = ["Python", "Java", "SQL", "JavaScript"]

print(languages[0])  # Python
print(languages[1])  # Java
print(languages[3])  # JavaScript
```

Negative indexing starts from the end:

``` python
print(languages[-1])  # JavaScript
print(languages[-2])  # SQL
```

### 3.2 List slicing

Slicing is used to access a portion of a list.

**Syntax**

``` python
list_name[start:stop:step]
```

-   `start`: Index where slicing begins; included.
-   `stop`: Index where slicing ends; excluded.
-   `step`: How many positions to move each time.

**Examples**

``` python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[1:4])   # [20, 30, 40]
print(numbers[:3])    # [10, 20, 30]
print(numbers[2:])    # [30, 40, 50, 60]
print(numbers[::2])   # [10, 30, 50]
print(numbers[::-1])  # [60, 50, 40, 30, 20, 10]
```

Remember that the stop index is excluded.

------------------------------------------------------------------------

## 4. The `range()` Function

`range()` represents a sequence of integers. It is commonly used when a
loop needs to repeat a known number of times.

**Syntax**

``` python
range(start, stop, step)
```

  Parameter   Description
  ----------- ---------------------------------------------
  `start`     Starting value; included. Defaults to `0`.
  `stop`      Ending boundary; excluded.
  `step`      Difference between values. Defaults to `1`.

**Examples**

``` python
range(5)          # 0, 1, 2, 3, 4
range(2, 7)       # 2, 3, 4, 5, 6
range(2, 11, 2)   # 2, 4, 6, 8, 10
range(10, 0, -1)  # 10 down to 1
```

A range object is not a list.

``` python
values = range(1, 6)

print(values)        # range(1, 6)
print(list(values))  # [1, 2, 3, 4, 5]
```

Use `list()` when you specifically need to create a list from the range.

------------------------------------------------------------------------

## 5. Loops

A loop repeats a block of code. Python provides `for` and `while` loops.

### 5.1 The `for` loop

A `for` loop visits the elements of an iterable, such as a list, string
or range.

**Syntax**

``` python
for item in iterable:
    # Statements to repeat
```

**Example -- Iterating over a list**

``` python
subjects = ["Python", "SQL", "Statistics"]

for subject in subjects:
    print(subject)
```

**Example -- Using `range()`**

``` python
for number in range(1, 6):
    print(number)
```

The loop takes each value from the iterable and assigns it to the loop
variable.

### 5.2 The `while` loop

A `while` loop repeats its block as long as its condition remains
`True`.

**Syntax**

``` python
while condition:
    # Statements to repeat
```

**Example**

``` python
attempt = 1

while attempt <= 3:
    print(f"Attempt number: {attempt}")
    attempt += 1
```

Make sure the condition can eventually become false. Otherwise, the loop
may run indefinitely.

### 5.3 `break` statement

`break` immediately terminates the nearest enclosing loop.

``` python
for number in range(1, 8):
    if number == 5:
        break
    print(number)
```

Output:

``` text
1
2
3
4
```

When the value reaches `5`, Python exits the loop.

------------------------------------------------------------------------

## 6. Nested Loops

A nested loop is a loop placed inside another loop.

For every iteration of the outer loop, the inner loop completes its
iterations, unless it is interrupted.

**Example -- Two `for` loops**

``` python
for row in range(1, 4):
    for column in range(1, 4):
        print(row, column)
```

The outer loop controls the row. The inner loop controls the column.

### 6.1 A `while` loop inside a `for` loop

Different types of loops can be combined when a problem requires it.

``` python
for student in range(1, 4):
    question = 1

    print(f"Student {student}")

    while question <= 2:
        print(f"  Question {question}")
        question += 1
```

Here:

-   The `for` loop moves through three students.
-   For each student, `question` is reset to `1`.
-   The `while` loop displays two questions for that student.
-   Once the `while` loop ends, the outer `for` loop moves to the next
    student.

This pattern is useful when one task must be repeated for each item, and
each item has its own repeated steps.

------------------------------------------------------------------------

# Part 2 -- Quick Revision Checklist

Use this checklist before moving to the next lesson.

-   [ ] Explain the difference between `if`, `if-else` and `elif`.
-   [ ] Explain when a nested `if` is useful.
-   [ ] Combine conditions using `and`, `or` and `not`.
-   [ ] Convert values using `int()`, `float()` and `bool()`.
-   [ ] Identify common truthy and falsy values.
-   [ ] Explain why `bool("False")` is `True`.
-   [ ] Create a list and access elements using positive and negative
    indexes.
-   [ ] Extract elements using list slicing.
-   [ ] Explain the `start`, `stop` and `step` parameters of `range()`.
-   [ ] Explain why `range()` is not a list.
-   [ ] Explain the difference between `for` and `while`.
-   [ ] Use `break` to stop a loop.
-   [ ] Trace the execution of nested loops.
-   [ ] Explain a `while` loop placed inside a `for` loop.

------------------------------------------------------------------------

# Part 3 -- Interview and Conceptual Questions

Try answering these in your own words. The goal is to explain the idea,
not just memorize a definition.

## A. Conditional Statements

1.  What is the purpose of conditional statements in Python?
2.  What is the difference between `if`, `elif` and `else`?
3.  Can we write an `if` statement without an `else` statement?
4.  What is a nested `if` statement? Give a practical example.
5.  What happens when multiple conditions in an `if-elif-else` chain are
    true?
6.  What is the difference between the logical operators `and` and `or`?
7.  What does the `not` operator do?
8.  Why is indentation important in Python conditional statements?

## B. Type Conversion and Boolean Values

9.  What is type conversion? Why is it required?
10. What is the difference between `int()` and `float()`?
11. What happens when we convert `8.9` into an integer using `int()`?
12. What does the `input()` function return by default?
13. Why should we convert user input before performing mathematical
    calculations?
14. What are truthy and falsy values?
15. Why does `bool(0)` return `False`, while `bool(1)` returns `True`?
16. What will be the output of `bool("False")`? Explain why.
17. What is the Boolean value of an empty list? What about a non-empty
    list?
18. What happens when we try to convert `"Python"` into an integer?

## C. Lists and Indexing

19. What is a list in Python?
20. Are lists mutable or immutable?
21. What is zero-based indexing?
22. What is negative indexing? Where is it useful?
23. What is the difference between indexing and slicing?
24. In `numbers[1:5]`, is index `5` included?
25. What does `numbers[::-1]` do?
26. What happens when we try to access a list using an index that does
    not exist?
27. What is the difference between `append()` and `insert()`?
28. What is the difference between `remove()` and `pop()`?

## D. Range and Loops

29. What is the purpose of the `range()` function?
30. What are the three parameters of `range()`?
31. Why is the stop value excluded in `range()`?
32. What is the difference between `range(5)` and `range(1, 5)`?
33. What does `range(10, 0, -2)` generate?
34. Does `range()` return a list?
35. What is the difference between a `for` loop and a `while` loop?
36. What can cause an infinite `while` loop?
37. What is a nested loop?
38. How many times does the inner loop execute when the outer loop
    completes one iteration?
39. Can we place a `while` loop inside a `for` loop?
40. What is the purpose of the `break` statement?
41. If `break` is placed inside a nested loop, which loop does it
    terminate?
42. Can a `for` loop iterate directly over a list without using
    `range()`?

------------------------------------------------------------------------

# Part 4 -- Predict the Output

Ask the learner to predict the output before running each program. This
helps develop execution-tracing skills.

## Question 1

``` python
x = 0

if x:
    print("A")
else:
    print("B")
```

## Question 2

``` python
value = "0"

if bool(value):
    print("Valid")
else:
    print("Invalid")
```

## Question 3

``` python
numbers = [10, 20, 30, 40, 50]

print(numbers[1:4])
print(numbers[-2])
print(numbers[::-1])
```

## Question 4

``` python
for i in range(2, 10, 3):
    print(i, end=" ")
```

## Question 5

``` python
count = 1

while count < 6:
    if count == 4:
        break

    print(count)
    count += 1
```

## Question 6

``` python
for i in range(1, 4):
    for j in range(1, 3):
        print(i, j)
```

## Question 7

``` python
for i in range(1, 4):
    j = 1

    while j <= 2:
        print(i, j)
        j += 1
```

## Question 8

``` python
numbers = [2, 4, 6]

for number in numbers:
    if number > 4:
        print("Found")
        break
else:
    print("Not found")
```

## Question 9

``` python
print(bool([]))
print(bool([0]))
print(bool(""))
print(bool(" "))
```

## Question 10

``` python
numbers = [10, 20, 30, 40, 50]

for i in range(len(numbers)):
    if i == 2:
        break

    print(numbers[i])
```

------------------------------------------------------------------------

# Part 5 -- Coding Practice Questions

These problems are designed to combine multiple concepts. They are
intentionally more practical than basic even/odd or prime-number
exercises.

For each problem, first ask the learner to explain the approach, then
write the code, and finally test it with different inputs.

## Level 1 -- Basic Application(Answers at last of the markdown)

### 1. Student Attendance Eligibility

Create a program that stores the total number of classes and the number
of classes attended.

Requirements:

-   Calculate the attendance percentage.
-   If attendance is at least 75%, display that the student is eligible.
-   Otherwise, display the shortage percentage.
-   If the student has attended more classes than the total classes
    conducted, display an invalid-data message.

**Concepts:** Lists or variables, conditions, type conversion and
arithmetic.



## Level 2 -- Logical Thinking(Answers at last of the markdown)

### 1. Online Login Attempt System

Create a basic login simulation.

Requirements:

-   Store a predefined username and password.
-   Give the user a maximum of three login attempts.
-   Ask for the username and password.
-   If both are correct, display a successful login message and stop.
-   Otherwise, display the number of attempts remaining.
-   After three unsuccessful attempts, display an account-locked
    message.

**Concepts:** `while` loop, conditions, type conversion where
appropriate and `break`.

------------------------------------------------------------------------

# **Python Coding Solutions – Beginner Level**

## **Level 1 – Basic Application**

### **1. Student Attendance Eligibility**

**Approach:**

1. Get the total number of classes.
2. Get the number of classes attended.
3. Check whether the entered data is valid.
4. Calculate the attendance percentage.
5. Check whether the student is eligible.

**Python Code:**

```
total_classes = int(input("Enter total number of classes: "))
attended_classes = int(input("Enter number of classes attended: "))

if attended_classes > total_classes or total_classes <= 0:
    print("Invalid Data")

else:
    attendance = (attended_classes / total_classes) * 100

    print(f"Attendance Percentage: {attendance:.2f}%")

    if attendance >= 75:
        print("Student is eligible for examinations")

    else:
        shortage = 75 - attendance
        print("Student is not eligible")
        print(f"Attendance shortage: {shortage:.2f}%")
```

**Sample Output:**

```
Enter total number of classes: 100
Enter number of classes attended: 80

Attendance Percentage: 80.00%
Student is eligible for examinations
```

**Concepts used:**

- Variables and `input()`
- Type conversion using `int()`
- Arithmetic operations
- Nested `if-else`
- Logical operators (`or`)
- f-strings

## **Level 2 – Logical Thinking**

### **1. Online Login Attempt System**

**Approach:**

1. Store a predefined username and password.
2. Initialize the number of attempts to zero.
3. Use a `while` loop to allow a maximum of three attempts.
4. Ask the user for their username and password.
5. Check whether both credentials match.
6. If correct, display a success message and use `break`.
7. Otherwise, display the remaining attempts.
8. If all three attempts fail, display an account-locked message.

**Python Code:**

```
correct_username = "admin"
correct_password = "python123"

attempts = 0
max_attempts = 3

while attempts < max_attempts:

    username = input("Enter username: ")
    password = input("Enter password: ")

    if username == correct_username and password == correct_password:
        print("Login Successful!")
        break

    else:
        attempts += 1

        remaining = max_attempts - attempts

        if remaining > 0:
            print("Invalid username or password")
            print(f"Attempts remaining: {remaining}")

        else:
            print("Account Locked!")
```

**Sample Output:**

```
Enter username: admin
Enter password: hello

Invalid username or password
Attempts remaining: 2

Enter username: admin
Enter password: test

Invalid username or password
Attempts remaining: 1

Enter username: admin
Enter password: python1234

Account Locked!
```

**Concepts used:**

- Variables
- `input()`
- String comparison
- `while` loop
- Logical operator (`and`)
- Nested `if-else`
- `break`
- Arithmetic operations

## **Additional Conceptual Questions**

After completing both programs, ask the learner:

1. Why do we use `and` in the login system instead of `or`?
2. Why do we initialize `attempts = 0`?
3. What happens if we remove the `break` statement?
4. Why do we check `total_classes <= 0`?
5. Why do we increment `attempts` only when the login fails?
6. Can we implement the login system using a `for` loop instead of a `while` loop?

------------------------------------------------------------------------

# Part 6 -- Suggested Practice Order

The learner does not need to solve all the questions in one sitting. Use
this order:

  Practice session   Questions
  ------------------ ----------------------------------------------
  Session 1          Predict the output questions
  Session 2          Shopping cart, attendance and salary summary
  Session 3          Ticket booking and expense analysis
  Session 4          Inventory and login attempt system
  Session 5          Seating arrangement and number patterns
  Session 6          Banking simulation and quiz application
  Session 7          Student performance report

------------------------------------------------------------------------

**End of Day 1 -- Python Fundamentals & Control Flow**

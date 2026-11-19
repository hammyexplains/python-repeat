# Python Learning Notes -- Smart Coding Techniques and Lists

## Topics Covered

1.  Multiple variable assignment
2.  Variable swapping
3.  Assigning the same value to multiple variables
4.  Ternary operator (conditional expression)
5.  Checking whether a list is empty
6.  Finding list length using `len()` and a loop
7.  Iterating using indexes or values
8.  Finding a list sum using `sum()` and a loop
9.  Sorting with `sorted()`
10. Finding maximum and minimum with `max()` and `min()`
11. `enumerate()`
12. `zip()`
13. List comprehension

------------------------------------------------------------------------

# Part 1 -- Topic Notes

## 1. Multiple Variable Assignment

Multiple variable assignment lets us assign values to more than one
variable in a single statement.

**Traditional approach**

``` python
name = "Alex"
age = 21
city = "Hyderabad"
```

**Python approach**

``` python
name, age, city = "Alex", 21, "Hyderabad"

print(name)
print(age)
print(city)
```

Python assigns each value to the variable in the corresponding position.

The number of variables and values should match:

``` python
a, b, c = 10, 20, 30
```

If the number does not match, Python raises a `ValueError`.

## 2. Variable Swapping

Variable swapping means exchanging the values stored in two variables.

**Traditional approach -- using a temporary variable**

``` python
a = 10
b = 20

temp = a
a = b
b = temp

print(a, b)
```

Output:

``` text
20 10
```

**Python approach -- multiple assignment**

``` python
a = 10
b = 20

a, b = b, a

print(a, b)
```

Output:

``` text
20 10
```

Python evaluates the values on the right-hand side first and then
assigns them to the variables on the left-hand side. This allows us to
swap values without a temporary variable.

## 3. Assigning the Same Value to Multiple Variables

Python allows us to assign the same value to multiple variables in one
statement.

``` python
a = b = c = 100

print(a)
print(b)
print(c)
```

Output:

``` text
100
100
100
```

**Note:** Be careful when using chained assignment with mutable objects
such as lists:

``` python
a = b = []
```

Both variables refer to the same list. Changing the list through `a`
also affects what you see through `b`.

------------------------------------------------------------------------

## 4. Ternary Operator -- Conditional Expression

A conditional expression is a short way to choose between two values
based on a condition. It is commonly called the ternary operator.

**Traditional `if-else` approach**

``` python
age = 20

if age >= 18:
    status = "Adult"
else:
    status = "Minor"

print(status)
```

**Shorter Python approach**

``` python
age = 20

status = "Adult" if age >= 18 else "Minor"

print(status)
```

**Syntax**

``` python
value_if_true if condition else value_if_false
```

Python checks the condition. If it is `True`, the expression returns the
first value; otherwise, it returns the value after `else`.

**Example -- Find the larger value**

``` python
a = 45
b = 70

largest = a if a > b else b

print(largest)
```

Use a conditional expression for a simple choice. If the logic becomes
complicated, a normal `if-else` statement is usually easier to read.

------------------------------------------------------------------------

## 5. Checking Whether a List Is Empty

An empty list contains no elements.

``` python
items = []
```

**Method 1 -- Using `len()`**

``` python
items = []

if len(items) == 0:
    print("The list is empty")
else:
    print("The list contains elements")
```

**Method 2 -- Using the list directly**

An empty list is falsy in Python. A non-empty list is truthy.

``` python
items = []

if not items:
    print("The list is empty")
else:
    print("The list contains elements")
```

This is the common Pythonic way to check whether a list is empty.

  List                  Boolean value
  --------------------- ---------------
  `[]`                  `False`
  `[10]`                `True`
  `["Python", "SQL"]`   `True`

------------------------------------------------------------------------

## 6. Finding the Length of a List

The length of a list is the total number of elements it contains.

**Method 1 -- Using `len()`**

``` python
numbers = [10, 20, 30, 40, 50]

count = len(numbers)

print("Number of elements:", count)
```

Output:

``` text
Number of elements: 5
```

**Method 2 -- Counting manually using a loop**

``` python
numbers = [10, 20, 30, 40, 50]

count = 0

for number in numbers:
    count += 1

print("Number of elements:", count)
```

Output:

``` text
Number of elements: 5
```

How it works:

1.  Set `count` to `0`.
2.  The loop visits each element.
3.  Increase `count` by `1` for every element.
4.  When the loop finishes, `count` contains the number of elements.

This manual approach helps us understand how counting works.

------------------------------------------------------------------------

## 7. Iterating Through a List -- Indexes vs Values

Consider this list:

``` python
languages = ["Python", "Java", "SQL", "JavaScript"]
```

**Method 1 -- Iterating directly over the list**

``` python
for language in languages:
    print(language)
```

The loop variable receives each element directly. Use this when you only
need the values.

**Method 2 -- Iterating using indexes with `range()`**

``` python
for i in range(len(languages)):
    print(languages[i])
```

How it works:

1.  `len(languages)` returns `4`.
2.  `range(4)` represents the index values `0, 1, 2, 3`.
3.  `i` receives each index.
4.  `languages[i]` accesses the element at that index.

Use this method when you need to work with element positions or update
elements by index.

**Example -- Updating elements using indexes**

``` python
numbers = [10, 20, 30]

for i in range(len(numbers)):
    numbers[i] = numbers[i] * 2

print(numbers)
```

Output:

``` text
[20, 40, 60]
```

  `for value in list`                 `for i in range(len(list))`
  ----------------------------------- ----------------------------------
  Iterates directly over elements     Iterates over index values
  Loop variable contains an element   Loop variable contains an index
  Best when only values are needed    Useful when positions are needed

------------------------------------------------------------------------

## 8. Finding the Sum of List Elements

The sum of a list is the total obtained by adding its numeric elements.

**Method 1 -- Using `sum()`**

``` python
numbers = [10, 20, 30, 40, 50]

total = sum(numbers)

print("Total:", total)
```

Output:

``` text
Total: 150
```

**Method 2 -- Finding the sum manually using a loop**

``` python
numbers = [10, 20, 30, 40, 50]

total = 0

for number in numbers:
    total += number

print("Total:", total)
```

Output:

``` text
Total: 150
```

How it works:

1.  Initialize `total` to `0`.
2.  Visit each element in the list.
3.  Add the current element to `total`.
4.  After the loop, `total` contains the sum.

Use `sum()` when you simply need the total. Use a loop when you need to
perform additional operations for each element or want to practise the
logic.

------------------------------------------------------------------------

## 9. Sorting a List -- `sorted()`

The `sorted()` function returns a new list containing the elements in
sorted order. It does not change the original list.

**Syntax**

``` python
sorted(iterable, reverse=False)
```

-   `iterable`: The collection to sort.
-   `reverse`: If `True`, sorts in descending order. The default is
    `False`.

**Ascending order**

``` python
numbers = [50, 10, 40, 20, 30]

result = sorted(numbers)

print(result)
```

Output:

``` text
[10, 20, 30, 40, 50]
```

**Descending order**

``` python
numbers = [50, 10, 40, 20, 30]

result = sorted(numbers, reverse=True)

print(result)
```

Output:

``` text
[50, 40, 30, 20, 10]
```

**Sorting strings**

``` python
names = ["Sam", "Alex", "John", "David"]

result = sorted(names)

print(result)
```

Output:

``` text
['Alex', 'David', 'John', 'Sam']
```

### `sorted()` vs `list.sort()`

  `sorted()`                        `list.sort()`
  --------------------------------- ----------------------------
  Returns a new sorted list         Sorts the original list
  Works with different iterables    List method; used on lists
  Original list remains unchanged   Original list is modified
  Can be assigned to a variable     Returns `None`

For this lesson, focus on `sorted()`.

------------------------------------------------------------------------

## 10. Finding the Maximum and Minimum

Python provides `max()` and `min()` to find the largest and smallest
elements in an iterable.

**`max()` -- returns the largest element**

``` python
marks = [78, 92, 65, 88, 95]

highest = max(marks)

print("Highest mark:", highest)
```

Output:

``` text
Highest mark: 95
```

**`min()` -- returns the smallest element**

``` python
marks = [78, 92, 65, 88, 95]

lowest = min(marks)

print("Lowest mark:", lowest)
```

Output:

``` text
Lowest mark: 65
```

**Using both together**

``` python
marks = [78, 92, 65, 88, 95]

print("Highest:", max(marks))
print("Lowest:", min(marks))
```

Calling `min()` or `max()` on an empty iterable raises a `ValueError`.

------------------------------------------------------------------------

## 11. The `enumerate()` Function

The `enumerate()` function allows us to iterate over an iterable while
getting both the index and the value.

It is useful when we need to know an element's position as well as the
element itself.

**Without `enumerate()`**

``` python
subjects = ["Python", "SQL", "Statistics"]

for i in range(len(subjects)):
    print(i, subjects[i])
```

**Using `enumerate()`**

``` python
subjects = ["Python", "SQL", "Statistics"]

for index, subject in enumerate(subjects):
    print(index, subject)
```

Output:

``` text
0 Python
1 SQL
2 Statistics
```

**Syntax**

``` python
enumerate(iterable, start=0)
```

-   `iterable`: The collection to iterate over.
-   `start`: The starting index. It defaults to `0`.

**Start counting from 1**

``` python
subjects = ["Python", "SQL", "Statistics"]

for index, subject in enumerate(subjects, start=1):
    print(index, subject)
```

Output:

``` text
1 Python
2 SQL
3 Statistics
```

Use `enumerate()` when you need both the index and the value. It is
usually cleaner than using `range(len(list))` for that purpose.

------------------------------------------------------------------------

## 12. The `zip()` Function

The `zip()` function combines elements from two or more iterables based
on their positions.

It is useful when related information is stored in separate lists and we
want to process corresponding elements together.

**Example**

``` python
names = ["Alex", "John", "Sam"]
marks = [90, 85, 95]

for name, mark in zip(names, marks):
    print(name, mark)
```

Output:

``` text
Alex 90
John 85
Sam 95
```

The first name is paired with the first mark, the second name with the
second mark, and so on.

**Syntax**

``` python
zip(iterable1, iterable2, ...)
```

**Combining three lists**

``` python
names = ["Alex", "John", "Sam"]
ages = [21, 22, 20]
cities = ["Hyderabad", "Bengaluru", "Chennai"]

for name, age, city in zip(names, ages, cities):
    print(name, age, city)
```

Output:

``` text
Alex 21 Hyderabad
John 22 Bengaluru
Sam 20 Chennai
```

**What if the lists have different lengths?**

By default, `zip()` stops when the shortest iterable runs out of
elements.

``` python
names = ["Alex", "John", "Sam"]
marks = [90, 85]

for name, mark in zip(names, marks):
    print(name, mark)
```

Output:

``` text
Alex 90
John 85
```

The remaining `"Sam"` is not included because there is no corresponding
mark.

------------------------------------------------------------------------

## 13. List Comprehension

List comprehension is a concise way to create a new list from an
existing iterable.

It allows us to write a loop and, optionally, a condition in a single
expression.

**Traditional approach**

``` python
squares = []

for number in range(1, 6):
    squares.append(number ** 2)

print(squares)
```

Output:

``` text
[1, 4, 9, 16, 25]
```

**Pythonic approach -- List comprehension**

``` python
squares = [number ** 2 for number in range(1, 6)]

print(squares)
```

Output:

``` text
[1, 4, 9, 16, 25]
```

**Syntax**

``` python
[expression for item in iterable]
```

### Example 1 -- Creating a list of even numbers

``` python
even_numbers = [number for number in range(1, 11) if number % 2 == 0]

print(even_numbers)
```

Output:

``` text
[2, 4, 6, 8, 10]
```

### Example 2 -- Converting names to uppercase

``` python
names = ["alex", "john", "sam"]

uppercase_names = [name.upper() for name in names]

print(uppercase_names)
```

Output:

``` text
['ALEX', 'JOHN', 'SAM']
```

### Example 3 -- Conditional expression inside list comprehension

This combines list comprehension with the ternary operator.

``` python
numbers = [1, 2, 3, 4, 5]

results = ["Even" if number % 2 == 0 else "Odd" for number in numbers]

print(results)
```

Output:

``` text
['Odd', 'Even', 'Odd', 'Even', 'Odd']
```

### Filtering vs conditional expression

**Filtering:** Keeps only elements that satisfy the condition.

``` python
numbers = [1, 2, 3, 4, 5]

even_numbers = [number for number in numbers if number % 2 == 0]

print(even_numbers)
```

Output:

``` text
[2, 4]
```

**Conditional expression:** Produces a result for every element,
choosing one value or another.

``` python
numbers = [1, 2, 3, 4, 5]

labels = ["Even" if number % 2 == 0 else "Odd" for number in numbers]

print(labels)
```

Output:

``` text
['Odd', 'Even', 'Odd', 'Even', 'Odd']
```

Use list comprehension for simple transformations and filtering. For
complicated logic, a regular loop may be easier to read.

------------------------------------------------------------------------

# Part 2 -- Quick Comparison Table

  -------------------------------------------------------------------------------------
  Topic                   What it does            Example
  ----------------------- ----------------------- -------------------------------------
  Multiple assignment     Assigns multiple values `a, b = 10, 20`
                          together                

  Variable swapping       Exchanges values        `a, b = b, a`

  Chained assignment      Assigns the same value  `a = b = c = 100`
                          to multiple variables   

  Ternary expression      Chooses between two     `"Adult" if age >= 18 else "Minor"`
                          values                  

  `len()`                 Returns the number of   `len(numbers)`
                          elements                

  `sum()`                 Returns the total       `sum(numbers)`

  `sorted()`              Returns a new sorted    `sorted(numbers)`
                          list                    

  `max()`                 Returns the largest     `max(numbers)`
                          element                 

  `min()`                 Returns the smallest    `min(numbers)`
                          element                 

  `enumerate()`           Provides index and      `enumerate(names)`
                          value                   

  `zip()`                 Combines corresponding  `zip(names, marks)`
                          elements                

  List comprehension      Creates a list          `[x * 2 for x in numbers]`
                          concisely               
  -------------------------------------------------------------------------------------

------------------------------------------------------------------------

# Part 3 -- Interview and Conceptual Questions

Try to answer these in your own words. Focus on understanding the
concept and explaining why a particular approach is useful.

## A. Assignment and Conditional Expressions

1.  What is multiple variable assignment in Python?
2.  How can we assign three different values to three variables in a
    single statement?
3.  How can we swap two variables without using a temporary variable?
4.  What happens when we write `a, b = b, a`?
5.  What is chained assignment? Give an example.
6.  What is the difference between `a, b = 10, 20` and `a = b = 10`?
7.  What is a ternary operator in Python?
8.  What is the general syntax of a conditional expression?
9.  When should we prefer a normal `if-else` statement over a ternary
    expression?

## B. Lists and Iteration

10. What is the purpose of the `len()` function?
11. How can you find the length of a list without using `len()`?
12. What is the difference between iterating directly over a list and
    iterating using `range(len(list))`?
13. When would you use `range(len(list))` instead of
    `for value in list`?
14. How can you update list elements using their indexes?
15. What is the difference between an index and an element?
16. How can you check whether a list is empty?
17. Why does `if not items` work for checking an empty list?
18. What is the difference between `len(items) == 0` and `not items`?

## C. Built-in Functions

19. What is the purpose of the `sum()` function?
20. How can you calculate the sum of list elements without using
    `sum()`?
21. What is the difference between `sorted()` and `list.sort()`?
22. Does `sorted()` modify the original list?
23. What does the `reverse` parameter in `sorted()` do?
24. What is the purpose of `max()` and `min()`?
25. What happens if we call `max()` on an empty list?

## D. `enumerate()` and `zip()`

26. What is the purpose of the `enumerate()` function?
27. What does `enumerate()` provide while iterating?
28. How can we start enumeration from index `1` instead of `0`?
29. What is the difference between `enumerate()` and `range(len(list))`?
30. What is the purpose of the `zip()` function?
31. How does `zip()` combine two lists?
32. What happens if the iterables passed to `zip()` have different
    lengths?
33. Can we use `zip()` with three or more lists?

## E. List Comprehension

34. What is list comprehension?
35. What is the general syntax of list comprehension?
36. How is list comprehension different from a regular `for` loop?
37. How can we create a list of squares using list comprehension?
38. How can we filter even numbers using list comprehension?
39. What is the difference between filtering with `if` and using
    `if-else` inside list comprehension?
40. When should we avoid using list comprehension?

------------------------------------------------------------------------

# Part 4 -- Predict the Output

Predict the output before executing each program.

## Question 1 -- Multiple Assignment

``` python
a, b, c = 10, 20, 30

a, b = b, c

print(a, b, c)
```

## Question 2 -- Variable Swapping

``` python
a = 5
b = 15

a, b = b, a

print(a)
print(b)
```

## Question 3 -- Chained Assignment

``` python
a = b = c = 50

b = 100

print(a, b, c)
```

## Question 4 -- Ternary Expression

``` python
age = 17

result = "Adult" if age >= 18 else "Minor"

print(result)
```

## Question 5 -- Empty List

``` python
items = [0]

if not items:
    print("Empty")
else:
    print("Not Empty")
```

## Question 6 -- Manual Length

``` python
numbers = [10, 20, 30, 40]

count = 0

for number in numbers:
    count += 1

print(count)
```

## Question 7 -- Index vs Value

``` python
numbers = [10, 20, 30]

for i in range(len(numbers)):
    print(i, numbers[i])
```

## Question 8 -- Manual Sum

``` python
numbers = [5, 10, 15]

total = 0

for number in numbers:
    total += number

print(total)
```

## Question 9 -- Sorting

``` python
numbers = [40, 10, 30, 20]

result = sorted(numbers, reverse=True)

print(result)
print(numbers)
```

## Question 10 -- `enumerate()`

``` python
names = ["Alex", "John", "Sam"]

for index, name in enumerate(names, start=1):
    print(index, name)
```

## Question 11 -- `zip()`

``` python
names = ["Alex", "John", "Sam"]
marks = [80, 90]

for name, mark in zip(names, marks):
    print(name, mark)
```

## Question 12 -- List Comprehension

``` python
numbers = [1, 2, 3, 4, 5, 6]

result = [number * 2 for number in numbers if number > 3]

print(result)
```

------------------------------------------------------------------------

# Part 5 -- Coding Practice Problems

These problems apply the concepts covered in this lesson. They focus on
practical situations and logical thinking rather than only basic
number-checking exercises.

## Level 1 -- Basic Application

### 1. Employee Salary Analysis

You are given a list containing the monthly salaries of employees.

``` python
salaries = [25000, 35000, 42000, 18000, 50000, 30000]
```

Requirements:

-   Find the total salary expenditure.
-   Calculate the average salary.
-   Find the highest and lowest salaries.
-   Display the salaries in ascending order.
-   Display the salaries in descending order.

**Concepts:** `sum()`, `len()`, `max()`, `min()`, `sorted()`.

### 2. Student Marks Report

You are given the marks obtained by a student in six subjects.

``` python
marks = [85, 92, 78, 65, 88, 95]
```

Requirements:

-   Calculate the total marks.
-   Calculate the average marks.
-   Find the highest and lowest marks.
-   Display the marks in descending order.
-   Check whether the student has scored at least 75 in every subject.

**Concepts:** Lists, built-in functions, loops and conditions.

### 3. Product Price Update

You are given a list of product prices.

``` python
prices = [100, 250, 400, 150, 500]
```

Requirements:

-   Create a new list containing prices after applying a 10% discount.
-   Do not modify the original list.
-   Display both the original and discounted prices.

**Concepts:** List comprehension, multiple assignment and arithmetic
operations.

### 4. Customer Name Display

You are given a list of customer names.

``` python
customers = ["Alex", "John", "Sam", "David", "Robert"]
```

Requirements:

-   Display every customer along with their position.
-   Start the position numbering from 1.
-   Display the total number of customers.

**Concepts:** `enumerate()` and `len()`.

------------------------------------------------------------------------

## Level 2 -- Logical Thinking

### 5. Product Inventory Report

You are given two lists containing product names and their corresponding
stock quantities.

``` python
products = ["Laptop", "Mouse", "Keyboard", "Monitor"]
quantities = [5, 25, 12, 3]
```

Requirements:

-   Display each product with its corresponding quantity.
-   Find the product with the lowest stock.
-   Display products whose stock is below 10.
-   Calculate the total number of items in stock.

**Concepts:** `zip()`, `min()`, loops, conditions and `sum()`.

### 6. Weekly Expense Analysis

You are given the daily expenses for one week.

``` python
expenses = [250, 400, 150, 600, 350, 500, 300]
```

Requirements:

-   Calculate the total weekly expense.
-   Find the average daily expense.
-   Identify the highest and lowest daily expenses.
-   Display the expenses in reverse order.
-   Create a new list containing only expenses above the average.

**Concepts:** `sum()`, `len()`, `max()`, `min()`, slicing and list
comprehension.

### 7. Student Ranking System

You are given student names and their corresponding marks.

``` python
students = ["Alex", "John", "Sam", "David", "Robert"]
marks = [85, 95, 78, 90, 88]
```

Requirements:

-   Display every student with their marks.
-   Sort the marks in descending order.
-   Find the highest-scoring student.
-   Display the students who scored above 85.

**Concepts:** `zip()`, `max()`, `sorted()`, `enumerate()` and
conditions.

### 8. Data Filtering System

You are given a list containing different numerical values.

``` python
numbers = [12, 45, 8, 67, 23, 90, 34, 5, 72]
```

Requirements:

-   Create a list containing numbers greater than 30.
-   Create another list containing numbers less than or equal to 30.
-   Create a list containing the squares of all the numbers.
-   Display the largest and smallest values.

**Concepts:** List comprehension, conditions, `max()` and `min()`.

------------------------------------------------------------------------

## Level 3 -- Challenging Problems

### 9. E-commerce Order Summary

You are given three lists containing customer names, product names and
order amounts.

``` python
customers = ["Alex", "John", "Sam", "David", "Robert"]
products = ["Laptop", "Mobile", "Keyboard", "Monitor", "Mouse"]
amounts = [55000, 25000, 1500, 12000, 800]
```

Requirements:

-   Display each customer's name, product and order amount.
-   Calculate the total revenue.
-   Find the highest order amount.
-   Identify the customer who placed the highest-value order.
-   Display all orders above ₹10,000.
-   Display the orders sorted by amount in ascending order.

**Concepts:** `zip()`, `max()`, `sum()`, `sorted()` and loops.

### 10. Top Performer Identification

You are given student names and their examination scores.

``` python
students = ["Alex", "John", "Sam", "David", "Robert", "Mike"]
scores = [78, 95, 88, 95, 72, 90]
```

Requirements:

-   Display each student's name and score.
-   Find the highest score.
-   Display every student who achieved the highest score.
-   Sort the scores in descending order.
-   Display students whose scores are greater than or equal to 85.

**Concepts:** `zip()`, `max()`, `sorted()`, loops and conditions.

### 11. Transaction Analysis

You are given a list containing transaction amounts.

``` python
transactions = [500, -200, 1500, -300, 800, -100, 2000]
```

Positive values represent deposits, while negative values represent
withdrawals.

Requirements:

-   Calculate the total deposits.
-   Calculate the total withdrawals as a positive amount.
-   Calculate the final net transaction amount.
-   Find the largest deposit.
-   Find the largest withdrawal by amount.
-   Create separate lists for deposits and withdrawals.

**Concepts:** Loops, conditions, `sum()`, `max()` and list
comprehension.

### 12. Compare Two Teams

Two teams participated in a competition. Their scores are stored in
separate lists.

``` python
team_a = [85, 90, 78, 95, 88]
team_b = [80, 92, 75, 89, 91]
```

Requirements:

-   Compare the scores at each corresponding position.
-   Display which team scored higher in each round.
-   Calculate the total score of each team.
-   Identify the overall winning team.
-   Display the score differences between the teams in each round.

**Concepts:** `zip()`, loops, conditions, `sum()` and list
comprehension.

------------------------------------------------------------------------

# Part 6 -- Recommended Practice Order

  Session   Topics to practise
  --------- -------------------------------------------------------
  1         Multiple assignment, swapping and ternary expressions
  2         Empty-list checks, `len()` and manual counting
  3         Direct list iteration vs index-based iteration
  4         `sum()`, manual summation, `max()` and `min()`
  5         `sorted()` and sorting applications
  6         `enumerate()` and `zip()`
  7         List comprehension
  8         Combined practical problems

## Learner Self-Assessment

Before moving to the next lesson, the learner should be able to:

-   [ ] Assign multiple values to multiple variables in one statement.
-   [ ] Swap two variables without a temporary variable.
-   [ ] Assign the same value to multiple variables.
-   [ ] Write a simple conditional expression.
-   [ ] Check whether a list is empty.
-   [ ] Find list length using `len()` and manually using a loop.
-   [ ] Explain direct iteration vs index-based iteration.
-   [ ] Calculate a list's sum using `sum()` and a loop.
-   [ ] Sort a list using `sorted()`.
-   [ ] Find the largest and smallest elements.
-   [ ] Iterate with both index and value using `enumerate()`.
-   [ ] Combine multiple lists using `zip()`.
-   [ ] Create and filter lists using list comprehension.

------------------------------------------------------------------------

**End of Lesson -- Python Smart Coding Techniques and List Operations**

# QHO444 – Programming in Practice (Python)
## Week 5 Seminar: Lists, Tuples and Nested Data Structures

**Level:** BSc Computing, Year 1  
**Working folder:** `week5/`  
**Tools:** Python 3, PyCharm (or another Python editor), Git and GitHub  
**Aim:** Understand how Python stores collections of data and practise solving navigation and falling-tile problems.

> **How to use this guide:** Read the concept examples first. Then complete Activities 1–7 in order, typing and running your own code. Each activity has a task checklist, sample output and an expandable reference solution. Try the activity before opening its solution.

---

## Learning outcomes

By the end of the seminar, you should be able to:

1. Create and change a **list** using `[]`, `append()` and indexing.
2. Use loops to display or collect list items.
3. Create a **tuple** using `()` and explain why it is immutable.
4. Return lists, individual values and tuples from functions.
5. Store tuples inside a list, then classify their values using `if` statements.
6. Save and push your work to GitHub.

## Recommended seminar sequence

| Part | Topic | Suggested time |
|---|---|---:|
| 1 | Concepts and short demonstrations | 20 min |
| 2 | List Activities 1–2 | 20 min |
| 3 | List Activities 3–4 | 25 min |
| 4 | Tuple Activities 1–2 | 20 min |
| 5 | Nested tuples Activity 3 | 20 min |
| 6 | GitHub checks and recap | 15 min |

The times are a suggested teaching plan, not a requirement of the original activity sheet.

---

# Part A – Concepts first

## 1. From one value to a collection

A **variable** can hold a value:

```python
student = "Alex"
score = 78
```

But a university application might need to store many student scores. Instead of creating `score1`, `score2`, `score3` and so on, place values in a **data structure**:

```python
scores = [78, 82, 69, 91]
print(scores)
```

**Real-world connection:** A shopping basket contains several products; a game route contains several movements; a weather station records several temperatures. Lists and tuples help us keep related values together.

Python also offers dictionaries and sets, but this seminar concentrates on the **ordered** data structures **lists** and **tuples**.

## 2. Lists: a shopping basket you can change

A list uses **square brackets** and is **mutable**, meaning items can be added, removed or replaced.

```python
basket = ["apple", "banana", "cherry"]

basket.append("orange")    # Add a new item at the end
basket[1] = "blueberry"     # Replace the item at index 1
basket.remove("cherry")    # Remove the first matching item

print(basket)
# ['apple', 'blueberry', 'orange']
```

### Indexing begins at zero

```text
Index       0          1          2
          ┌──────────┬──────────┬──────────┐
List      │  apple   │  banana  │  cherry  │
          └──────────┴──────────┴──────────┘
```

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])   # apple
print(fruits[2])   # cherry
```

**Ask yourself:** What index accesses `"banana"`? **Answer:** `1`.

Common list operations:

| Operation | Meaning | Example |
|---|---|---|
| `append(x)` | Add to the end | `fruits.append("pear")` |
| `remove(x)` | Remove first matching value | `fruits.remove("apple")` |
| `del items[i]` | Delete by index | `del fruits[0]` |
| `len(items)` | Number of items | `len(fruits)` |
| `items[i]` | Read an item | `fruits[0]` |
| `items[i] = x` | Change an item | `fruits[0] = "pear"` |

### Lists may contain different data types

```python
movement = ["Move Forward", 10, "Turn Left", 3]
```

The text is the instruction; the following integer gives the number of steps.

## 3. Iterating through lists

**Iterating** means visiting items one after another.

```python
directions = ["North", "South", "East"]

for direction in directions:
    print(direction)
```

If you also need each item's position:

```python
for index in range(len(directions)):
    print(f"{index}: {directions[index]}")
```

**Real-world connection:** A satnav reads the next instruction in a planned route. A menu displays each option and its number.

## 4. Functions: reusable blocks of instructions

Functions help us separate jobs. One function can **prepare the data**; another can **use and display it**.

```python
def directions():
    return ["Move Forward", "Turn Left"]


def show_route():
    route = directions()
    print(route)


if __name__ == "__main__":
    show_route()
```

**Key ideas:**

- `def` defines the function.
- `return` sends a value back to the code that called the function.
- `route = directions()` stores that returned value.
- `if __name__ == "__main__":` runs the entry-point function when the file is executed directly, rather than imported by another file.

**Analogy:** One team member prepares a parcel (`return`); another receives it and decides what to do next.

## 5. Tuples: a collection whose entries cannot be reassigned

A tuple is **ordered**, **indexed** and **immutable**. You can read its elements, but you cannot directly replace, append or remove its entries.

```python
person = ("Bob", 40, "Lecturer")
print(person[0])  # Bob
```

```python
temperatures = (19, 23, 21, 21, 20, 18, 22)

print(min(temperatures))       # 18
print(max(temperatures))       # 23
print(20 in temperatures)      # True
print(temperatures + (20, 21)) # A NEW tuple
print(temperatures * 2)       # A NEW repeated tuple
```

Attempting `temperatures[0] = 25` causes a `TypeError` because tuple elements cannot be reassigned.

**Real-world connection:** Consider a fixed GPS coordinate pair `(latitude, longitude)` or a fixed configuration record that should not accidentally be modified. A tuple can communicate that the group of values is intended to stay together.

| List | Tuple |
|---|---|
| `[]` | `()` (or comma-separated values) |
| Mutable | Immutable |
| Has `append()` and `remove()` | No `append()` or `remove()` |
| Indexed and ordered | Indexed and ordered |
| Example: editable shopping basket | Example: fixed coordinate pair |

**Technical note:** A tuple cannot have its elements reassigned, but if one element is itself a mutable list, that nested list can still change.

## 6. Returning two values from a function

A function can return two values as a tuple:

```python
def lowest_and_highest():
    return (4, 99)

result = lowest_and_highest()
print(result[0])  # 4
print(result[1])  # 99
```

You can also **unpack** the tuple:

```python
minimum, maximum = lowest_and_highest()
print(minimum, maximum)
```

## 7. Nested data: a list of tuples

A **list of tuples** is useful when each item contains a pair of related values.

```python
steps = [
    ("step 1", 50),
    ("step 2", 38),
    ("step 3", 27),
]
```

```text
OUTER LIST
  index 0  ──► ("step 1", 50)
                    │        │
                    ▼        ▼
                  name      risk (%)
  index 1  ──► ("step 2", 38)
  index 2  ──► ("step 3", 27)
```

To read the second element of the first tuple:

```python
print(steps[0][1])  # 50
```

To inspect every pair:

```python
for name, risk in steps:
    print(f"{name}: {risk}%")
```

**Game connection:** Each tuple represents a falling tile and its chance of falling. The list stores all the tiles that the player must consider.

---

# Part B – Practical activities

## Initial setup

1. Open your existing module Git repository in PyCharm.
2. Create a folder named **`week5`** in the project root if it does not already exist.
3. Create the files below as you reach the relevant activities:

```text
project-root/
└── week5/
    ├── list_tasks.py
    └── tuple_tasks.py
```

4. After each completed activity, **run the relevant `run_task...()` function**, compare with the expected output, then commit the code.
5. Keep previous functions in each file; do not overwrite an earlier solution when moving to the next activity.

**Important:** Because both files use function names such as `run_task1`, this is not a problem; they are in separate Python files. In each file, change the entry-point call to the activity you want to test.

---

# Section 1 – Lists: Maze navigation

## Activity 1 – Simple List

**Scenario:** A robot needs a collection of possible movements to navigate a maze.

**Your task**

1. In `week5/`, create **`list_tasks.py`**.
2. Define a function called `directions()` with no parameters.
3. Inside it, create a list named `steps` containing exactly:
   - `"Move Forward"`
   - `"Move Backward"`
   - `"Turn Left"`
   - `"Turn Right"`
4. Return the list.
5. Define `run_task1()` with no parameters.
6. Call `directions()` inside `run_task1()` and print the returned list.
7. Add the `if __name__ == "__main__":` entry point to run the function.
8. Run the file and check the output.

**Expected output**

```text
['Move Forward', 'Move Backward', 'Turn Left', 'Turn Right']
```

**Think:** Why is a list better than four unrelated variables here?

<details>
<summary><strong>Show reference solution and explanation</strong></summary>

```python
# Return all available maze directions.
def directions():
    steps = ["Move Forward", "Move Backward", "Turn Left", "Turn Right"]
    return steps


# Display the list of directions.
def run_task1():
    available = directions()
    print(available)


if __name__ == "__main__":
    run_task1()
```

**Explanation:** `directions()` builds and returns the list. `run_task1()` receives and prints it. The list keeps the four directions together in order.

</details>

**Commit example:** `git commit -m "Added code to demonstrate a simple list"`

---

## Activity 2 – Indexing

**Scenario:** The maze robot needs both a movement direction and the number of steps for that movement.

**Your task**

1. Continue using **`list_tasks.py`**.
2. Create `movements()` with no parameters.
3. Create a list named `path` containing exactly:

```python
["Move Forward", 10, "Move Backward", 5,
 "Move Left", 3, "Move Right", 1]
```

4. Return `path`.
5. Define `run_task2()`.
6. Display `Moving...`.
7. Call `movements()` and store its returned list.
8. Read the list in pairs: position `0` with `1`, then `2` with `3`, etc.
9. Print each pair as `{direction} for {steps} steps`.
10. Change the bottom entry point to call `run_task2()` and run the file.

**Expected output**

```text
Moving...
Move Forward for 10 steps
Move Backward for 5 steps
Move Left for 3 steps
Move Right for 1 steps
```

**Hint:** `range(0, len(path), 2)` gives the starting index of each pair. Use `path[index]` and `path[index + 1]`.

<details>
<summary><strong>Show reference solution and explanation</strong></summary>

```python
# Return alternating directions and step counts.
def movements():
    path = ["Move Forward", 10, "Move Backward", 5,
            "Move Left", 3, "Move Right", 1]
    return path


def run_task2():
    print("Moving...")
    route = movements()

    # Advance two positions at a time: direction, then count.
    for index in range(0, len(route), 2):
        direction = route[index]
        steps = route[index + 1]
        print(f"{direction} for {steps} steps")


if __name__ == "__main__":
    run_task2()
```

**Explanation:** The direction is at each even index (`0, 2, 4, 6`), and the associated step count is at the following odd index (`1, 3, 5, 7`). This is a useful stepping stone before learning tuples.

</details>

**Commit example:** `git commit -m "Added code to demonstrate list indexing"`

---

## Activity 3 – Iterate

**Scenario:** Display a numbered movement menu so that the robot operator can see the available choices.

**Your task**

1. Keep the `directions()` function from Activity 1.
2. Define a new function `menu()` with no parameters.
3. Display `Please select a direction:`.
4. Call `directions()` and store its returned list.
5. Loop through each index and print `{index}: {direction}`.
6. Define `run_task3()` to call `menu()`.
7. Change the entry point to call `run_task3()` and run the program.

**Expected output**

```text
Please select a direction:
0: Move Forward
1: Move Backward
2: Turn Left
3: Turn Right
```

**Think:** Why do menu numbers start at `0`? Because Python list indices start at zero.

<details>
<summary><strong>Show reference solution and explanation</strong></summary>

```python
# Keep directions() from Activity 1.
def directions():
    return ["Move Forward", "Move Backward", "Turn Left", "Turn Right"]


def menu():
    print("Please select a direction:")
    available = directions()

    # Print each direction with its index.
    for index in range(len(available)):
        print(f"{index}: {available[index]}")


def run_task3():
    menu()


if __name__ == "__main__":
    run_task3()
```

**Explanation:** `range(len(available))` produces index values `0` through `3`. Each index retrieves the matching direction from the list.

</details>

**Commit example:** `git commit -m "Added code to iterate through a list"`

---

## Activity 4 – Populate a List

**Scenario:** Let the operator choose five moves, then build a complete escape route.

**Your task**

1. Keep `directions()` from Activity 1.
2. Define `menu_and_input()` with no parameters.
3. Display `Please select a direction:` and the numbered direction menu.
4. Ask the user to enter the menu index using `input()`.
5. Convert the response to `int` and return the corresponding direction.
6. Define `run_task4()`.
7. Create an empty list named `route`.
8. Display `Working out escape route...`.
9. Use a loop that repeats **five times**.
10. Each time, call `menu_and_input()` and `append()` its returned direction to `route`.
11. Print `Escape route: {route}`.
12. Change the entry point to `run_task4()` and run the file.

**Example user selections:** `0`, `0`, `2`, `0`, `3`.

**Expected final output**

```text
Escape route: ['Move Forward', 'Move Forward', 'Turn Left', 'Move Forward', 'Turn Right']
```

**Hint:** You will need `route.append(menu_and_input())` inside the loop.

<details>
<summary><strong>Show reference solution and explanation</strong></summary>

```python
def directions():
    return ["Move Forward", "Move Backward", "Turn Left", "Turn Right"]


def menu_and_input():
    print("Please select a direction:")
    available = directions()

    for index in range(len(available)):
        print(f"{index}: {available[index]}")

    choice = int(input("Enter a menu number (0-3): "))
    return available[choice]


def run_task4():
    route = []
    print("Working out escape route...")

    # Ask for five movements and store them.
    for count in range(5):
        next_direction = menu_and_input()
        route.append(next_direction)

    print(f"Escape route: {route}")


if __name__ == "__main__":
    run_task4()
```

**Explanation:** The empty list grows by one element after each menu selection. After five iterations, the list holds the complete route. The core activity assumes the user enters a valid index `0–3`.

**Optional challenge:** Add a `while` loop and `try/except` so incorrect numbers or text input do not crash the program. This is an extension, not part of the required task.

</details>

**Commit example:** `git commit -m "Added code to populate an escape route list"`

---

# Section 2 – Tuples: Falling-tile puzzle

A platform game contains five tiles, each with a **likelihood of falling**. We want to use tuples to work out the lowest and highest risks and classify the tiles.

## Activity 5 – Simple Tuple (Tuple Task 1)

**Your task**

1. Create **`week5/tuple_tasks.py`**.
2. Define a function `likelihood()` with no parameters.
3. Create a tuple named `likelihoods` containing exactly `(50, 38, 27, 99, 4)`.
4. Use `min()` to find the smallest value.
5. Return that value.
6. Define `run_task1()` with no parameters.
7. Call `likelihood()` and store its returned result in a local variable.
8. Display `Minimum likelihood of falling: {value}%`.
9. Add an entry point to call `run_task1()` and run the file.

**Expected output**

```text
Minimum likelihood of falling: 4%
```

**Question:** Is `4` the index of the safest tile? **No.** It is the *likelihood value*. The corresponding tile is fifth in the sequence (index `4`).

<details>
<summary><strong>Show reference solution and explanation</strong></summary>

```python
# Return the lowest falling likelihood.
def likelihood():
    likelihoods = (50, 38, 27, 99, 4)
    return min(likelihoods)


def run_task1():
    minimum = likelihood()
    print(f"Minimum likelihood of falling: {minimum}%")


if __name__ == "__main__":
    run_task1()
```

**Explanation:** `min()` reads all values and returns the smallest number, `4`. The tuple itself is not changed.

</details>

**Commit example:** `git commit -m "Added code to demonstrate a simple tuple"`

---

## Activity 6 – Returning a Tuple (Tuple Task 2)

**Scenario:** The player wants to know the safest and riskiest tile likelihoods.

**Your task**

1. Continue in `tuple_tasks.py`.
2. Define `likelihood_min_max()` with no parameters.
3. Create the same `likelihoods = (50, 38, 27, 99, 4)` tuple.
4. Find the minimum and maximum with `min()` and `max()`.
5. Return both values **together as a tuple**.
6. Define `run_task2()` to call that function and store the returned tuple.
7. Print its minimum and maximum values on separate lines.
8. Change the entry point to run `run_task2()`.

**Expected output**

```text
Minimum likelihood of falling: 4%
Maximum likelihood of falling: 99%
```

**Hint:** `return (min(likelihoods), max(likelihoods))`.

<details>
<summary><strong>Show reference solution and explanation</strong></summary>

```python
# Return a tuple containing the minimum and maximum risks.
def likelihood_min_max():
    likelihoods = (50, 38, 27, 99, 4)
    return (min(likelihoods), max(likelihoods))


def run_task2():
    result = likelihood_min_max()
    print(f"Minimum likelihood of falling: {result[0]}%")
    print(f"Maximum likelihood of falling: {result[1]}%")


if __name__ == "__main__":
    run_task2()
```

**Explanation:** The returned tuple is `(4, 99)`. Index `0` is the minimum, and index `1` is the maximum.

**Alternative (tuple unpacking):**

```python
minimum, maximum = likelihood_min_max()
```

</details>

**Commit example:** `git commit -m "Added code to return a tuple from a function"`

---

## Activity 7 – Nested Tuples: Classify Safe and Unsafe Steps (Tuple Task 3)

**Scenario:** Each tile has a label and a chance of falling. A likelihood **50 or greater** puts it into `bad_steps`; otherwise, it belongs in `good_steps`.

**Your task**

1. Continue in `tuple_tasks.py`.
2. Define a function `steps()` with no parameters.
3. Create a **list of tuples** named `likelihoods` with these exact entries:

```python
[
    ("step 1", 50),
    ("step 2", 38),
    ("step 3", 27),
    ("step 4", 99),
    ("step 5", 4),
]
```

4. Return that list.
5. Define `run_task3()` with no parameters.
6. Call `steps()` and store the result locally.
7. Create two empty lists: `good_steps = []` and `bad_steps = []`.
8. Loop through each `(name, likelihood)` pair.
9. If the likelihood is **`>= 50`**, append the full tuple to `bad_steps`.
10. Otherwise, append the full tuple to `good_steps`.
11. Print the numbers of entries using `len()`.
12. Change the entry point to call `run_task3()` and run the file.

### Visual classification

```text
INPUT:  List of (step name, falling likelihood)

("step 1", 50) ───► 50 >= 50? YES ───► BAD
("step 2", 38) ───► 38 >= 50? NO  ───► GOOD
("step 3", 27) ───► 27 >= 50? NO  ───► GOOD
("step 4", 99) ───► 99 >= 50? YES ───► BAD
("step 5",  4) ───►  4 >= 50? NO  ───► GOOD

GOOD: 3 steps                 BAD: 2 steps
```

**Expected output**

```text
Good steps: 3, Bad steps: 2
```

<details>
<summary><strong>Show reference solution and explanation</strong></summary>

```python
# Return the names and falling likelihoods of five tiles.
def steps():
    likelihoods = [
        ("step 1", 50),
        ("step 2", 38),
        ("step 3", 27),
        ("step 4", 99),
        ("step 5", 4),
    ]
    return likelihoods


def run_task3():
    all_steps = steps()
    good_steps = []
    bad_steps = []

    # Unpack each tuple into its name and likelihood.
    for name, risk in all_steps:
        if risk >= 50:
            bad_steps.append((name, risk))
        else:
            good_steps.append((name, risk))

    print(f"Good steps: {len(good_steps)}, Bad steps: {len(bad_steps)}")


if __name__ == "__main__":
    run_task3()
```

**Explanation:** The outer list stores five tuples. Each tuple holds two related values. `for name, risk in all_steps` unpacks them. The `if` decision sends the entire pair to one of two lists, and `len()` counts the entries in each group.

**Check the boundary:** `50` belongs in `bad_steps`, because the condition uses `>=`, not `>`.

</details>

**Commit example:** `git commit -m "Added code to classify nested tuples in lists"`

---

# Part C – GitHub and testing

## Commit after each working activity

In PyCharm, open the **Terminal** at the project root and use:

```bash
git status
git add week5/
git commit -m "Completed Week 5 list or tuple activity"
git push
```

Change the message so it describes the specific activity you completed. Commit often, and push at least by the end of the session. If a commit reports that nothing has changed, check whether your file was saved and whether the changes were already committed.

## Self-check before finishing

- [ ] `week5/list_tasks.py` includes all **four list activities**.
- [ ] `week5/tuple_tasks.py` includes all **three tuple activities**.
- [ ] Each required function has the correct name and accepts **no parameters**.
- [ ] You can explain why `fruits[0]` accesses the first item.
- [ ] You understand why `append()` works for lists but not tuples.
- [ ] Your program produces the expected outputs for each activity.
- [ ] The threshold of **50** is correctly classified as **bad**.
- [ ] Changes are committed and appear in the GitHub repository.

## Quick questions and answers

<details>
<summary>1. What is the main difference between a list and a tuple?</summary>

A list is mutable; a tuple is immutable. Both are ordered and support indexing.

</details>

<details>
<summary>2. What does append() do?</summary>

Adds a single item to the end of a list, modifying the existing list.

</details>

<details>
<summary>3. What does return do inside a function?</summary>

Sends a value back to the caller and ends the function execution.

</details>

<details>
<summary>4. What is the result of len([10, 20, 30])?</summary>

`3`, because the list has three elements.

</details>

<details>
<summary>5. How do you read the risk from the first item in steps = [("step 1", 50)]?</summary>

`steps[0][1]`. The first index selects the tuple; the second selects its likelihood value.

</details>

<details>
<summary>6. Should a risk of exactly 50 be classified as good or bad?</summary>

Bad, because `risk >= 50` includes 50.

</details>

## Optional extension: show the actual good and bad tiles

After Activity 7, add:

```python
print("Good tiles:", good_steps)
print("Bad tiles:", bad_steps)
```

This helps verify that **the correct tuples**, and not just the correct number of tuples, are stored.

---

## A few useful Python accuracy notes

- In the temperature example, write `min(temperatures)` and `max(temperatures)` using the variable that was actually defined; `temperature` (singular) would be undefined.
- The uploaded background material mentions `cmp()`, which is **not a Python 3 built-in**. Do not use it in this seminar.
- `list.pop(index)` removes and returns the item **at that index**; calling `pop()` without an index removes the last item.
- An ordinary Python list can store different types and grow dynamically. Python arrays and NumPy arrays have different capabilities and constraints; they are **not necessary** for the activities here.
- For the menu activity, a valid number `0–3` is assumed. Input validation is an optional improvement.

**Reference:** Original Week 5 list and tuple activities and the supplied Data Structures notes. The shopping-basket examples, diagrams, hints, reference solutions, checkpoints and optional extensions were added to support seminar delivery.

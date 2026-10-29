# QHO444 — Programming in Practice (Python)
## Week 3: While loops, for loops, nested loops and decisions

Student practice guide — suitable for GitHub `README.md`. Code is for Python 3.

## Start here
1. Open the cloned QHO444 repository in PyCharm.
2. Create a `week3/` folder.
3. Make `while_loops.py`, `for_loops.py`, `nested_loops.py` and `nesting.py`.
4. **Complete one activity at a time.** If reusing `while_loops.py` or `for_loops.py`, comment out older exercises before running the next; alternatively save each exercise as a separate file.
5. Run, compare against the expected result, then commit your working code.

## Quick concept Q&A

**Q: What is a loop?** A: Code that repeats. A `while` loop repeats while a condition remains true; a `for` loop iterates through a sequence.

**Q: What does `range(start, stop, step)` mean?** A: Start at `start`, advance by `step`, and stop *before* `stop`. Example: `range(0, 6, 2)` gives 0, 2, 4.

**Q: What does `end=""` change?** A: It prevents `print()` adding its usual newline.

**Q: What is a nested loop?** A: One loop inside another. For 2 rows and 3 columns, the inner print runs 2 × 3 = 6 times.

**Q: What are nested decisions?** A: An `if`/`elif` inside another control block such as a loop or `if`. They are useful when scanning for the two markers.

**Q: Is a `for` loop variable inaccessible after the loop?** A: No. In Python, a variable assigned by a `for` loop is normally available afterwards in the same scope, provided at least one iteration assigned it.

## Exercises — questions, answers and brief explanations

### 1. Robot removes apples (While)

**Question:** Ask how many apples to remove, then print “Removed apple.” once per apple.
**File:** `week3/while_loops.py`
**Expected check:** Input 3 → three lines saying Removed apple.

<details><summary>Reveal a suggested answer</summary>

```python
apples = int(input("How many apples should I remove? "))
removed = 0
while removed < apples:
    print("Removed apple.")
    removed += 1
```

**Why this works:** A counter changes on each iteration, so the condition eventually becomes False.

</details>

### 2. Obstacle-avoiding robot (While)

**Question:** Ask for the number of obstacles; show “Avoiding...Done! n obstacles avoided.” for each.
**File:** `week3/while_loops.py`
**Expected check:** Input 2 → two numbered obstacle messages followed by completion.

<details><summary>Reveal a suggested answer</summary>

```python
target = int(input("How many obstacles must I avoid? "))
count = 0
while count < target:
    print("Avoiding...", end="")
    count += 1
    print(f"Done! {count} obstacles avoided!")
print("All obstacles have been avoided.")
```

**Why this works:** end="" stops print() from inserting a newline.

</details>

### 3. Robot battery charging (While)

**Question:** Ask for a number of bars and grow a text-based battery one bar at a time.
**File:** `week3/while_loops.py`
**Expected check:** Input 3 → Charging: █, then █ █, then █ █ █.

<details><summary>Reveal a suggested answer</summary>

```python
target = int(input("How many bars should be charged? "))
bars = 0
while bars < target:
    bars += 1
    print("Charging:", "█ " * bars)
print("The battery is fully charged.")
```

**Why this works:** A string can be repeated using multiplication.

</details>

### 4. Repeat Hi for each character (While)

**Question:** Ask for a phrase and print Hi once for every character, including spaces.
**File:** `week3/while_loops.py`
**Expected check:** Input Hello → Hi Hi Hi Hi Hi

<details><summary>Reveal a suggested answer</summary>

```python
phrase = input("Please enter a phrase: ")
count = 0
while count < len(phrase):
    print("Hi", end=" ")
    count += 1
print()
```

**Why this works:** len() gives the length of a string, including spaces.

</details>

### 5. Add the numbers 1 to 100 (While)

**Question:** Use a while loop and running total to calculate 1 + 2 + … + 100.
**File:** `week3/while_loops.py`
**Expected check:** The final total must be 5050.

<details><summary>Reveal a suggested answer</summary>

```python
number = 1
total = 0
while number <= 100:
    total += number
    number += 1
print(f"...Done! The answer is {total}.")
```

**Why this works:** An accumulator stores the running total.

</details>

### 6. Sum numbers supplied by a user (While)

**Question:** Ask how many values to add, prompt for each, and output their sum.
**File:** `week3/while_loops.py`
**Expected check:** Inputs 4, then 11, 6, 22, 12 → 51.

<details><summary>Reveal a suggested answer</summary>

```python
amount = int(input("How many numbers should I sum up? "))
count = 0
total = 0
while count < amount:
    value = int(input(f"Please enter number {count + 1} of {amount}: "))
    total += value
    count += 1
print(f"The answer is {total}.")
```

**Why this works:** Input is converted to int before arithmetic.

</details>

### 7. ASCII mountains (For)

**Question:** Ask how many mountains and output the same six-line ASCII mountain that many times.
**File:** `week3/for_loops.py`
**Expected check:** Input 2 → two mountain drawings.

<details><summary>Reveal a suggested answer</summary>

```python
mountains = int(input('How many mountains should I display? '))
print('Displaying...')
for count in range(mountains):
    print('      /' + chr(92))
    print('     /  ' + chr(92))
    print('    /    ' + chr(92))
    print('___/______' + chr(92) + '___')
print('Done!')
```

**Why this works:** range(n) runs n times, with count values 0 through n−1.

</details>

### 8. Count down steps (For)

**Question:** Ask for a target distance and count down to 1.
**File:** `week3/for_loops.py`
**Expected check:** Input 3 → 3, 2, 1 steps remaining.

<details><summary>Reveal a suggested answer</summary>

```python
steps = int(input("How far are we from the target? "))
for left in range(steps, 0, -1):
    print(f"{left} steps remaining")
print("Target achieved!")
```

**Why this works:** A negative range step counts backwards; the stop is excluded.

</details>

### 9. Brightness increasing by two (For)

**Question:** Ask for an even brightness level; display 2, 4, 6… asterisks up to that level.
**File:** `week3/for_loops.py`
**Expected check:** Input 6 → ** then **** then ******.

<details><summary>Reveal a suggested answer</summary>

```python
target = int(input("What level of brightness is required? "))
print("Adjusting brightness...")
for level in range(2, target + 1, 2):
    print("Brightness level:", "*" * level)
print("Complete!")
```

**Why this works:** The third range argument is the step.

</details>

### 10. Character index explorer (For)

**Question:** Ask for a word and print the index and character on each line.
**File:** `week3/for_loops.py`
**Expected check:** Input Hello → index 0: H … index 4: o.

<details><summary>Reveal a suggested answer</summary>

```python
word = input("What word do you see? ")
print("Displaying index positions...")
for index in range(len(word)):
    print(f"index {index}: {word[index]}")
print("Done!")
```

**Why this works:** Python string indexing begins at zero.

</details>

### 11. Reverse a phrase (For)

**Question:** Read a phrase, then build its reverse by iterating backwards through indexes.
**File:** `week3/for_loops.py`
**Expected check:** Input sucoP sucoH → Hocus Pocus.

<details><summary>Reveal a suggested answer</summary>

```python
phrase = input("What phrase do you want to see in reverse? ")
reversed_phrase = ""
for index in range(len(phrase) - 1, -1, -1):
    reversed_phrase += phrase[index]
print("The phrase is:", reversed_phrase)
```

**Why this works:** The last character has index len(phrase) − 1.

</details>

### 12. Iterate through characters (For)

**Question:** Ask for a phrase and print one character per line using for character in phrase.
**File:** `week3/for_loops.py`
**Expected check:** Input Hello → H, e, l, l, o on separate lines.

<details><summary>Reveal a suggested answer</summary>

```python
phrase = input("What phrase do you want to print? ")
print("The phrase is:")
for character in phrase:
    print(character)
```

**Why this works:** Iterating directly over a string avoids managing an index.

</details>

### 13. ASCII emoji grid (Nested)

**Question:** Ask for rows and columns; display :-) in a matching rectangular grid.
**File:** `week3/nested_loops.py`
**Expected check:** Rows 2, columns 3 → two lines, each with three :-) faces.

<details><summary>Reveal a suggested answer</summary>

```python
rows = int(input("How many rows should I have? "))
columns = int(input("How many columns should I have? "))
print("Here I go:")
for row in range(rows):
    for column in range(columns):
        print(":-)", end=" ")
    print()
print("Done!")
```

**Why this works:** The outer loop controls rows; the inner loop controls columns; print() moves to the next row.

</details>

### 14. Distance between two markers (Nested)

**Question:** Read a dash-and-marker sequence and a marker character; count dashes between the first two occurrences.
**File:** `week3/nesting.py`
**Expected check:** x---x → 3; --x--x-- → 2; ---xx → 0.

<details><summary>Reveal a suggested answer</summary>

```python
sequence = input("Please enter a sequence: ")
marker = input("Please enter the character for the marker: ")
first = -1
second = -1
for index in range(len(sequence)):
    if sequence[index] == marker:
        if first == -1:
            first = index
        elif second == -1:
            second = index
            break
if first == -1 or second == -1:
    print("Two markers were not found.")
else:
    distance = second - first - 1
    print(f"The distance between the markers is {distance}.")
```

**Why this works:** Nested decisions inside a loop track the first two markers. This task does not require a nested loop.

</details>

## Self-check questions

1. **Which loop keeps running while a condition is True?**
   **Answer:** while. A while loop rechecks its condition before each iteration.

2. **What does range(2, 8, 2) produce?**
   **Answer:** 2, 4, 6. The stop value 8 is excluded.

3. **What is len("Hi all")?**
   **Answer:** 6. The space counts as a character.

4. **Which statement prints without a newline?**
   **Answer:** print("Hi", end=""). The end parameter controls the trailing text.

5. **How many times does the inner loop run for 3 rows and 4 columns?**
   **Answer:** 12. 3 × 4 = 12 executions.

6. **What is the first index in a Python string?**
   **Answer:** 0. Indexes start at zero.

7. **What does range(5, 0, -1) produce?**
   **Answer:** 5, 4, 3, 2, 1. The stopping value 0 is excluded.

8. **Why must a while-loop counter change?**
   **Answer:** To avoid running forever. Without a changing control variable, the condition might never become False.

9. **What is a running total called?**
   **Answer:** Accumulator. An accumulator gathers values across iterations.

10. **For --x--x--, how many characters are between the markers?**
   **Answer:** 2. The first x is at index 2 and the second at index 5; 5−2−1=2.

11. **Which structure matches the marker-distance task?**
   **Answer:** Loop with nested decisions. A loop with nested if/elif decisions is sufficient.

12. **What does git push do?**
   **Answer:** Uploads local commits to the remote repository. Push shares local commits with the configured remote.

## Save your work to GitHub

```bash
git status
git add week3/
git commit -m "Completed Week 3 Python loop activities"
git push
```

> If `git push` fails, check that the repository was cloned correctly and that you are authenticated. Never commit passwords, tokens, or SSH private keys.

## Quick troubleshooting

- **`IndentationError`:** Ensure the loop body is indented consistently (usually four spaces).
- **`ValueError`:** `int(input(...))` requires an integer. Try typing `3`, not `three`.
- **Infinite while loop:** Update the control variable inside the loop.
- **Wrong number of iterations:** Remember `range()` excludes the `stop` value.
- **Extra/absent line breaks:** Check `print(..., end="")` and `print()`.

## Notes on the supplied teaching materials

The source set uses QHO426 in some earlier examples; this guide labels the course QHO444 as requested. The original examples include a few typographical/output mistakes: `len("Hello Friend")` is 12 (including the space); `Hello` ends with the letter `o`, not zero; and Python `for` loop variables are generally accessible after the loop in their enclosing scope. The marker-distance exercise is best described as a loop with nested conditional decisions, not necessarily nested loops.
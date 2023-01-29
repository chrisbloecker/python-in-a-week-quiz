# python-in-a-week-quiz

In this companion repository for the paper _Python in a Week: Conceptual Tests for Learning and Course Development_, we present our concept inventory for identifying programming misconceptions which consists of 21 short questions.


# Question 1: Variable assignments
**Aim: understanding variable assignments.**
```python
x = 3
y = 2*5-x
x += 2
z = x*y
```
**Q: What are the values of x, y, z?**
1. `x=3`, `y=7`, `z=21`
2. `x=5`, `y=7`, `z=35`
3. `x=5`, `y=5`, `z=25`

**Mistakes**
1. The value of `x` remains `3` throughout the example, which is incorrect because `x` is updated in line 3.
2. Correct answer.
3. Changing the value of `x` in line 3 affects the value of `y`, but this does not happen because `y` was assigned before `x` is changed.


# Question 2: String slicing
**Aim: understand string slicing and that the indices can be used that are larger than the length of the string.**
```python
letters = "abc"
many_letters = letters + letters + letters
long_string = (2 * many_letters)[2:32]
```

**Q: What is the value of `long_string`?**
1. `cabcabcabcabcabc` $\leftarrow$
2. `bcabcabcabcabcabcabcabca`
3. `abcabcabcabcabcabcabcabcabcabc`

**Mistakes**
1. Correct answer
2. Assuming that the result must start with the letter `b` because the start index is `2`, but this is incorrect because indices are zero-based.
3. Slicing a string with indices `[2:32]` returns a string of length 30, but this is only the case if the string is long enough.


# Question 3: Boolean expressions
**Aim: understand how Boolean expressions are evaluated.**

**Q: When is the following expression true `(a and not b) or (b and not a)`?**
1. `a=False`, `b=False`
2. `a=False`, `b=True` $\leftarrow$
3. `a=True`, `b=False` $\leftarrow$
4. `a=True`, `b=True`

**Mistakes**
1. Misunderstanding how the logical conjunctions `and` and `or` work.
2. Correct answer.
3. Correct answer.
4. Misunderstanding how the logical conjunctions `and` and `or` work.

(The expression can be rewritten as `a != b`, also known as exclusive or.)


# Question 4: Indentation
**Aim: paying attention to indentation and that variable names are not necessarily descriptive.**
```python
primes = [2,3,5,7,11,13,17]
miss = 0
for x in range(20):
  if not (x in primes):
    print(x)
  miss += 1
print(miss)
```

**Q: What numbers does this code print?**
1. `2`, `3`, `5`, `7`, `11`, `13`, `17`, `7`
2. `2`, `3`, `5`, `7`, `11`, `13`, `17`, `20`
3. `0`, `1`, `4`, `6`, `8`, `9`, `10`, `12`, `14`, `15`, `16`, `18`, `19`, `20`
4. `0`, `1`, `4`, `6`, `8`, `9`, `10`, `12`, `14`, `15`, `16`, `18`, `19`, `13`

**Mistakes**
1. The code inside the if statement is executed when the respective number is in the list `primes`, leading to printing exactly the listed prime numbers and `miss` is incremented only when a number is printed. But the code inside the if statement is executed when the respective number is *not* in `primes`, and `miss += 1` is executed in every iteration of the for loop because of its indentation level.
2. The code inside the if statement is executed when the respective number is in the list `primes`, but it is exactly the opposite: those numbers that are not in `primes` are printed. The indentation of `miss += 1` is interpreted correctly.
3. Correct answer.
4. Assuming that `miss` counts how many numbers were not printed, but because of the indentation level of `miss += 1`, this statement is always executed.


# Question 5: Short-circuit evaluation
**Aim: understand short-circuit evaluation and paying attention to that `ok` is also an undefined variable.**
```python
if (a and b) or (not a and c) and (d != e):
  print(ok)
```
**Q: What variable assignment will prevent this code from crashing? Note that not all variables are defined in all cases.**
1. `a=False`, `b=False`, `d=False`, `e=True`
2. `a=True`, `c=False`, `d=True`, `e=False`
3. `a=False`, `c=False`, `d=False`, `e=True`
4. `a=False`, `c=True`, `d=False`, `e=True`

**Mistakes**
1. Misunderstanding of evaluation order and how short-circuit evaluation works. These valuations cause a crash because Python tries to access the undefined variable `c`
2. Misunderstanding of evaluation order and how short-circuit evaluation works. These valuations cause a crash because Python tries to access the undefined variable `b`
3. Correct answer.
4. With these valuations, the condition evaluates to `True` and Python tries to print the undefined variable `ok`, which causes a crash. However, giving this answer indicates a good understanding of short-circuit evaluation.


# Question 6: Mutable data
**Aim: understand that mutable structures remain mutable, even within immutable structures.**
```python
t = (1,"abc",[1,2,3],True)
```
**Q: Which of the following operations are allowed?**
1. `print(len(t))`
2. `t[0] += 1`
3. `t[1] += "def"`
4. `t[2].append(4)`
5. `t[3] = False`

**Mistakes**
1. Correct answer.
2. Assumption that, as normally possible integers can be changed. However, in this case this is not possible because integers are scalars, and as members of tuples, they cannot be changed since this would violate the non-mutability of tuples.
3. Assumption that strings can be changed. However, even in the normal case, this would create a new string. Therefore, appending `def` would create a new string and assign it to the 2nd element in the tuple, which would violate its non-mutability.
4. Correct answer. In Python, list are mutable, even within tuples. But it would be forbidden to assign a new value to `t[2]`.
5. Assuming that a new value can be assigned, but this is not allowed due to the non-mutability of tuples.


# Question 7: Pseudocode
**Aim: Understand the purpose of writing pseudocode.**

**Q: What is the purpose of writing pseudocode?**
1. To develop faster programs
2. To better understand the problem before starting to code
3. To make sure that you're on the same page with your colleagues about the code you are going to develop

**Mistakes**
1. Pseudocode leads to faster programs. Understanding a problem by developing pseudocode may lead to faster programs in some situations, but this does not hold in general. The main purpose is to devise a strategy of how a problem can be solved.
2. Correct answer.
3. Correct answer.


# Questions 8: Decomposing problems
**Aim: understand principles for deconstructing problems when writing pseudocode.**

**Q: What aspects should you consider to deconstruct problems and develop pseudocode?**
1. Look for lists of things that should be processed in the same way and use loops for that
2. Come up with small examples and try out your pseudo code on them by hand
3. Specify the data types of the values in your input to get a better understanding of the problem at hand
4. Identify conditions that guide how values should be handled and use if/else statements to reflect this
5. Outline the different logical steps you need to perform to solve the problem
6. Break down the problem into sub-problems which become easier to solve

**Mistakes**
1. Correct answer.
2. Correct answer.
3. Correct answer.
4. Correct answer.
5. Correct answer.
6. Correct answer.

(The list is non-exhaustive.)


# Question 9: Functions and methods
**Aim: be able to distinguish between functions and method calls.**

```python
my_list = [1,2,3,4,5]
my_dictionary = {"one":1, "two":2, "three":3}
```

**Q: Which of the following examples contain method calls?**
1. `len(my_list)`
2. `"the quick brown fox".strip("aeiou")`
3. `my_list.append(42)`
4. `sum(my_dictionary.values())`
5. `max([1,1,2,3,5,8,13,21,34])`
6. `int(bool("python"))`
7. `"four" in my_dictionary.keys()`


**Mistakes**
1. Mistaking a function call for a method call, due to not understanding the syntactic difference.
2. Correct answer.
3. Correct answer.
4. Correct answer.
5. Mistaking a function call for a method call, due to not understanding the syntactic difference.
6. Mistaking a function call for a method call, due to not understanding the syntactic difference.
7. Correct answer.


# Question 10: Writing to files
**Aim: mixing for and while loops and writing to a file**
```python
bases = "ACCATGGTGACGAGT"
res   = ""

i = len(bases)-1

while i >= 0:
  if bases[i] == "A":
    res += "T"
  elif bases[i] == "C":
    res += "G"
  elif bases[i] == "G":
    res += "C"
  elif bases[i] == "T":
    res += "A"
  
  i -= 1

fh = open("output.txt", "r")
fh.write(res)
fh.close()
```

**Q: What does this code do?**
1. It computes the complement of a sequence
2. It computes the reverse complement of a sequence
3. It prints the result on the terminal
4. It writes the result to a file
5. It crashes with an error

**Mistakes**
1. Realising that for each base the complement is computed but missing that this happens in reverse order.
2. Correct answer.
3. Writing the result to a destination causes also printing it.
4. It is possible to write to a file after opening it, however, in this case, the file was opened in read mode, which will cause an exception when trying to write to it.
5. Correct answer.


# Question 11: Sets
**Aim: understand that sets don't hold duplicates (and remember how the modulo operation works).**
```python
s = set()
for x in range(10):
  s.add(x % 3)
```
**Q: What is the value of `s`?**
1. `{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10}`
2. `{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}`
3. `{0, 1, 2, 3}`
4. `{0, 1, 2}`

**Mistakes**
1. The maximum value generated by `range(10)` is `10`, but this is incorrect, that largest value `x` takes is `9`. Moreover, misunderstanding how the modulo operation works.
2. Misunderstanding how the modulo operation works.
3. `x % 3` produces values between `0` and `3`, inclusive, but since the modulo operation returns the rest of the whole number division by `3`, the result can be at most `2`, so that `3` cannot have been inserted into the set.
4. Correct answer.


# Question 12: Dictionaries
**Aim: understand how dictionaries work.**
```python
text = "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Ut purus elit, vestibulum ut, placerat ac, adipiscing vitae, felis. Curabitur dictum gravida mauris. Nam arcu libero, nonummy eget, consectetuer id, vulputate a, magna. Donec vehicula augue eu neque. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Mauris ut leo. Cras viverra metus rhoncus sem. Nulla et lectus vestibulum urna fringilla ultrices. Phasellus eu tellus sit amet tortor gravida placerat. Integer sapien est, iaculis in, pretium quis, viverra ac, nunc. Praesent eget sem vel leo ultrices bibendum. Aenean faucibus. Morbi dolor nulla, malesuada eu, pulvinar at, mollis ac, nulla. Curabitur auctor semper nulla. Donec varius orci eget risus. Duis nibh mi, congue eu, accumsan eleifend, sagittis quis, diam. Duis eget orci sit amet orci dignissim rutrum."

counts = {}

for letter in "abcdefghijklmnopqrstuvwxyz":
  counts[letter] = 0

for letter in "ABCDEFGHIJKLMNOPQRSTUVWXYZ":
  counts[letter] = 0

for letter in text:
  if letter != "." and letter != ",":
    counts[letter] += 1
```

**Q: What does this code do?**
1. It counts all the letters in the text
2. In counts only lower-case letters in the text
3. It counts only upper-case letters in the text
4. It crashes because it tries to count punctuation marks but they are not added as keys to the dictionary
5. It crashes because it encounters unexpected characters

**Mistakes**
1. Assuming that the code does what is looks like it was designed to do, but without carefully checking that this actually is the case. Specifically, missing that when the code encounters a blank, it crashed when trying to update the count of blanks that have been seen so far.
2. Missing that the code loops over all characters encountered in the given text, including, but not limited to, lowercase letters.
3. Missing that the code loops over all characters encountered in the given text, including, but not limited to, uppercase letters.
4. Punctuation marks are indeed not added as keys to the dictionary, but they are ignored by the condition in the if statement.
5. Correct answer. The blank symbol was not inserted as a key to the dictionary so that, when trying to increase its count, the code with crash.


# Question 13: Mutable data in dictionaries
**Aim: understand the problem of inserting references to mutable data structures into dictionaries.**
```python
l = []
d = {}
for x in range(1,6):
  l.append(x)
  d[x] = l
```
**Q: What is the value of `d[3]`?**
1. `[1]`
2. `[1,2]`
3. `[1,2,3]`
4. `[1,2,3,4]`
5. `[1,2,3,4,5]`

**Mistakes**
1. When selecting this answer, this is likely due to missing insight into what the code does at all.
2. When selecting this answer, this is likely due to missing insight into what the code does at all.
3. This is the result one would reasonably expect, but this is not the case because only a reference to the list is inserted into the dictionary. Therefore, changes to the list become visible in all places where the list is referred to.
4. When selecting this answer, this is likely due to missing insight into what the code does at all.
5. Correct answer. When `l` is assigned as a value under a key in the dictionary, not a copy, but a reference to `l` is saved there. Therefore, changed to `l` become visible, and all entries in the dictionary refer to the same list.


# Question 14: Scoping
**Aim: understand scopes of local and global variables.**
```python
x = 1
y = 2

def my_function(x):
  x *= 2
  return x*y

y = 4
z = my_function(2)
print(x,y,z)
```
**Q: What does the code print?**
1. `1, 2, 4`
2. `1, 4, 8`
3. `1, 4, 16`
4. `2, 4, 4`
5. `2, 4, 8`
6. `2, 4, 16`

**Mistakes**
1. Disregarding the updated value for `y` and assuming that the values used inside `my_function` are fixed at the time when the function is defined (using the values `x = 1` and `y = 2` from lines 1 and 2).
2. Using the value of the global variable `x = 1` when computing a value for `z` and ignoring that the local variable `x`, which is set to `2`, shadows the global variable `x`.
3. Correct answer.
4. Assuming that the global variable `x` is changed when calling `my_function` and using the values of the global variables `x = 1` and `y = 2` when calculating a value for `z`.
5. Assuming that the global variable `x` is changed when calling `my_function` and using the value of the global variable `x = 1` when calculating a value for `z`, ignoring scoping rules.
6. Assuming that the global variable `x` is changed when calling `my_function`.


# Question 15: Command line arguments
**Aim: understand system parameters.**

Consider the following script and assume that it is saved in a file called `my_script.py`.
```python
import sys

i = 0
while i < len(sys.argv):
  print("Parameter number " + str(i) + " is: " + sys.argv[i])
  i += 1

fh = open(sys.argv[0], "r")

for line in fh:
  print(line.strip("\n"))

fh.close()
```

Assume that the following content is saved in a file called `input.txt`:
```txt
Lorem ipsum dolor sit amet,
consectetur adipiscing elit,
sed do eiusmod tempor incididunt
ut labore et dolore magna aliqua.
```

**Q: What is printed on the terminal when we execute the script with `python3 my_script.py input.txt and four more arguments`?**

1. The script prints four lines, listing the command line arguments
2. The script prints five lines, listing the command line arguments
3. The script prints six lines, listing the command line arguments
4. The script prints itself
5. The script prints the four lines from input.txt

**Mistakes**
1. Missing that the script's name itself and the filename `input.txt` are also passed as arguments.
2. Missing that the script's name itself is also passed as an argument.
3. Correct answer.
4. Correct answer.
5. Missing that the first argument (`sys.argv[0]`) is the script's own name.


# Question 16: break and continue
**Aim: understand how break and continue work**
```python
i = 0
while True:
  if i > 10:
    break

  i += 1

  if i in [0,2,4,6,8,10]:
    continue

  print(i)
```

**Q: What does this code do?**
1. Print all natural numbers from 0 up to infinity
2. Print all even natural numbers between 1 and 10 (including 10)
3. Print all even natural numbers between 1 and 10 (excluding 10)
4. Print all odd natural numbers between 1 and 11 (including 11)
5. Print all odd natural numbers between 1 and 11 (excluding 11)

**Mistakes**
1. The while loop will run forever because of its condition `True`. But this is not the case because `i` starts with value `0` and is increased by `1` on every iteration. When `i` is bigger than `10`, the loop end because of `break`. The value `11` is printed, though.
2. Assuming that all values are printed, but even number are not printed because the loop jumps to the next iteration with `continue` when `i` holds an even number between `0` and `10`.
3. Assuming that all values are printed, but even number are not printed because the loop jumps to the next iteration with `continue` when `i` holds an even number between `0` and `10`.
4. Correct answer.
5. Assuming that the loop terminates when `i` reaches the value `10`, but this is not the case because `i` is set to `11`, and then printed before the condition `i > 10` is checked again and the loop terminated.


# Question 17: for loop and break
**Aim: learn to see break as a way to stop a computation in case of an unexpected situation.**
```python
ok_bases = "ACGT"
string   = "ACGGTGTAGXCGTGCGTTTGA"
counts   = dict()

for base in ok_bases:
  counts[base] = 0

for base in string:
  if base in ok_bases:
    counts[base] += 1
  else:
    print("Unexpected base: " + base)
    break

print(f"Counted {sum(counts.values())} bases")
```

**Q: What does this code do?**
1. It counts all bases in the given string
2. It prints "Unexpected base: X"
3. It counts all bases up until it finds an unexpected base
4. It prints "Counted 10 bases"

**Mistakes**
1. Assuming that the loop will proceed to the end of the string, but this is not the case because the loop is terminated when an unexpected base is encountered.
2. Correct answer.
3. Correct answer.
4. Assuming that the 10th base will also be included in the counts, but this is the base that stops the counting (`break`) and its value is not counted.


# Question 18: Default arguments
```python
def print_message(name = "Sven Svensson", greeting = "Hej", message = ""):
  print(greeting + " " + name + "! " + message)

print_message()
print_message("Hello", "there", "General Kenobi.")
print_message(message = "I'm learning python.")
```

**Q: Which of the following lines does the code print?**
1. `"Hej Sven Svensson! I'm learning python."`
2. `"Hello there! General Kenobi."`
3. `" ! "`
4. `"Hej Sven Svensson! "`

**Mistakes**
1. Correct answer.
2. Assuming that the string are printed in a sensible order, but because of how the function is defined, this calls prints `"there Hello! General Kenobi."`.
3. Missing how default arguments work and assuming that giving no parameters leaves `name`, `greeting`, and `message` empty.
4. Correct answer.


# Question 19: pandas
Consider the following data file named `input.csv`
```text
,name,age,city,nationality
1,Hans,74,Stockholm,Swedish
2,Gudrun,62,Berlin,German
3,Steve,50,London,English
4,Ida,40,Uppsala,Swedish
5,Robert,50,Lund,Swedish
6,Katrina,55,Perth,Australian
7,Patrick,30,Hamburg,German
8,Marlene,46,Stockholm,Swedish
9,Sven,68,Umeå,Swedish
10,Johanna,32,Helsinki,Finnish
```

And let us read it with pandas
```python
import pandas

df  = pandas.read_table("input.csv", index_col = 0)
res = df[(df.age <= 50) & (df.nationality == "Swedish")].name
```

**Q: What names are selected by this code?**
1. Ida, Marlene
2. Ida, Robert, Marlene
3. Steve, Ida, Robert, Patrick, Marlene, Johanna
4. Hans, Ida, Robert, Marlene, Sven
5. Steve, Patrick, Johanna
6. Patrick, Johanna
7. Hans, Gudrun, Steve, Ida, Robert, Katrina, Patrick, Marlene, Sven, Johanna

**Mistakes**
1. Missing that also persons with an age of `50` should be selected, not only those who are younger than `50`. 
2. Correct answer.
3. Missing that the nationality of the selected persons should be `Swedish`. The selected persons are simply those who are at most `50` years old.
4. Missing the first part of the condition the requires that the age should be no larger than `50`. The selected persons are simply those of `Swedish` nationality.
5. These are the persons who are not of `Swedish` nationality and at most `50`, meaning that the second part of the condition was negated.
6. These are the persons who are not of `Swedish` nationality and younger than `50`.
7. This is the whole data set without applying any filters.


# Question 20: Regular expressions 1
**Q: Which strings will be printed by the following code?**
```python
import re

r = "^A[GC]A+T*A?$"
for s in ["ACGATT", "ACAA", "ACAT", "AGAATTTA", "GAAA", "ACAAATTTA", "ACATTAA"]:
  if re.match(r,s):
    print(s)
```

1. `"ACGATT"`
2. `"ACAA"`
3. `"ACAT"`
4. `"AGAATTTA"`
5. `"GAAA"`
6. `"ACAAATTTA"`
7. `"ACATTAA"`

**Mistakes**

1. Only one of [GC] is allowed, not both together.
2. Correct answer.
3. Correct answer.
4. Correct answer.
5. The string must start with A.
6. Correct answer.
7. The last A is unmatched, ^ and $ specify start and end of the string, so there cannot be anything more than the match.


# Question 21: Regular expressions 2
```python
import re

r = "[aeiou][^aeiou]"
t = "the quick brown fox jumps over the lazy dog"

num_matches = len(re.findall(r,t))
```
**Q: How many matches of `r` are found in `t`?**
1. 8
2. 10
3. 11
4. 12

**Mistakes**
1. Missing that "e " and "e " (from the two occurences of `the `) are also matches.
2. Correct answer.
3. Mistakenly counting `ui` as a match.
4. Miscounting.
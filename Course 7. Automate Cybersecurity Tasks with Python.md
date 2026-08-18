# Course 7: Automate Cybersecurity Tasks with Python

![Course](https://img.shields.io/badge/Intro%20to%20Python%20for%20Cybersecurity-4285F4)
![Course](https://img.shields.io/badge/Write%20effective%20Python%20Code-4285F4)
![Course](https://img.shields.io/badge/Work%20with%20Strings%20and%20Lists-4285F4)
![Course](https://img.shields.io/badge/Python%20in%20Practice-4285F4)
![Status](https://img.shields.io/badge/Status-Completed-4EEB2A)

# About Course

The course covers the basics of Python programming and how those basics apply directly to security work such as log analysis, access control, and building simple automation scripts. Below is a breakdown of every major topic covered, along with explanations, code examples, and how each concept connects to real security tasks.

---

## Certificate of completion:

<p align="center">
  <img src="images/Google Cert 7 Automate Cybersecurity Tasks with Python_page_1.png" alt="Certificate placeholder" width="720"/>
</p>

---

# What I learned

## Getting to Know Python

Python is a general purpose language, meaning it is not built for just one job. It can build websites, analyze data, and automate repetitive work. This last point is exactly why Python matters so much in cybersecurity. As a security analyst, a huge part of the job is repetitive: checking logs, verifying access lists, scanning for patterns. Python takes over these repetitive tasks so analysts can focus on the parts of the job that actually require human judgment.

Some areas where Python automation is commonly applied in security:

| Area | What Gets Automated |
|---|---|
| Log analysis | Scanning large log files for suspicious entries |
| Malware analysis | Parsing and identifying patterns in malicious code |
| Access control list management | Adding or removing approved users and devices |
| Intrusion detection | Flagging unusual login or network activity |
| Compliance checks | Verifying systems meet security policy |
| Network scanning | Checking IP addresses and open ports |

### Python Environments

Python code can be written and run in a few different environments:

- **Notebooks** (like Jupyter Notebook or Google Colab): mix code cells and markdown cells, so code and documentation live side by side. This course used notebooks for every lab.
- **Integrated Development Environments (IDEs)**: full applications with error checking and editing tools built in.
- **Command line**: a text based interface used to run Python files directly from the terminal.

Understanding notebooks specifically mattered here because every lab in this course was built around code cells (for running Python) and markdown cells (for writing notes and comments about that code).

---

## Data Types

A data type defines what kind of value a piece of data is, and Python needs to know this to handle it correctly. The course covered five core data types in depth, plus three additional ones used less often but still useful to recognize.

| Data Type | Description | Example |
|---|---|---|
| String | Ordered sequence of characters, in quotes | `"192.168.1.1"` |
| Integer | Whole number, no decimal | `5` |
| Float | Number with a decimal point | `4.0` |
| Boolean | Only `True` or `False` | `True` |
| List | Ordered, changeable collection | `[12, 36, 54]` |
| Tuple | Ordered, unchangeable collection | `(46, 2, 13)` |
| Dictionary | Key value pairs | `{1: "East", 2: "West"}` |
| Set | Unordered collection of unique values | `{"jlansky", "drosas"}` |

The distinction between a list and a tuple stood out as particularly useful for security work. A tuple cannot be changed after it is created, so storing something like a set of approved software identifiers in a tuple guarantees nobody can accidentally modify that list later in the code. A list, on the other hand, is meant to be flexible, which fits situations like an allow list that regularly gets new usernames added or removed.

```python
# Integer division vs float division
print(1 // 4)     # Output: 0  (rounds down, stays integer)
print(1.0 / 4.0)  # Output: 0.25 (keeps decimal)
```

---

## 3. Variables

A variable is a named container that stores a value. Think of it as a labeled box: the label (the variable name) stays the same even when the contents inside change. This is what makes automation possible in the first place. Without variables, every value would need to be rewritten by hand every single time.

```python
# Assigning and reassigning a variable
username = "nzhao"
old_username = username
username = "zhao2"

print("Previous username:", old_username)  # nzhao
print("Current username:", username)       # zhao2
```

Python automatically assigns the correct data type when a variable is created, so there is no need to declare types manually the way some other languages require.

### Naming Best Practices

- Use only letters, numbers, and underscores. Example: `login_attempts`
- Variable names are case sensitive. `time`, `Time`, and `TIME` are three different variables.
- Do not use Python keywords as names, such as `True`, `False`, or `if`.
- Keep names descriptive but not overly long. `num_login_attempts` is better than `variable_that_equals_3`.
- Avoid similar sounding names that could be confused, like `start_time` and `starting_time`.

---

## Conditional Statements

A conditional statement checks whether a condition is true, then decides what action to take based on that result. This is the backbone of automated decision making, things like checking whether a login attempt should be allowed or whether a system needs an update.

### Comparison Operators

| Operator | Meaning |
|---|---|
| `>` | greater than |
| `<` | less than |
| `>=` | greater than or equal to |
| `<=` | less than or equal to |
| `==` | equal to |
| `!=` | not equal to |

### if, elif, else

```python
if status == 200:
    print("OK")
elif status == 400:
    print("Bad Request")
elif status == 500:
    print("Internal Server Error")
else:
    print("check other status")
```

Python checks each condition top to bottom. The moment one `elif` evaluates to `True`, it skips the rest. This is different from writing multiple separate `if` statements, where Python checks every single one regardless of the outcome of the others.

### Logical Operators

- `and`: both conditions must be true
- `or`: at least one condition must be true
- `not`: flips the result, true becomes false and vice versa

```python
# Practical security example: access only granted during allowed hours
# and only for approved users
if username in approved_list and organization_hours == True:
    print("Login attempt made by an approved user during organization hours.")
else:
    print("Username not approved or login attempt made outside of organization hours.")
```

Combining conditions with `and` and `or` is how a single check can cover multiple security requirements at once instead of writing separate nested checks for every possibility.

---

## Loops

A loop repeats a block of code, which is exactly what is needed when the same check has to run across dozens or thousands of log entries. The course covered two types.

### for Loops

Used when iterating over a known sequence, such as a list of IP addresses.

```python
ip_addresses = ["192.168.142.245", "192.168.109.50", "192.168.86.232"]

for ip in ip_addresses:
    if ip in allow_list:
        print("IP address is allowed")
    else:
        print("IP address is not allowed")
```

The `range()` function is often paired with `for` loops to repeat an action a set number of times: `range(start, stop, step)`. The stop value is always excluded from the sequence.

### while Loops

Used when the number of repetitions depends on a condition rather than a fixed sequence.

```python
login_attempts = 0
while login_attempts < 5:
    print("Login attempts:", login_attempts)
    login_attempts = login_attempts + 1
```

The key difference between the two loop types comes down to certainty. A `for` loop is the right choice when the number of iterations is already known (a list of five IPs means five iterations). A `while` loop fits better when the loop needs to keep running until some condition changes, like waiting for a login status to flip to `False`.

### Controlling Loops

- `break` exits the loop immediately.
- `continue` skips the current iteration and moves to the next one.

```python
for ip in ip_addresses:
    if ip not in allow_list:
        print("IP address is not allowed. Further investigation required")
        break  # stop checking once a flagged address is found
    print("IP address is allowed")
```

An infinite loop happens when the exit condition is never met. In a live terminal this needs a manual interrupt (`CTRL-C`), so writing a correct exit condition matters a lot in production automation scripts.

---

## Functions

A function is a reusable block of code. Instead of repeating the same lines every time a task needs to happen, that logic gets written once and called whenever needed.

### Defining and Calling

```python
def alert():
    print("Potential security issue. Investigate further.")

alert()  # calling the function
```

### Parameters, Arguments, and Return Values

A **parameter** is the variable listed in the function definition. An **argument** is the actual value passed in when the function is called.

```python
def remaining_login_attempts(maximum_attempts, total_attempts):
    return maximum_attempts - total_attempts

remaining = remaining_login_attempts(3, 2)  # 3 and 2 are arguments
print(remaining)  # Output: 1
```

The `return` keyword sends a value back out of the function so it can be stored and reused elsewhere in the code, unlike `print()` which only displays it on screen. Once Python hits a `return` statement, the function exits immediately, so any code written after it inside that function will never run.

### Global vs Local Variables

A **global variable** is defined outside any function and can be accessed from anywhere in the program. A **local variable** is defined inside a function and only exists while that function is running.

```python
username = "elarson"  # global

def greet():
    username = "bmoreno"  # local, only exists inside greet()
    print("2:" + username)

greet()               # prints "2:bmoreno"
print("3:" + username)  # prints "3:elarson", global variable is untouched
```

Reusing a global variable name inside a function does not overwrite the global one, it creates a completely separate local variable with the same name. This distinction avoided a lot of confusion once it clicked: functions should generally rely on parameters rather than reaching out to global variables directly, since that keeps the function predictable and reusable for different inputs.

### Useful Built-in Functions

| Function | Purpose |
|---|---|
| `print()` | Displays information to the screen |
| `type()` | Returns the data type of a value |
| `max()` / `min()` | Returns the largest or smallest value in a sequence |
| `sorted()` | Returns a sorted version of a list, without changing the original |

```python
failed_login_list = [119, 101, 99, 91, 92, 105, 108, 85, 88, 90, 264, 223]
print(sorted(failed_login_list))
print(max(failed_login_list))  # useful for spotting outlier months
```

Sorting a list of monthly failed login counts and pulling out the maximum value is a simple but genuinely useful way to spot outlier activity, like a sudden spike that might indicate a brute force attempt.

---

## Modules and Libraries

A **module** is a Python file containing pre-written functions, and a **library** is a collection of modules. Rather than writing every function from scratch, importing existing modules saves time and reduces errors.

```python
import statistics

monthly_failed_attempts = [20, 17, 178, 33, 15, 21, 19, 29, 32, 15, 25, 19]
mean_failed = statistics.mean(monthly_failed_attempts)
median_failed = statistics.median(monthly_failed_attempts)
```

Specific functions can also be imported directly, which removes the need to prefix them with the module name:

```python
from statistics import mean, median
mean_failed = mean(monthly_failed_attempts)
```

External libraries, such as `numpy` for numerical work or `bs4` (Beautiful Soup) for parsing HTML, need to be installed first using `%pip install library_name` before they can be imported. The `re` module, used later for pattern matching, is part of the Python Standard Library and does not require installation.

---

## Syntax and Readability (PEP 8)

PEP 8 is the official Python style guide, and following it matters more in a team setting than it might seem at first. Security code often gets reviewed by multiple analysts, so consistent, readable code reduces mistakes.

Key points:

- Comments start with `#`. Multi line comments can either use `#` on every line, or triple quotes (`""" """`) as a docstring.
- Indentation should be 4 spaces. Python actually needs correct indentation to run at all, since it is how the language identifies the body of a loop, conditional, or function.
- Keep lines under 79 characters where possible.
- String data always needs quotation marks; integers, floats, and Booleans never do.
- Every header (`if`, `for`, `while`, `def`) must end with a colon.

```python
# remaining_login_attempts() takes two integer parameters,
# the maximum login attempts allowed and the total attempts made,
# and returns an integer representing remaining login attempts
def remaining_login_attempts(maximum_attempts, total_attempts):
    return maximum_attempts - total_attempts
```

---

## Strings in a Security Context

String data shows up constantly in security work: usernames, IP addresses, URLs, device IDs. None of these need to be manipulated mathematically, which is exactly what strings are for.

### Indices and Slicing

Every character in a string has a position, called an index, starting at 0.

```python
device_id = "h32rb17"
print(device_id[0])     # 'h', the first character
print(device_id[0:3])   # 'h32', a slice from index 0 up to (not including) index 3
```

### Useful String Functions and Methods

| Function/Method | Purpose | Example |
|---|---|---|
| `str()` | Converts a value into a string | `str(19329302)` |
| `len()` | Returns the number of characters | `len("h32rb17")` returns `7` |
| `.upper()` / `.lower()` | Changes case | `"IT".lower()` returns `"it"` |
| `.index()` | Finds the position of a substring | `"h32rb17".index("r")` returns `3` |

```python
url = "https://exampleURL1.com"
ind = url.index(".com")
print(url[8:ind])       # exampleURL1, the website name
print(url[ind:ind+4])   # .com, the domain extension
```

Extracting parts of a URL or device ID this way is a common building block for larger automation, such as pulling only the domain name out of thousands of URLs in a log file.

---

## Lists in a Security Context

Lists store multiple related values in one place, which is exactly how something like an allow list or a set of flagged IP addresses would normally be represented.

### Bracket Notation and Slicing

```python
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]
print(username_list[2])      # 'tshah'
print(username_list[0:2])    # ['elarson', 'fgarcia'], a sublist
username_list[1] = "bmoreno" # lists can be changed after creation, unlike strings
```

### List Methods

| Method | Purpose |
|---|---|
| `.insert(index, value)` | Adds an element at a specific position |
| `.remove(value)` | Removes the first matching element |
| `.append(value)` | Adds an element to the end |
| `.index(value)` | Finds the position of an element |

```python
approved_users = ["elarson", "bmoreno", "tshah"]
approved_devices = ["8rp2k75", "hl0s5o1", "2ye3lzg"]

def login(username, device_id):
    if username in approved_users:
        ind = approved_users.index(username)
        if device_id == approved_devices[ind]:
            print(device_id, "is the assigned device for", username)
        else:
            print(device_id, "is not their assigned device.")
    else:
        print("The username", username, "is not approved to access the system.")
```

This function ties together almost everything covered up to this point: conditionals, list indexing, and functions, into one small algorithm that checks whether a username and device pair is valid. Two parallel lists, matched by index position, is a simple but effective pattern for connecting related pieces of data (a username at index 2 in one list corresponds to the device at index 2 in the other).

---

## Regular Expressions

A regular expression, or regex, is a pattern used to search through text for specific structures, like an IP address or an email format. This is far more powerful than searching for exact matches, since it can catch variations.

```python
import re
re.findall("\w", "h32rb17")   # matches every alphanumeric character
```

### Common Symbols

| Symbol | Matches |
|---|---|
| `\w` | Any alphanumeric character or underscore |
| `\d` | Any single digit |
| `\s` | Any whitespace |
| `.` | Any character except a newline |
| `\.` | A literal period |
| `+` | One or more occurrences |
| `*` | Zero or more occurrences |
| `{n}` | Exactly n occurrences |
| `{n,m}` | Between n and m occurrences |

### Building a Pattern: Extracting Valid IP Addresses

```python
import re

log_file = "eraab 2022-05-10 6:03:41 192.168.152.148 \niuduike ... 192.168.22.115"
pattern = "\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}"

valid_ip_addresses = re.findall(pattern, log_file)
print(valid_ip_addresses)
```

The `{1,3}` part matters a lot here. Using `\d+` instead would also match malformed entries with five or six digits in a segment, since `+` places no upper limit. Building the pattern with `{1,3}` restricts each segment to a realistic one to three digit range, which filters out corrupted or invalid IP addresses automatically. This was a good example of how a small syntax choice in a regex pattern directly affects data accuracy in a security log.

---

## Automating Security in CI/CD

This section connected everything learned so far to a real world workflow: Continuous Integration and Continuous Delivery/Deployment (CI/CD) pipelines. This is the process of automatically building, testing, and releasing software.

**DevSecOps** means folding security directly into that pipeline instead of treating it as a separate, later step. Development, security, and operations work together from the start rather than security being bolted on at the end.

### Why Python Fits This Role

- **Speed**: automated checks run far faster than manual review.
- **Early detection**: catching a vulnerability during development is cheaper than catching it after release.
- **Consistency**: a script performs the same check the same way every time, removing human error.
- **Reduced workload**: frees security teams to focus on higher level problems instead of repetitive checks.

### Tasks Python Can Automate in a Pipeline

| Task | What It Involves |
|---|---|
| SAST (Static Application Security Testing) | Scans code for weaknesses before it is built |
| DAST (Dynamic Application Security Testing) | Tests running software for vulnerabilities |
| SCA (Software Composition Analysis) | Checks third party dependencies for known issues |
| Vulnerability scanning | Scans containers and infrastructure settings |
| Compliance checks | Verifies code and configuration follow security policy |
| Secrets management | Prevents credentials from being hardcoded in source code |
| Policy enforcement | Stops a release automatically if a policy is violated |

Python connects to CI/CD tools like Jenkins, GitLab CI, and CircleCI mainly through running scripts directly as pipeline steps, or through APIs that let a script trigger scans, retrieve results, and manage the release process. This is essentially the same idea as the login and allow list scripts built earlier in the course, just applied at the scale of an entire software release pipeline instead of a single log file.

---

## Working with Files

Most real security data lives in log files, so reading and writing files in Python is a core automation skill.

### Opening, Reading, and Writing

```python
with open("update_log.txt", "r") as file:
    updates = file.read()
print(updates)
```

The `with` keyword handles closing the file automatically once the block finishes, which avoids leaving files open unnecessarily. The second argument to `open()` controls what the file is opened for:

| Mode | Purpose |
|---|---|
| `"r"` | Read the file |
| `"w"` | Write to the file, replacing existing content |
| `"a"` | Append new content to the end without deleting existing data |

```python
line = "jrafael,192.168.243.140,4:56:27,True"
with open("access_log.txt", "a") as file:
    file.write(line)
```

### Parsing with .split() and .join()

`.split()` converts a string into a list, breaking it apart at a specified character (or at whitespace by default). `.join()` does the opposite, combining a list back into a single string.

```python
with open("update_log.txt", "r") as file:
    updates = file.read()

updates = updates.split()          # string to list, so it can be looped through

# ... later, after modifying the list
updates = " ".join(updates)        # list back to string, so it can be written
with open("update_log.txt", "w") as file:
    file.write(updates)
```

### Applying This: Removing Outdated IP Addresses from an Allow List

```python
def update_file(import_file, remove_list):
    with open(import_file, "r") as file:
        ip_addresses = file.read()

    ip_addresses = ip_addresses.split()

    for element in ip_addresses:
        if element in remove_list:
            ip_addresses.remove(element)

    ip_addresses = " ".join(ip_addresses)
    with open(import_file, "w") as file:
        file.write(ip_addresses)
```

This function brings together file handling, loops, conditionals, and list methods into one reusable automation tool. Instead of manually opening a text file and deleting outdated entries by hand, this function does it in a single call, which is a small but realistic example of the kind of script an analyst might actually run against a real allow list.

---

## Skills Gained

- Writing and running Python code in a notebook environment
- Working confidently with strings, lists, integers, floats, and Booleans
- Assigning, reassigning, and naming variables following best practices
- Building conditional logic with comparison and logical operators
- Automating repetitive tasks using `for` and `while` loops
- Defining and calling functions, including parameters, arguments, and return values
- Understanding the difference between global and local variable scope
- Importing and using Python Standard Library modules and external libraries
- Writing readable, PEP 8 compliant code with proper comments and indentation
- Extracting and manipulating data using string and list methods
- Building regular expression patterns to search and validate text data
- Understanding how Python fits into DevSecOps and CI/CD security automation
- Reading from and writing to files, including parsing data with `.split()` and `.join()`
- Combining all of the above into small, reusable automation functions

## Key Learnings and Reflections

- Python is widely used in cybersecurity for automating repetitive tasks like log analysis, access control, and compliance checks.
- Core data types (string, integer, float, Boolean, list, tuple, dictionary, set) each serve a different purpose depending on whether data needs to be changed, searched, or calculated with.
- Variables, conditionals, and loops form the foundation for any automated decision making process.
- Functions turn repeated logic into reusable, organized code, and understanding global versus local scope prevents unexpected bugs.
- Regular expressions allow precise searching and validation of structured data like IP addresses.

## Conclusion

This course built a complete foundation in Python, starting from print statements and basic data types, all the way up to writing small automation scripts that manage login validation, allow lists, and log parsing. What stood out most was how naturally these concepts stack on top of each other: a data type feeds into a variable, a variable feeds into a conditional, a conditional runs inside a loop, and the whole thing gets wrapped in a function so it can be reused. Regular expressions and file handling then turned these building blocks into tools that can actually process real log data, and the CI/CD section showed how the exact same logic scales up to secure an entire software release pipeline. The overall takeaway is that automation in cybersecurity is not about writing complicated code, it is about writing simple, reliable code that removes repetitive manual work so analysts can focus on judgment calls that actually need a human.
- File handling connects Python code to real world log files, enabling reading, writing, and parsing of security data.
- These same building blocks extend directly into DevSecOps practices, automating security checks inside CI/CD pipelines.
- Overall, this course shifted the focus from just understanding security concepts to actually building the tools that apply them.

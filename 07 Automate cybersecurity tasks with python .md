# Python Fundamentals for Cybersecurity

Notes covering functions, strings, lists, and loop-based algorithms, with security-flavoured examples.

## Table of Contents

1. [Python Functions](#1-python-functions)
2. [Strings: Indexing, Slicing, and Methods](#2-strings-indexing-slicing-and-methods)
3. [Lists](#3-lists)
4. [Algorithms: Automating Tasks with Loops and Lists](#4-algorithms-automating-tasks-with-loops-and-lists)

---

## 1. Python Functions

Python has two kinds of functions: **user-defined** and **built-in**.

### 1.1 User-Defined Functions

User-defined functions are written by you to fit your own needs. You define them once and reuse them as often as you like.

```python
# Define the function
def check_log_status(log_entry):
    if log_entry["status"] == "potential concern":
        print(f"Alert in {log_entry['source']}: Investigate activity")

# Simulated log data (e.g., pulled from a file or API)
system_logs = [
    {"source": "application", "status": "potential concern"},
    {"source": "email", "status": "okay"},
    {"source": "firewall", "status": "potential concern"}
]

# Call the function for every log (works for hundreds or thousands of logs)
for log in system_logs:
    check_log_status(log)
```

**Output:**

```
Alert in application: Investigate activity
Alert in firewall: Investigate activity
```

### 1.2 Built-in Functions

Built-in functions are pre-defined by Python and are always available.

| Function | Purpose |
|----------|---------|
| `print()` | Displays output |
| `len()` | Returns the length of an object |
| `type()` | Returns the data type of an object |
| `int()`, `str()`, `float()` | Convert values between types |
| `min()`, `max()` | Return the smallest / largest value |

---

## 2. Strings: Indexing, Slicing, and Methods

### 2.1 Indexing

Characters in a string are indexed starting from `0`. Use square brackets `[]` to get a character by position.

```python
log_status = "ALERT"

print(log_status[0])  # Output: A (first character)
print(log_status[4])  # Output: T (fifth character)
```

### 2.2 Slicing

Slicing extracts a substring using `[start:end]`. The **start** index is inclusive; the **end** index is **exclusive**.

```python
ip_address = "192.168.1.50"

# Index 0 up to (but not including) index 3
network_prefix = ip_address[0:3]
print(network_prefix)  # Output: 192
```

### 2.3 The `.index()` Method

Returns the index where a character or substring **first** appears. It is case-sensitive and only finds the first match.

```python
file_path = "/var/log/auth.log"

position = file_path.index("log")
print(position)  # Output: 5
```

### 2.4 Immutability

Strings cannot be changed in place. Trying to assign to an index raises a `TypeError`.

```python
username = "admin"

# username[0] = "r"
# TypeError: 'str' object does not support item assignment
```

To get around this, build a new string:

```python
new_username = "r" + username[1:]
print(new_username)  # Output: rdmin
```

---

## 3. Lists

A list holds multiple items in a specific order under one variable name. In cybersecurity, lists are commonly used to track usernames, IP addresses, or device IDs.

### 3.1 Creating and Accessing Lists

Lists are written with square brackets `[]`, items separated by commas. Indexing starts at `0`, just like strings.

```python
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]

print(username_list[2])  # Output: tshah (third item)
```

### 3.2 Slicing a List

Use `[start:end]` to extract a sublist. Start is included, end is excluded.

```python
print(username_list[0:2])  # Output: ['elarson', 'fgarcia']
```

### 3.3 Concatenation

Combine two lists with the `+` operator.

```python
default_permissions = ["read", "write"]
extra_permissions = ["execute"]

all_permissions = default_permissions + extra_permissions
print(all_permissions)  # Output: ['read', 'write', 'execute']
```

### 3.4 Mutability

Unlike strings, lists **can** be modified in place by reassigning an element via its index.

```python
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]

username_list[1] = "bmoreno"
print(username_list)  # Output: ['elarson', 'bmoreno', 'tshah', 'sgilmore']
```

### 3.5 List Methods

| Method | Description |
|--------|-------------|
| `.insert(index, element)` | Adds an item at a specific index, shifting the rest to the right |
| `.remove(element)` | Deletes the first occurrence of a value |
| `.append(element)` | Adds an item to the end of the list |
| `.index(element)` | Returns the index of the first occurrence of a value |

**`.insert()`**

```python
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]

username_list.insert(2, "wjaffrey")
print(username_list)
# Output: ['elarson', 'fgarcia', 'wjaffrey', 'tshah', 'sgilmore']
```

**`.remove()`**

```python
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]

username_list.remove("elarson")
print(username_list)
# Output: ['fgarcia', 'tshah', 'sgilmore']
```

**`.append()`**

Commonly paired with loops to build a list dynamically.

```python
username_list = ["elarson", "fgarcia"]

username_list.append("btang")
print(username_list)
# Output: ['elarson', 'fgarcia', 'btang']
```

**`.index()`**

```python
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]

print(username_list.index("tshah"))  # Output: 2
```

**Security example: managing an IP allow list**

```python
ip_whitelist = ["192.168.1.10", "192.168.1.20"]

# Insert a new IP at index 1
ip_whitelist.insert(1, "192.168.1.15")
print(ip_whitelist)
# Output: ['192.168.1.10', '192.168.1.15', '192.168.1.20']

# Remove a compromised or outdated IP
ip_whitelist.remove("192.168.1.10")
print(ip_whitelist)
# Output: ['192.168.1.15', '192.168.1.20']
```

---

## 4. Algorithms: Automating Tasks with Loops and Lists

### 4.1 What Is an Algorithm?

An algorithm is a logical, step-by-step recipe for solving a problem. Instead of processing an entire security log at once, break the task into small steps:

- **Input:** A collection of IP addresses
- **Process:** Look at each IP address one by one and extract its network prefix
- **Output:** A new list containing only the network prefixes

### 4.2 Solve It for One Item First

Work out the logic on a single item before scaling up. Here, slicing (`[0:3]`) grabs the first three characters of an IP address.

```python
ip_address = "192.168.1.1"

network_prefix = ip_address[0:3]
print(network_prefix)  # Output: 192
```

### 4.3 Scale It with a Loop

Use a `for` loop to repeat the logic across a whole list, and `.append()` to store each result in a new list.

```python
ip_addresses = ["192.168.1.50", "10.0.0.15", "172.16.0.99"]

# Empty list to store results
networks = []

for ip in ip_addresses:
    prefix = ip[0:3]          # Extract the first three characters
    networks.append(prefix)   # Store the result

print(networks)
# Output: ['192', '10.', '172']
```

> **Note:** Slicing by a fixed number of characters is a simple demo. It gives `'10.'` for the second IP because that address has only two digits in its first segment. For real work, use `ip.split(".")[0]` to reliably get the first segment.

Expanding variables in shell scripting involves substituting the value of a variable into commands or strings. This is a fundamental concept in shell scripting and allows for dynamic and flexible scripts. Here’s how variable expansion works and some common techniques for using and expanding variables.

### Basic Variable Expansion

#### Defining Variables

Variables are defined without spaces around the `=` sign:

```sh
variable_name=value
```

#### Basic Expansion

To use the value of a variable, prefix it with a `$`:

```sh
#!/bin/bash

# Define a variable
name="Alice"

# Expand the variable
echo "Hello, $name!"
```

Output:
```
Hello, Alice!
```

### Types of Variable Expansion

#### 1. **Basic Expansion**

Simply using `$variable` to get the value of a variable.

```sh
greeting="Hello"
echo "$greeting, World!"
```

#### 2. **Curly Braces Expansion**

Using curly braces `${variable}` is useful for clarity, especially when concatenating with other characters.

```sh
#!/bin/bash

name="Alice"
echo "Hello, ${name}!"
```

#### 3. **Default Values**

You can specify default values for variables if they are unset or empty.

- **`${variable:-default}`**: Use `default` if `variable` is unset or null.
- **`${variable:=default}`**: Assign `default` to `variable` if `variable` is unset or null.
- **`${variable:+replacement}`**: Use `replacement` if `variable` is set and non-null.
- **`${variable:?error_message}`**: Print an error message and exit if `variable` is unset or null.

```sh
#!/bin/bash

# Unset variable
echo "Value: ${unset_var:-default_value}"  # Output: default_value

# Assign default value
unset_var=${unset_var:-default_value}
echo "Value: $unset_var"  # Output: default_value

# Replacement
echo "Value: ${unset_var:+replacement_value}"  # Output: replacement_value

# Error message
echo "Value: ${unset_var:?Variable is not set}"  # Prints error and exits if unset_var is not set
```

#### 4. **Substring Extraction**

Extract a substring from a variable:

- **`${variable:position}`**: Extract substring from `position` to end.
- **`${variable:position:length}`**: Extract substring starting at `position` with length `length`.

```sh
#!/bin/bash

text="Hello, World!"
echo "${text:7}"        # Output: World!
echo "${text:7:5}"      # Output: World
```

#### 5. **String Manipulation**

Perform operations on strings using variable expansion:

- **`${variable#pattern}`**: Remove shortest match of `pattern` from the beginning.
- **`${variable##pattern}`**: Remove longest match of `pattern` from the beginning.
- **`${variable%pattern}`**: Remove shortest match of `pattern` from the end.
- **`${variable%%pattern}`**: Remove longest match of `pattern` from the end.

```sh
#!/bin/bash

filename="file.txt"
echo "${filename%.txt}"  # Output: file (removes .txt)
echo "${filename#file.}" # Output: txt (removes shortest match of file.)
```

### Example Script

Here’s a complete script that demonstrates various forms of variable expansion:

```sh
#!/bin/bash

# Define variables
name="Alice"
path="/home/alice/documents"

# Basic expansion
echo "Name: $name"

# Curly braces expansion
echo "Welcome, ${name}!"

# Default values
unset_var=""
echo "Default value: ${unset_var:-Default}"

# String manipulation
filename="report_2024.pdf"
echo "Base name: ${filename%.pdf}"  # Output: report_2024
echo "File extension: ${filename#*_}" # Output: 2024.pdf
```

### Summary

- **Basic Expansion**: Use `$variable` to get the value.
- **Curly Braces Expansion**: Use `${variable}` for clarity and concatenation.
- **Default Values**: Provide default values for unset or null variables.
- **Substring Extraction**: Extract substrings from variables.
- **String Manipulation**: Remove patterns from variables.

Variable expansion is a powerful feature in shell scripting that enhances the flexibility and functionality of your scripts.

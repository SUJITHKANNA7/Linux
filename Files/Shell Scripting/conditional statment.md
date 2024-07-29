Conditional statements are essential in shell scripting for making decisions and executing different code blocks based on certain conditions. Here's a detailed guide on how to use conditional statements in shell scripts, including examples with `if`, `elif`, `else`, and `case`.

### Using `if` Statements

#### Basic `if` Statement

```sh
#!/bin/bash

echo "Enter a number: "
read num

if [ $num -gt 10 ]; then
  echo "The number is greater than 10."
fi
```

#### `if-else` Statement

```sh
#!/bin/bash

echo "Enter a number: "
read num

if [ $num -gt 10 ]; then
  echo "The number is greater than 10."
else
  echo "The number is 10 or less."
fi
```

#### `if-elif-else` Statement

```sh
#!/bin/bash

echo "Enter a number: "
read num

if [ $num -gt 10 ]; then
  echo "The number is greater than 10."
elif [ $num -eq 10 ]; then
  echo "The number is equal to 10."
else
  echo "The number is less than 10."
fi
```

### Comparison Operators

Here are some common comparison operators used in `if` statements:

- `-eq` - Equal to
- `-ne` - Not equal to
- `-lt` - Less than
- `-le` - Less than or equal to
- `-gt` - Greater than
- `-ge` - Greater than or equal to

### String Comparisons

String comparisons can be done using `=` and `!=`.

```sh
#!/bin/bash

echo "Enter a string: "
read str

if [ "$str" = "hello" ]; then
  echo "The string is hello."
else
  echo "The string is not hello."
fi
```

### Logical Operators

Logical operators `&&` (AND) and `||` (OR) can be used to combine conditions.

```sh
#!/bin/bash

echo "Enter a number: "
read num

if [ $num -gt 10 ] && [ $num -lt 20 ]; then
  echo "The number is between 10 and 20."
else
  echo "The number is not between 10 and 20."
fi
```

### Using `case` Statements

The `case` statement is useful for handling multiple conditions.

```sh
#!/bin/bash

echo "Enter a letter: "
read letter

case $letter in
  a)
    echo "You entered A."
    ;;
  b)
    echo "You entered B."
    ;;
  c)
    echo "You entered C."
    ;;
  *)
    echo "You entered something else."
    ;;
esac
```

In shell scripting, you can use both single `[` and double `[[` brackets for conditional statements. However, there are differences between them in terms of functionality and syntax. Here’s an explanation of these differences, along with examples:

### Single Bracket `[ ... ]`

The single bracket `[` is the traditional test command in POSIX-compliant shells like `sh` and `bash`. It has certain limitations compared to double brackets.

### Double Bracket `[[ ... ]]`

The double bracket `[[` is a more powerful and flexible conditional expression introduced in `bash` and other modern shells. It supports more complex expressions and offers additional features.

### Differences Between Single and Double Brackets

1. **Logical Operators**:
   - Single brackets `[ ]` use `-a` for AND and `-o` for OR.
   - Double brackets `[[ ]]` use `&&` for AND and `||` for OR.

   ```sh
   # Single Bracket
   if [ $num -gt 5 -a $num -lt 15 ]; then
     echo "The number is between 5 and 15."
   fi

   # Double Bracket
   if [[ $num -gt 5 && $num -lt 15 ]]; then
     echo "The number is between 5 and 15."
   fi
   ```

2. **String Comparison**:
   - Single brackets require quoting variables to prevent word splitting and glob expansion.
   - Double brackets do not require quoting and provide better string comparison operators.

   ```sh
   # Single Bracket
   if [ "$str" = "hello" ]; then
     echo "The string is hello."
   fi

   # Double Bracket
   if [[ $str == "hello" ]]; then
     echo "The string is hello."
   fi
   ```

3. **Pattern Matching**:
   - Double brackets support pattern matching with `==` and `!=` operators.
   - Single brackets do not support pattern matching.

   ```sh
   # Double Bracket
   if [[ $str == h* ]]; then
     echo "The string starts with 'h'."
   fi
   ```

4. **Arithmetic Operations**:
   - Both single and double brackets support arithmetic comparisons, but double brackets provide more features.

   ```sh
   # Single Bracket
   if [ $num -gt 10 ]; then
     echo "The number is greater than 10."
   fi

   # Double Bracket
   if [[ $num -gt 10 ]]; then
     echo "The number is greater than 10."
   fi
   ```

Certainly! Here’s a simplified summary of common `if` flags used in shell scripting with a single example:

### Common `if` Flags

- **`-e`**: Check if a file exists.
- **`-f`**: Check if a file is a regular file.
- **`-d`**: Check if a directory exists.
- **`-s`**: Check if a file exists and is not empty.
- **`-z`**: Check if a string is empty.
- **`-n`**: Check if a string is non-empty.
- **`-w`**: Check if a file is writable.
- **`-r`**: Check if a file is readable.
- **`-x`**: Check if a file is executable.

### Example

Here’s a script that uses several `if` flags to check different conditions:

```sh
#!/bin/bash

filename="example.txt"
string="Hello World"

# Check if the file exists and is not empty
if [ -s "$filename" ]; then
  echo "The file '$filename' exists and is not empty."
else
  echo "The file '$filename' either does not exist or is empty."
fi

# Check if the file is a regular file
if [ -f "$filename" ]; then
  echo "'$filename' is a regular file."
else
  echo "'$filename' is not a regular file."
fi

# Check if the file is writable
if [ -w "$filename" ]; then
  echo "'$filename' is writable."
else
  echo "'$filename' is not writable."
fi

# Check if the string is non-empty
if [ -n "$string" ]; then
  echo "The string is non-empty."
else
  echo "The string is empty."
fi
```

### Summary

This example script demonstrates how to use various `if` flags to check for the existence and properties of a file, as well as the state of a string.

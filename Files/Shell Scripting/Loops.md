Loops in shell scripting, such as `for` and `while`, are commonly used for repetitive tasks. You can combine them with flags (conditions) to control their behavior. Here’s a guide on using `for` and `while` loops with flags in shell scripts.

### `for` Loop

A `for` loop iterates over a list of items or a range of values.

#### Basic Syntax

```sh
for item in list
do
  # commands
done
```

#### Example: Using `for` Loop with Flags

Here’s a script that uses a `for` loop to iterate over a list of files and checks if each file is writable using the `-w` flag.

```sh
#!/bin/bash

files=("file1.txt" "file2.txt" "file3.txt")

for file in "${files[@]}"
do
  if [ -w "$file" ]; then
    echo "$file is writable."
  else
    echo "$file is not writable."
  fi
done
```

### `while` Loop

A `while` loop continues executing as long as its condition evaluates to true.

#### Basic Syntax

```sh
while [ condition ]
do
  # commands
done
```

#### Example: Using `while` Loop with Flags

Here’s a script that uses a `while` loop to read lines from a file and checks if each line contains a specific keyword.

```sh
#!/bin/bash

filename="data.txt"
keyword="important"

# Read the file line by line
while IFS= read -r line
do
  if [[ "$line" == *"$keyword"* ]]; then
    echo "Line contains the keyword '$keyword': $line"
  else
    echo "Line does not contain the keyword '$keyword': $line"
  fi
done < "$filename"
```

### Combining Loops and Flags

You can also combine loops with flags for more complex scenarios. Here’s an example where we use a `while` loop to keep prompting the user until a valid file name is provided:

```sh
#!/bin/bash

valid_file=false

while [ "$valid_file" = false ]
do
  echo "Enter a file name:"
  read filename

  # Check if the file exists and is readable
  if [ -e "$filename" ] && [ -r "$filename" ]; then
    echo "File '$filename' exists and is readable."
    valid_file=true
  else
    echo "File '$filename' does not exist or is not readable. Please try again."
  fi
done
```

### Summary

- **`for` Loop**: Iterates over a list of items or range of values. Use flags inside the loop to check conditions.
- **`while` Loop**: Continues execution while a condition is true. Use flags to control the flow based on file properties or user input.

These loops, combined with flags, provide powerful mechanisms for handling repetitive tasks and conditional logic in shell scripts.

Command-line arguments allow you to pass data to your script when you run it. In shell scripting, these arguments are accessed using special variables. Here's a detailed explanation of how to use command-line arguments in shell scripts.

### Accessing Command-Line Arguments

In a shell script, you can access the command-line arguments using positional parameters:

- `$0` - The name of the script.
- `$1` - The first argument.
- `$2` - The second argument.
- ... and so on.
- `$#` - The number of arguments.
- `$@` - All the arguments as a list.
- `$*` - All the arguments as a single string.

### Example Script Using Command-Line Arguments

Here's an example shell script that demonstrates how to use these special variables:

```sh
#!/bin/bash

# Display script name and arguments
echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"

# Display the number of arguments
echo "Number of arguments: $#"

# Display all arguments
echo "All arguments (as a list): $@"
echo "All arguments (as a single string): $*"
```

Save this script as `args_example.sh` and make it executable:

```bash
chmod +x args_example.sh
```

Now, run the script with some arguments:

```bash
./args_example.sh arg1 arg2 arg3
```

The output will be:

```
Script name: ./args_example.sh
First argument: arg1
Second argument: arg2
Number of arguments: 3
All arguments (as a list): arg1 arg2 arg3
All arguments (as a single string): arg1 arg2 arg3
```

### Using Command-Line Arguments in a Practical Script

Let's create a more practical example: a script that adds two numbers passed as arguments.

```sh
#!/bin/bash

# Check if exactly two arguments are provided
if [ $# -ne 2 ]; then
  echo "Usage: $0 num1 num2"
  exit 1
fi

# Read the arguments
num1=$1
num2=$2

# Perform addition
sum=$((num1 + num2))

# Display the result
echo "The sum of $num1 and $num2 is: $sum"
```

Save this script as `add_numbers.sh` and make it executable:

```bash
chmod +x add_numbers.sh
```

Run the script with two numbers as arguments:

```bash
./add_numbers.sh 5 10
```

The output will be:

```
The sum of 5 and 10 is: 15
```

### Handling Command-Line Arguments with Flags

You can also handle command-line arguments with flags, which is useful for more complex scripts. Here’s an example that uses flags:

```sh
#!/bin/bash

while getopts ":a:b:" opt; do
  case $opt in
    a) num1=$OPTARG ;;
    b) num2=$OPTARG ;;
    \?) echo "Invalid option -$OPTARG" >&2; exit 1 ;;
    :) echo "Option -$OPTARG requires an argument." >&2; exit 1 ;;
  esac
done

# Check if both arguments are provided
if [ -z "$num1" ] || [ -z "$num2" ]; then
  echo "Usage: $0 -a num1 -b num2"
  exit 1
fi

# Perform addition
sum=$((num1 + num2))

# Display the result
echo "The sum of $num1 and $num2 is: $sum"
```

Save this script as `add_numbers_with_flags.sh` and make it executable:

```bash
chmod +x add_numbers_with_flags.sh
```

Run the script with flags:

```bash
./add_numbers_with_flags.sh -a 5 -b 10
```

The output will be:

```
The sum of 5 and 10 is: 15
```

These examples illustrate how to handle command-line arguments in shell scripts, making your scripts more flexible and interactive.

In Linux shell scripting, you can perform arithmetic operations and handle input/output using various built-in features. Here's a comprehensive guide on how to do this:

### Arithmetic Operations

#### Basic Arithmetic with `expr`

The `expr` command can be used for simple arithmetic operations.

```sh
#!/bin/bash

a=5
b=10

sum=$(expr $a + $b)
difference=$(expr $a - $b)
product=$(expr $a \* $b)
quotient=$(expr $b / $a)
remainder=$(expr $b % $a)

echo "Sum: $sum"
echo "Difference: $difference"
echo "Product: $product"
echo "Quotient: $quotient"
echo "Remainder: $remainder"
```

#### Arithmetic with `let`

The `let` command allows arithmetic expansion.

```sh
#!/bin/bash

a=5
b=10

let sum=a+b
let difference=a-b
let product=a*b
let quotient=b/a
let remainder=b%a

echo "Sum: $sum"
echo "Difference: $difference"
echo "Product: $product"
echo "Quotient: $quotient"
echo "Remainder: $remainder"
```

#### Arithmetic with `$(( ))`

The `$(( ))` syntax is a more modern and preferred method for arithmetic operations.

```sh
#!/bin/bash

a=5
b=10

sum=$((a + b))
difference=$((a - b))
product=$((a * b))
quotient=$((b / a))
remainder=$((b % a))

echo "Sum: $sum"
echo "Difference: $difference"
echo "Product: $product"
echo "Quotient: $quotient"
echo "Remainder: $remainder"
```

The `bc` (Basic Calculator) command in Linux is a powerful tool for performing arithmetic operations, especially those involving floating-point numbers, which are not handled well by the shell's built-in arithmetic operators. Here's a guide on how to use `bc` for various arithmetic operations and handling input/output.

### Using `bc` for Arithmetic Operations

#### Basic Usage

You can use `bc` to perform basic arithmetic operations directly from the command line or within a script.

```sh
echo "5 + 10" | bc
```

This command outputs `15`.

#### Floating-Point Arithmetic

For floating-point arithmetic, you can specify the scale (number of decimal places).

```sh
echo "scale=2; 5 / 3" | bc
```

This command outputs `1.66`.

### Using `bc` in a Shell Script

Here’s an example script that uses `bc` to perform arithmetic operations on user inputs.

```sh
#!/bin/bash

# Prompt user for input
echo "Enter two numbers: "
read num1 num2

# Perform arithmetic operations using bc
sum=$(echo "$num1 + $num2" | bc)
difference=$(echo "$num1 - $num2" | bc)
product=$(echo "$num1 * $num2" | bc)
quotient=$(echo "scale=2; $num1 / $num2" | bc)
remainder=$(echo "$num1 % $num2" | bc)

# Display the results
echo "Sum: $sum"
echo "Difference: $difference"
echo "Product: $product"
echo "Quotient: $quotient"
echo "Remainder: $remainder"
```


#### Using `bc` with Mathematical Functions

`bc` supports mathematical functions like `sqrt` and `sine`.

```sh
#!/bin/bash

# Perform square root and sine operations using bc
sqrt_result=$(echo "scale=4; sqrt(16)" | bc)
sine_result=$(echo "scale=4; s(1.57)" | bc -l)

# Display the results
echo "Square root of 16: $sqrt_result"
echo "Sine of 1.57 radians: $sine_result"
```


The `awk`, `tr`, and `comm` commands are powerful tools for text processing and manipulation in Unix-like systems. Here’s a detailed guide on each command:

### `awk` Command

`awk` is a programming language and command-line utility for pattern scanning and processing. It’s particularly useful for handling and analyzing structured text data, like tables or CSV files.

#### Basic Syntax

```sh
awk 'pattern { action }' [file...]
```

#### Common Features

- **Print Specific Columns**

  ```sh
  awk '{ print $1, $3 }' file.txt
  ```

- **Field Separator**

  Use `-F` to specify a field separator. By default, `awk` uses whitespace.

  ```sh
  awk -F, '{ print $1, $2 }' file.csv
  ```

- **Pattern Matching**

  Print lines that match a pattern.

  ```sh
  awk '/pattern/' file.txt
  ```

- **Condition and Action**

  Perform actions based on conditions.

  ```sh
  awk '$3 > 50 { print $1, $3 }' file.txt
  ```

- **Built-in Variables**

  - **`$0`**: The entire line.
  - **`$1`, `$2`, ...**: Fields in the current line.
  - **`NR`**: The number of records (lines) processed.
  - **`NF`**: The number of fields in the current record.

  ```sh
  awk '{ print NR, NF, $1 }' file.txt
  ```

#### Examples

1. **Print the First and Third Columns**

   ```sh
   awk '{ print $1, $3 }' file.txt
   ```

2. **Print Lines Where the Second Field is Greater than 100**

   ```sh
   awk '$2 > 100' file.txt
   ```

3. **Sum Values in the Second Column**

   ```sh
   awk '{ sum += $2 } END { print sum }' file.txt
   ```

4. **Print Lines Matching a Pattern**

   ```sh
   awk '/error/' logfile.txt
   ```

### `tr` Command

`tr` (translate or delete characters) is used to translate or delete characters from the input text.

#### Basic Syntax

```sh
tr [options] set1 [set2]
```

#### Common Options

- **`-d`**: Delete characters in `set1`.

  ```sh
  echo "hello 123" | tr -d '123'
  # Output: hello
  ```

- **`-s`**: Squeeze repeated characters in `set1` into a single character.

  ```sh
  echo "hello     world" | tr -s ' '
  # Output: hello world
  ```

- **`-c`**: Complement the set (invert the set).

  ```sh
  echo "hello 123" | tr -c 'a-zA-Z' '-'
  # Output: hello---
  ```

- **`[:lower:]`** and **`[:upper:]`**: Convert lowercase to uppercase and vice versa.

  ```sh
  echo "hello world" | tr 'a-z' 'A-Z'
  # Output: HELLO WORLD
  ```

#### Examples

1. **Convert Lowercase to Uppercase**

   ```sh
   echo "hello world" | tr 'a-z' 'A-Z'
   # Output: HELLO WORLD
   ```

2. **Delete Digits**

   ```sh
   echo "hello 123" | tr -d '0-9'
   # Output: hello 
   ```

3. **Replace Spaces with Hyphens**

   ```sh
   echo "hello world" | tr ' ' '-'
   # Output: hello-world
   ```

4. **Squeeze Multiple Spaces into a Single Space**

   ```sh
   echo "hello     world" | tr -s ' '
   # Output: hello world
   ```

### `comm` Command

`comm` compares two sorted files line by line and outputs three columns: lines unique to the first file, lines unique to the second file, and lines common to both files.

#### Basic Syntax

```sh
comm [options] file1 file2
```

#### Common Options

- **`-1`**: Suppress the first column (lines unique to file1).

  ```sh
  comm -1 file1.txt file2.txt
  ```

- **`-2`**: Suppress the second column (lines unique to file2).

  ```sh
  comm -2 file1.txt file2.txt
  ```

- **`-3`**: Suppress the third column (lines common to both files).

  ```sh
  comm -3 file1.txt file2.txt
  ```

#### Examples

1. **Compare Two Files**

   ```sh
   comm file1.txt file2.txt
   ```

2. **Show Only Lines Unique to the First File**

   ```sh
   comm -2 -3 file1.txt file2.txt
   ```

3. **Show Only Lines Common to Both Files**

   ```sh
   comm -1 -2 file1.txt file2.txt
   ```

4. **Show Lines Unique to the Second File**

   ```sh
   comm -1 -3 file1.txt file2.txt
   ```

### Summary

- **`awk`**: A powerful text processing language for pattern scanning and data extraction. Supports field manipulation, pattern matching, and custom actions.
- **`tr`**: Translates or deletes characters from the input text. Useful for character substitution, deletion, and squeezing repeated characters.
- **`comm`**: Compares two sorted files and outputs lines unique to each file and lines common to both. Requires sorted input files.

These commands are essential for text manipulation and data processing in Unix-like systems, each offering unique capabilities for handling and analyzing text data.

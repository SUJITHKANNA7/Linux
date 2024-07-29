The `sort`, `cut`, and `uniq` commands are fundamental tools in Unix-like systems for processing and manipulating text files. Here’s a detailed guide on each command:

### `sort` Command

The `sort` command sorts lines of text files. It supports various options to customize the sorting behavior.

#### Basic Syntax

```sh
sort [options] [file...]
```

#### Common Options

- **`-n`**: Sort numerically.
  
  ```sh
  sort -n file.txt
  ```

- **`-r`**: Reverse the order (sort in descending order).
  
  ```sh
  sort -r file.txt
  ```

- **`-k`**: Specify the key (column) to sort by. For example, `-k2` sorts by the second column.

  ```sh
  sort -k2 file.txt
  ```

- **`-t`**: Specify the field delimiter (e.g., `-t,` for CSV files).

  ```sh
  sort -t, -k2 file.csv
  ```

- **`-u`**: Output only unique lines (removes duplicates).

  ```sh
  sort -u file.txt
  ```

#### Examples

1. **Sort Alphabetically**

   ```sh
   sort file.txt
   ```

2. **Sort Numerically**

   ```sh
   sort -n numbers.txt
   ```

3. **Sort by Specific Column**

   ```sh
   sort -t, -k2 file.csv
   ```

4. **Sort and Remove Duplicates**

   ```sh
   sort -u file.txt
   ```

### `cut` Command

The `cut` command is used to extract sections from each line of files. It’s useful for working with columns of data.

#### Basic Syntax

```sh
cut [options] [file...]
```

#### Common Options

- **`-f`**: Specify the fields (columns) to extract, with fields delimited by the `-d` option.
  
  ```sh
  cut -f1,3 -d, file.csv
  ```

- **`-d`**: Specify the delimiter character (e.g., `-d,` for CSV files).

  ```sh
  cut -d, -f1,2 file.csv
  ```

- **`-c`**: Specify the character positions to extract.

  ```sh
  cut -c1-5 file.txt
  ```

#### Examples

1. **Extract Specific Fields**

   ```sh
   cut -f1,2 -d, file.csv
   ```

2. **Extract Character Positions**

   ```sh
   cut -c1-5 file.txt
   ```

3. **Extract Fields from a Tab-Delimited File**

   ```sh
   cut -f1,3 file.txt
   ```

### `uniq` Command

The `uniq` command filters out repeated lines from sorted input. It’s commonly used in conjunction with `sort`.

#### Basic Syntax

```sh
uniq [options] [file...]
```

#### Common Options

- **`-c`**: Prefix lines with the number of occurrences.

  ```sh
  uniq -c file.txt
  ```

- **`-d`**: Only print duplicate lines.

  ```sh
  uniq -d file.txt
  ```

- **`-u`**: Only print unique lines (lines that are not repeated).

  ```sh
  uniq -u file.txt
  ```

#### Examples

1. **Remove Duplicate Lines**

   ```sh
   sort file.txt | uniq
   ```

2. **Count Occurrences of Each Line**

   ```sh
   sort file.txt | uniq -c
   ```

3. **Print Only Duplicates**

   ```sh
   sort file.txt | uniq -d
   ```

4. **Print Only Unique Lines**

   ```sh
   sort file.txt | uniq -u
   ```

### Summary

- **`sort`**: Sorts lines of text files. Options include sorting numerically (`-n`), reversing order (`-r`), specifying a key (`-k`), and removing duplicates (`-u`).
  
- **`cut`**: Extracts sections from each line of files. Options include specifying fields (`-f`) and delimiters (`-d`), or character positions (`-c`).

- **`uniq`**: Filters out repeated lines from sorted input. Options include counting occurrences (`-c`), printing only duplicates (`-d`), and printing only unique lines (`-u`).

These commands are powerful tools for text processing and data manipulation in Unix-like systems, and they can be used in combination to perform complex data transformations efficiently.

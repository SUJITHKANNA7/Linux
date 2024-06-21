### Basic commands and Navigation  

1. **ls** (list directory contents):
   - `-l`: Long listing format (displays detailed information).
   - `-a`: Include hidden files (files starting with `.`).
   - `-h`: Human-readable sizes (e.g., 1K, 234M, 2G).
   - `-r`: Reverse print
   - `-t`: Time based sort

   Example: `ls -lha`

2. **cd** (change directory):
   - No commonly used flags, but `cd -` switches to the previous directory.
     
   Example: `cd /path/to/directory`

3. **pwd** (print working directory):
   - No commonly used flags.

   Example: `pwd`

4. **cp** (copy files and directories):
   - `-r`: Copy directories recursively.
   - `-i`: Prompt before overwriting existing files.

   Example: `cp -ri source destination`

5. **mv** (move/rename files and directories):
   - `-i`: Prompt before overwriting existing files (when moving).
   - `-b`: Create a backup of each existing destination file (when moving).

   Example: `mv -i source destination`

6. **rm** (remove/delete files and directories):
   - `-r`: Remove directories and their contents recursively.
   - `-f`: Force removal without confirmation.

   Example: `rm -rf directory`

7. **mkdir** (make directories):
   - `-p`: Create parent directories if they don't exist.

   Example: `mkdir -p /path/to/new/directory`

8. **rmdir** (remove empty directories):
   - No commonly used flags.

   Example: `rmdir directory`

9. **cat** (concatenate and display files):
   - `-n`: Number all output lines.
   - `-b`: Number non-empty output lines.

   Example: `cat -n file.txt`

10. **head** (output the first part of files):
    - `-n`: Specify number of lines to display (e.g., `-n 10`).

    Example: `head -n 10 file.txt`

11. **tail** (output the last part of files):
    - `-n`: Specify number of lines to display (e.g., `-n 20`).

    Example: `tail -n 20 file.txt`

Certainly! Here's a breakdown of each command and its primary use in Linux:

12. **diff**:
   - **Purpose**: `diff` is used to compare files line by line and display the differences between them.
   - **Syntax**: `diff [options] file1 file2`
   - **Commonly used options**:
     - `-u` or `-U NUM`: Unified format, shows NUM lines of context around each change.
     - `-r` or `-R`: Recursively compare directories.
     - `-q`: Report only whether files differ, not the details.
     - `-i`: Ignore case differences.
     - `-w`: Ignore all white space.
       

13. **Others**:
  - Use `diff` when you need to compare files or directories and see detailed differences.
  - Use `less` when you want to view the content of a file and navigate through it interactively.
  - Use `more` when you want a basic way to view a file's content, especially for files that fit within a single screen.


# *nix terminal commands cheat sheet

Some notes:

  - Anything in angle brackets (`<>`) denotes an argument that you are supposed to provide for the command
  - Anything denoted like `$SOME_VAL` refers to an [environment or shell variable](https://askubuntu.com/questions/26318/environment-variable-vs-shell-variable-whats-the-difference) \[1\]
  - I've tried to make this as OS-agnostic as possible, but I don't guarantee that there won't be subtle differences
  - Generally speaking, most command flags can be combined
  - Suggestions for improvement are always welcome
  - Goals
    - Provide a _basic_ reference for those who are new to or infrequent users of Unix/Linux/BSD-based terminals
    - Help those who are starting from zero become proficient *nix command-line users by providing a gentle introduction to (some of) the most commonly used commands and useful options 
  - Non-goals
    - This is not meant to be a thorough guide or tutorial.
    - This is not a guide to the best way to accomplish a given task. The nature of the *nix ecosystem is such that, more often than not, there are multiple (but often subtly different) ways of accomplishing the same thing. For any non-trivial tasks, particularly those in which performance or portability are critical, you are advised to do your own research on the pros and cons of various utilities

## Navigation

- `cd <DIR>`: change working (current) directory
  - `cd ~` or `cd` by itself: go to your home directory (defined in `$HOME`)
  - `cd ..`: go to the current working directory's parent directory
  - `cd -`: go to the directory you were previously in
- `pwd`: print working directory
- `ls <DIR>`: list directory contents
  - `ls`: list contents of the current directory
  - `ls -l`: list contents with the long format
    - The long format listing includes:
      - file types
      - permissions
      - hard links
      - owner
      - group
      - last-modified date & time
      - name
  - `ls -a`: list all directory contents, including [dotfiles](https://www.freecodecamp.org/news/dotfiles-what-is-a-dot-file-and-how-to-create-it-in-mac-and-linux/)
  - `ls -h`: show file sizes in a human-readable format (i.e., show size units instead of the number of bytes)
  - `ls -F`: append `/` to directories' names and `*` to executables

## File and Directory creation

  - `mkdir <DIR>`: create a new directory
    - `mkdir -p <PARENT_DIR_NAME>/<CHILD_DIR_NAME>`: create a new directory and its parent if it doesn't exist
    - `mkdir -v <DIR>`: verbose; print a message after the creation of each directory
  - `touch <FILE_NAME>`: often used to create a new file, this actually changes the modification and access times of a file

## Text Searching and Manipulation

  - `tail <FILE_NAME>`: prints the last 10 lines of a file
    - `tail -n <N> <FILE_NAME>`: prints the last `<N>` lines of a file
    - `tail -f <FILE_NAME>`: prints the last 10 (or `<N>`, if `-n` is specified) and any newly appended lines. Use `ctrl-c` to quit.
  - `grep <STRING_OR_REGEX> <FILE_NAME>`: prints each line in which a string or [regular expression](https://en.wikipedia.org/wiki/Regular_expression) exists
    - `grep -i <STRING_OR_REGEX> <FILE_NAME>`: prints each line in which a string or pattern exists, but case-insensitive
    - `grep -v <STRING_OR_REGEX> <FILE_NAME>`: excludes lines containing the string/pattern
    - `grep -e <REGEX> <FILE_NAME>`: used for specifying a regex. only necessary if searching for multiple patterns or patterns beginning with a dash `-`
    - `grep -E <REGEX> <FILE_NAME>`: interpret the pattern as an [extended regex](https://en.wikibooks.org/wiki/Regular_Expressions/POSIX-Extended_Regular_Expressions). This is the same as `egrep`'s behavior
    - `grep -n <STRING_OR_REGEX> <FILE_NAME>`: show the line number of each match
  - `cat <FILE_NAME>`: print the contents of one or more files. If more than one file is specified, the output is the concatenated contents. Note: It is _not_ necessary to `cat` a file and pipe its contents to `grep` if you wish to search it.
  - `diff <FILE1> <FILE2>`: compares and displays the differences between two files _on a line-by-line basis_
    - how to read the output\[2\]:
      - `<` refers to `FILE1`'s lines
      - `>` refers to `FILE2`'s lines
      - All text fitting this pattern: `2d3,6` are commands that the `patch` command can use to reconcile the differences between two files. This is a breakdown of how to interpret it:
        - The first number refers to the line number(s) in `FILE1` in which the string appears
        - The second number refers to the corresponding line number(s) in `FILE2`
        - The letter is one of these:
          - `a`: add the lines in the range denoted by the last number(s) in `FILE2` after the line denoted by the first number. E.g., 1a4,10 means that lines 4-10 in `FILE2` are to be added _after_ line 1 in `FILE1`.
          - `c`: replace the line(s) in `FILE1` with the line(s) in `FILE2`
          - `d`: delete the line(s) in `FILE1`. `FILE2`'s line numbers are where that/those line(s) would be if they existed in that file


Sources:
\
\[1\] [https://askubuntu.com/questions/26318/environment-variable-vs-shell-variable-whats-the-difference](https://askubuntu.com/questions/26318/environment-variable-vs-shell-variable-whats-the-difference)
\
\[2\] [https://www.math.utah.edu/docs/info/diff_3.html#SEC13](https://www.math.utah.edu/docs/info/diff_3.html#SEC13)
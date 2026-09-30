# 🧠 Shell Scripting Quiz

> Practice questions with answers hidden. Click **Show answer** to check yourself.

- [Day 1 - Shell Scripting Fundamentals](#day-1---shell-scripting-fundamentals)
- [Day 2 - Shell Scripting Advanced](#day-2---shell-scripting-advanced)

---

## Day 1 - Shell Scripting Fundamentals

### Q1. A script needs to check for the existence of a configuration directory before proceeding. Which conditional statement correctly performs this check?

- A) `if [ -f /etc/config ]; then ... fi`
- B) `if [ -s /etc/config ]; then ... fi`
- C) `if [ dir /etc/config ]; then ... fi`
- D) `if [ -d /etc/config ]; then ... fi`

<details>
<summary>Show answer</summary>

**Answer: D)** `if [ -d /etc/config ]; then ... fi`

</details>

### Q2. Why is the Shebang line important in DevOps?

- A) It makes the script run faster
- B) It grants root permissions
- C) It ensures portability by telling the system which interpreter to use
- D) It creates the documentation

<details>
<summary>Show answer</summary>

**Answer: C)** It ensures portability by telling the system which interpreter to use

</details>

### Q3. How do you limit the scope of a variable to exist only inside a function?

- A) `private VAR`
- B) `local VAR`
- C) `static VAR`
- D) `const VAR`

<details>
<summary>Show answer</summary>

**Answer: B)** `local VAR`

</details>

### Q4. Which loop syntax is correct for iterating over a list?

- A) `for (item in list) do ... done`
- B) `for item in list; do ... done`
- C) `foreach item in list do ... done`
- D) `for item = list do ... done`

<details>
<summary>Show answer</summary>

**Answer: B)** `for item in list; do ... done`

</details>

### Q5. In a deployment script, which of the following is the correct syntax for assigning the output of the `date` command to a variable named `TIMESTAMP`?

- A) `TIMESTAMP = $(date)`
- B) ``let TIMESTAMP = `date``
- C) `TIMESTAMP=$(date)`
- D) `TIMESTAMP=date`

<details>
<summary>Show answer</summary>

**Answer: C)** `TIMESTAMP=$(date)`

> No spaces around `=` in Bash.

</details>

### Q6. How do you access/print the value of the variable `PORT` defined above?

- A) `echo $PORT`
- B) `print(PORT)`
- C) `echo PORT`
- D) `echo %PORT%`

<details>
<summary>Show answer</summary>

**Answer: A)** `echo $PORT`

</details>

### Q7. How do you increment a counter variable in a while loop?

- A) `COUNT + 1`
- B) `increment COUNT`
- C) `COUNT = COUNT + 1`
- D) `((COUNT++))`

<details>
<summary>Show answer</summary>

**Answer: D)** `((COUNT++))`

</details>

### Q8. What command displays the shell you are currently using?

- A) `whoami`
- B) `echo $SHELL`
- C) `which bash`
- D) `ls shell`

<details>
<summary>Show answer</summary>

**Answer: B)** `echo $SHELL`

</details>

### Q9. What is the primary purpose of using `set -u` at the beginning of a production script?

- A) Print each command to the terminal before it is executed for debugging
- B) Ensure that errors within a pipeline are properly caught
- C) Treat unset variables as an error & exit, preventing potentially dangerous operations
- D) Cause the script to exit immediately if a command fails

<details>
<summary>Show answer</summary>

**Answer: C)** Treat unset variables as an error & exit, preventing potentially dangerous operations

</details>

### Q10. What does the flag `-d` check for in a conditional statement?

- A) If a file exists
- B) If the item is a directory
- C) If the file is executable
- D) If the file is empty

<details>
<summary>Show answer</summary>

**Answer: B)** If the item is a directory

</details>

### Q11. A junior engineer uses the command `grep "ERROR" syslog > error_log.txt` in a daily script to log server errors. Why does `error_log.txt` only contain errors from the most recent run?

- A) Redirection operator `>>` should have been used instead of `>`
- B) Pipe `|` should have been used instead of `>`
- C) Standard error (`2>&1`) was not redirected
- D) `grep` command does not support writing to files directly

<details>
<summary>Show answer</summary>

**Answer: A)** Redirection operator `>>` should have been used instead of `>`

> `>` overwrites the file every run. `>>` appends.

</details>

### Q12. How do you explicitly stop a script and indicate failure?

- A) `stop`
- B) `return false`
- C) `exit 1`
- D) `break`

<details>
<summary>Show answer</summary>

**Answer: C)** `exit 1`

</details>

### Q13. How do you write "OR" logic in a Bash `if` statement?

- A) `||`
- B) `OR`
- C) `&&`
- D) `|`

<details>
<summary>Show answer</summary>

**Answer: A)** `||`

</details>

### Q14. A script named `create_user.sh` is executed with the command: `./create_user.sh admin dev`. Inside the script, what does the special variable `$#` contain?

- A) First argument, `admin`
- B) Total number of arguments passed, which is 2
- C) Name of the script, `create_user.sh`
- D) All arguments as a single string, `admin dev`

<details>
<summary>Show answer</summary>

**Answer: B)** Total number of arguments passed, which is 2

</details>

### Q15. How do you redirect Standard Error to the same destination as Standard Output?

- A) `1>2`
- B) `error >> output`
- C) `|&`
- D) `2>&1`

<details>
<summary>Show answer</summary>

**Answer: D)** `2>&1`

</details>

---

## Day 2 - Shell Scripting Advanced

### Q1. What is the correct way to write the numerical comparison `if [ $count > 5 ]` in Bash to prevent it from creating an empty file named `5`?

- A) `if ($count > 5)`
- B) `if [ $count -gt 5 ]`
- C) `if [[ $count > 5 ]]`
- D) `if test $count > 5`

<details>
<summary>Show answer</summary>

**Answer: B)** `if [ $count -gt 5 ]`

> Inside `[ ]`, `>` is treated as a redirect, so it creates a file named `5`. Use `-gt` for numeric comparison.

</details>

### Q2. In the context of DevOps, why are shell scripts often described as the "glue" that connects different tools?

- A) Because Bash scripts are compiled into a universal format that all DevOps tools can understand
- B) Because they are used to automate the sequence of operations between various tools, such as build, test, and deployment tools
- C) Because they provide a graphical user interface (GUI) for managing servers
- D) Because they are the only way to install new software on a Linux server

<details>
<summary>Show answer</summary>

**Answer: B)** Because they are used to automate the sequence of operations between various tools, such as build, test, and deployment tools

</details>

### Q3. How do you declare an associative array in Bash?

- A) `declare -A array`
- B) `array=()`
- C) `declare -a array`
- D) `typeset -A array`

<details>
<summary>Show answer</summary>

**Answer: A)** `declare -A array`

> Capital `-A` = associative array (key-value). Small `-a` = indexed array.

</details>

### Q4. In production scripts, why is `set -u` critical when using `rm -rf $DIRECTORY/`?

- A) Improves performance
- B) Prevents deleting root directory if `DIRECTORY` is unset
- C) Enables debugging
- D) Makes script faster

<details>
<summary>Show answer</summary>

**Answer: B)** Prevents deleting root directory if `DIRECTORY` is unset

> If `DIRECTORY` is empty, the command becomes `rm -rf /`. `set -u` stops the script instead.

</details>

### Q5. What is the primary benefit of using functions in a complex shell script?

- A) Functions are the only way to accept arguments into a shell script
- B) Functions run significantly faster than the same code outside a function
- C) Functions automatically handle errors for the code they contain
- D) Functions allow for code reuse & improve script readability and maintainability

<details>
<summary>Show answer</summary>

**Answer: D)** Functions allow for code reuse & improve script readability and maintainability

</details>

### Q6. In a function, what's the difference between `$1` inside vs outside the function?

- A) No difference
- B) Inside function: function's first argument. Outside: script's first argument
- C) Inside function refers to script arguments
- D) Functions can't use `$1`

<details>
<summary>Show answer</summary>

**Answer: B)** Inside function: function's first argument. Outside: script's first argument

</details>

### Q7. Why is it important to check if a directory exists before creating it?

- A) To ensure idempotency
- B) To save battery life
- C) To rename the directory
- D) To delete the directory

<details>
<summary>Show answer</summary>

**Answer: A)** To ensure idempotency

> Idempotent script = running it many times gives the same result without errors.

</details>

### Q8. What happens if you check `$?` two commands later?

- A) Gets the original exit code
- B) Gets average of all exit codes
- C) Only holds exit code of the immediately preceding command
- D) Always returns 0

<details>
<summary>Show answer</summary>

**Answer: C)** Only holds exit code of the immediately preceding command

</details>

### Q9. In `if [[ "$STATUS" == "success" ]]; then`, why quote `"$STATUS"`?

- A) Enables case-insensitive matching
- B) Handles values with spaces or special characters
- C) Makes comparison faster
- D) Required syntax

<details>
<summary>Show answer</summary>

**Answer: B)** Handles values with spaces or special characters

</details>

### Q10. In the context of "Command Substitution," what is the specific function of the `$(command)` syntax?

- A) It runs the command in the background
- B) It stores the output of the command into a variable
- C) It verifies if the command exists
- D) It redirects errors to a log file

<details>
<summary>Show answer</summary>

**Answer: B)** It stores the output of the command into a variable

</details>

### Q11. Regarding conditional syntax, why does the text recommend `[[ ... ]]` over the older `[ ... ]` syntax?

- A) It is the modern, powerful Bash version
- B) It is faster
- C) It allows you to skip quoting variables
- D) It uses less memory

<details>
<summary>Show answer</summary>

**Answer: A)** It is the modern, powerful Bash version

</details>

### Q12. Which command makes a variable available to child scripts or processes?

- A) `set`
- B) `define`
- C) `export`
- D) `global`

<details>
<summary>Show answer</summary>

**Answer: C)** `export`

</details>

### Q13. Why should you always quote variables in file operations (e.g., `"$VAR"`)?

- A) To make them bold
- B) To handle filenames containing spaces
- C) To convert them to strings
- D) It is optional

<details>
<summary>Show answer</summary>

**Answer: B)** To handle filenames containing spaces

</details>

### Q14. Which external tool does the text explicitly mention for scanning code for syntax errors and bad practices?

- A) LintBash
- B) DebuggerPro
- C) ShellCheck
- D) BashDoctor

<details>
<summary>Show answer</summary>

**Answer: C)** ShellCheck

</details>

### Q15. In the "Environment Variables" section, what command is used to display all current environment variables?

- A) `showall`
- B) `list-env`
- C) `printenv`
- D) `echo $ALL`

<details>
<summary>Show answer</summary>

**Answer: C)** `printenv`

</details>

---

⭐ If this quiz helped you, give the repo a star!

# 🐚 Shell Scripting Notes for DevOps

> Beginner-friendly Bash scripting notes with simple explanations, code examples, real-world use cases and common mistakes.

## 📑 Table of Contents

1. [What is Shell & Bash](#1-what-is-shell--bash)
2. [How a Shell Script Works](#2-how-a-shell-script-works)
3. [Script Structure & Shebang](#3-script-structure--shebang)
4. [Variables](#4-variables)
5. [Input & Arguments](#5-input--arguments)
6. [Conditionals (if, else)](#6-conditionals-if-else)
7. [Loops (for, while)](#7-loops-for-while)
8. [Functions](#8-functions)
9. [File & Directory Checks](#9-file--directory-checks)
10. [Exit Codes](#10-exit-codes)
11. [Pipes & Redirects](#11-pipes--redirects)
12. [Environment Variables](#12-environment-variables)
13. [Debugging Scripts](#13-debugging-scripts)
14. [Cron Jobs & Scheduling](#14-cron-jobs--scheduling)
15. [Writing Production-Safe Scripts](#15-writing-production-safe-scripts)

---

## 1. What is Shell & Bash

### 1. Simple Explanation

Think of the "Shell" as the steering wheel and dashboard of your computer's operating system. Instead of clicking icons (GUI), you type text commands to tell the computer what to do. "Bash" (Bourne Again Shell) is a specific brand of shell, just like Chrome is a specific brand of web browser. It is the most common language used to talk to Linux servers.

### 2. Why This Matters in DevOps

Bash is the "glue" of DevOps. It connects different tools together. You use it to navigate servers, install software, run tests, and manage cloud infrastructure. If you are managing a Linux server, you are likely using Bash.

### 3. Key Concepts

- **Shell:** A command-line interpreter that processes commands.
- **Bash:** The default shell on most Linux distributions (Ubuntu, CentOS) and older macOS versions.
- **Terminal:** The window where you type shell commands.

### 4. Visual / Diagram Explanation

```
User (Types command)
   ↓
Terminal (Accepts input)
   ↓
Shell/Bash (Interprets command)
   ↓
Operating System Kernel (Executes hardware task)
   ↓
Output displayed to User
```

### 5. Code Examples

```bash
# This is a basic command entered in the terminal
echo "Hello, DevOps!"

# Check which shell you are currently using
echo $SHELL
```

### 6. Real-World Example

A DevOps engineer logs into a remote AWS EC2 server using a terminal to manually restart a crashed web server using Bash commands.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Confusing the terminal (the window) with the shell (the program running inside).
  - ✅ **Correction:** You can run different shells (like Zsh or Sh) inside the same terminal window. Bash is just the software interpreting your typing.

### 8. Quick Revision Summary

- Shell is the interface to the OS.
- Bash is the most popular shell for Linux.
- It is a text-based command processor.
- It bridges the user and the Kernel.

---

## 2. How a Shell Script Works

### 1. Simple Explanation

A shell script is simply a text file containing a list of commands you want the computer to run, one after another. Instead of typing `update system`, then `download file`, then `move file` manually every time, you save them in a file. Running the file runs all the commands automatically.

### 2. Why This Matters in DevOps

**Automation.** If you have to do a task more than once, write a script. DevOps engineers use scripts to spin up environments, deploy apps, and patch systems without human intervention.

### 3. Key Concepts

- **Interpreter:** Bash reads the file top-to-bottom and executes lines sequentially.
- **Execution:** Scripts are interpreted, not compiled (unlike C++ or Java).
- **Automation:** Turning manual steps into a repeatable process.

### 4. Visual / Diagram Explanation

```
Script File (myscript.sh)
   ↓
Bash Interpreter reads Line 1 → Executes Line 1
   ↓
Reads Line 2 → Executes Line 2
   ↓
... → End of File → Exit
```

### 5. Code Examples

```bash
# This is how you run a script
bash myscript.sh

# Alternatively, if the file is executable
./myscript.sh
```

### 6. Real-World Example

A "setup script" that runs automatically when a new server starts, installing Docker, setting up firewalls, and creating user accounts so the server is ready for use immediately.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Thinking scripts run all commands at once.
  - ✅ **Correction:** They run sequentially. If line 1 takes 10 minutes, line 2 waits 10 minutes.

### 8. Quick Revision Summary

- Scripts are text files with commands.
- Executed line-by-line.
- Used to automate manual tasks.
- Files usually end in `.sh`.

---

## 3. Script Structure & Shebang

### 1. Simple Explanation

The "Shebang" is the very first line of a script that looks like `#!`. It tells the computer exactly which language interpreter to use (e.g., "Use Bash to read this"). Without it, the computer guesses, which can cause errors.

### 2. Why This Matters in DevOps

**Portability.** You might write a script on your laptop, but it needs to run on a Jenkins CI server. The shebang ensures the server knows how to run your code, even if its default settings are different.

### 3. Key Concepts

- **`#!/bin/bash`:** The standard shebang line forcing the script to use Bash.
- **Permissions:** Scripts must be made "executable" to run directly.
- **Comments:** Lines starting with `#` are ignored by the computer but help humans understand the code.

### 4. Visual / Diagram Explanation

```
File Header (#!/bin/bash)
   ↓
Comments (Human readable context)
   ↓
Code (The actual logic)
```

### 5. Code Examples

```bash
#!/bin/bash
# This is a comment. The computer ignores this line.
# The line above (shebang) tells Linux to use Bash.

echo "The script is starting..."
```

**To make it executable:**

```bash
chmod +x myscript.sh
./myscript.sh
```

### 6. Real-World Example

A deployment script explicitly uses `#!/bin/bash` because it uses specific Bash features (like arrays) that would crash if the system tried to run it using the older, simpler `sh` shell.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Putting the shebang on the second line.
  - ✅ **Correction:** The shebang **MUST** be line #1.
- ❌ **Mistake:** Forgetting `chmod +x`.
  - ✅ **Correction:** You cannot run `./script.sh` until you grant execute permissions.

### 8. Quick Revision Summary

- Start scripts with `#!/bin/bash`.
- Use `#` for comments.
- Use `chmod +x filename.sh` to make it runnable.
- Shebang ensures the correct interpreter is used.

---

## 4. Variables

### 1. Simple Explanation

Variables are like labeled boxes where you store information. You can label a box "FILENAME" and put "data.txt" inside it. Later, whenever you need that file, you just refer to the box "FILENAME".

### 2. Why This Matters in DevOps

**Flexibility.** Instead of hardcoding "server-1" in 50 places in your script, you use a variable `SERVER_NAME`. When you move to "server-2", you only change the variable once at the top of the file.

### 3. Key Concepts

- **Assignment:** `VAR=value` (No spaces allowed around the `=`).
- **Access:** `$VAR` or `${VAR}` to read the value.
- **Command Substitution:** Storing the output of a command in a variable using `$(command)`.

### 4. Visual / Diagram Explanation

```
Create Box (NAME="John")
   ↓
Store Data
   ↓
Retrieve Data (echo $NAME)
   ↓
Output ("John")
```

### 5. Code Examples

```bash
#!/bin/bash

# Assigning a string to a variable (NO spaces around =)
APP_NAME="MyApp"
PORT=8080

# Using the variable
echo "Starting $APP_NAME on port $PORT"

# Storing command output (Dynamic variable)
CURRENT_DATE=$(date)
echo "Server started at: $CURRENT_DATE"
```

### 6. Real-World Example

Defining `BACKUP_DIR="/var/backups"` at the top of a backup script. If the backup location changes, you update one line instead of rewriting the whole script.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** `NAME = "John"` (Spaces around equal sign).
  - ✅ **Correction:** Bash interprets `NAME` as a command. Must be `NAME="John"`.
- ❌ **Mistake:** Forgetting the `$` when reading.
  - ✅ **Correction:** `echo NAME` prints the word "NAME". `echo $NAME` prints the value inside.

### 8. Quick Revision Summary

- `KEY=value` to set.
- `$KEY` to get.
- No spaces around `=`.
- `$(command)` saves command output to a variable.

---

## 5. Input & Arguments

### 1. Simple Explanation

Arguments allow you to pass information to a script right when you run it, like handing ingredients to a chef before they start cooking. You can also pause the script to ask the user a question.

### 2. Why This Matters in DevOps

**Reusability.** A single deployment script can deploy to "Dev", "Stage", or "Prod" depending on the argument you pass it (e.g., `./deploy.sh prod`).

### 3. Key Concepts

- **Positional Parameters:** `$1` (first argument), `$2` (second argument).
- **`$0`:** The name of the script itself.
- **`$#`:** The total number of arguments passed.
- **`read`:** Prompts the user for interactive input.

### 4. Visual / Diagram Explanation

```
Run Command (./script.sh user1)
   ↓
Script maps "user1" to variable $1
   ↓
Script uses $1 in logic
```

### 5. Code Examples

```bash
#!/bin/bash

# Using arguments passed when running the script
# Run this as: ./script.sh filename.txt
echo "Deploying file: $1"

# Interactive input
echo "Are you sure? (y/n)"
read CONFIRMATION
echo "User entered: $CONFIRMATION"
```

### 6. Real-World Example

A user creation script `create_user.sh` that takes a username as an argument: `./create_user.sh john_doe`. The script uses `$1` to create the user "john_doe".

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Assuming an argument exists without checking.
  - ✅ **Correction:** Check that the argument is provided (using `if`) before using it to prevent errors.

### 8. Quick Revision Summary

- `$1`, `$2` access command line arguments.
- `$@` means "all arguments".
- `read` accepts keyboard input.
- `$#` counts the arguments.

---

## 6. Conditionals (if, else)

### 1. Simple Explanation

This is the logic of your script. "If this happens, do that; otherwise, do this." It allows the script to make decisions based on success, failure, or specific values.

### 2. Why This Matters in DevOps

**Safety checks.** "If the directory exists, clean it. If not, create it." or "If the tests fail, stop the deployment immediately."

### 3. Key Concepts

- **Syntax:** `if [ condition ]; then ... fi`
- **Test Command:** `[[ ... ]]` is the modern, powerful Bash version of `[ ... ]`.
- **Operators:** `-eq` (equal numbers), `==` (equal strings), `-lt` (less than).

### 4. Visual / Diagram Explanation

```
Start
   ↓
Check Condition (if)
   ├── True?  → Execute "then" block
   └── False? → Execute "else" block
   ↓
Continue
```

### 5. Code Examples

```bash
#!/bin/bash

COUNT=10

# Numeric comparison
if [[ $COUNT -gt 5 ]]; then
    echo "Count is greater than 5"
else
    echo "Count is small"
fi

# String comparison
STATUS="error"
if [[ "$STATUS" == "success" ]]; then
    echo "Great job!"
else
    echo "Something went wrong."
fi
```

### 6. Real-World Example

Checking if a user is "root" before running a system update. If the user ID is not `0` (root), the script exits with an error message preventing permission issues.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Forgetting spaces inside the brackets. `[$a -eq $b]` fails.
  - ✅ **Correction:** Must be `[ $a -eq $b ]`.
- ❌ **Mistake:** Using `>` for numbers (which redirects output).
  - ✅ **Correction:** Use `-gt` (greater than) for numbers in single brackets.

### 8. Quick Revision Summary

- `if [[ condition ]]; then ... fi`
- Spaces inside brackets are mandatory.
- `-eq`, `-gt` for numbers.
- `==`, `!=` for strings.

---

## 7. Loops (for, while)

### 1. Simple Explanation

Loops let you repeat a task multiple times. "For every file in this folder, upload it." "While the server is starting, wait."

### 2. Why This Matters in DevOps

**Batch processing.** Backing up 50 databases, restarting 10 microservices, or waiting for a cloud resource to become available (polling).

### 3. Key Concepts

- **For Loop:** Iterates over a defined list (e.g., list of files, numbers 1-10).
- **While Loop:** Continues running *as long as* a condition is true.
- **Until Loop:** Continues running *until* a condition becomes true.

### 4. Visual / Diagram Explanation

```
Check Condition → Yes? (Run Code) → Repeat
                → No?  (Exit Loop)
```

### 5. Code Examples

```bash
#!/bin/bash

# FOR LOOP: Iterating over a list
# Useful for processing lists of servers or files
NAMES="ServerA ServerB ServerC"
for NAME in $NAMES; do
    echo "Pinging $NAME..."
done

# WHILE LOOP: Running while a condition is true
# Useful for waiting for a process
COUNT=1
while [[ $COUNT -le 3 ]]; do
    echo "Attempt $COUNT..."
    ((COUNT++))
done
```

### 6. Real-World Example

A loop that iterates through all `.log` files and compresses them one by one to save disk space.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Creating infinite loops (forgetting to update the counter in a `while` loop).
  - ✅ **Correction:** Ensure logic exists to eventually break the loop.
- ❌ **Mistake:** Looping over `ls` output (`for f in $(ls)`).
  - ✅ **Correction:** Use globbing: `for f in *.txt`.

### 8. Quick Revision Summary

- `for var in list; do ... done`
- `while [ cond ]; do ... done`
- Use loops for repetitive tasks.
- Avoid looping over `ls`.

---

## 8. Functions

### 1. Simple Explanation

Functions are reusable mini-scripts inside your main script. Instead of writing the same 5 lines of code to "LogError" every time something fails, you write it once as a function and call it by name.

### 2. Why This Matters in DevOps

**Maintainability and modularity.** If you need to change how logging works, you change it in one function, not in 20 places in your script. It makes complex deployment scripts readable.

### 3. Key Concepts

- **Definition:** `my_func() { ... }`
- **Parameters:** Functions have their own `$1`, `$2`.
- **Local Variables:** Use `local` to keep variables inside the function safe from the rest of the script.

### 4. Visual / Diagram Explanation

```
Main Script
   ↓
Call deploy_app
   ↓
Jump to Function Code → Execute Function
   ↓
Return to Main Script
```

### 5. Code Examples

```bash
#!/bin/bash

# Define the function
check_status() {
    local SERVICE=$1
    echo "Checking status of $SERVICE..."
    # logic to check service
}

# Call the function
check_status "nginx"
check_status "mysql"
```

### 6. Real-World Example

A `cleanup()` function defined at the top of a script that removes temporary files. This function is called at the end of the script **AND** if the script crashes, ensuring no garbage is left behind.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Using `function functionName` syntax.
  - ✅ **Correction:** Just use `functionName() { ... }` for maximum compatibility.
- ❌ **Mistake:** Forgetting that `$1` inside a function is the function's argument, not the script's argument.

### 8. Quick Revision Summary

- `name() { commands; }`
- Use `local` for variables inside functions.
- Functions make code reusable (DRY).
- Call them just like commands.

---

## 9. File & Directory Checks

### 1. Simple Explanation

Before trying to read a file or enter a folder, you should ask the computer, "Does this exist?" This prevents your script from crashing.

### 2. Why This Matters in DevOps

**Idempotency.** If a script creates a directory, it should first check if it already exists to avoid an error. This allows you to run the same script multiple times safely.

### 3. Key Concepts

- `-f`: Check if it is a file.
- `-d`: Check if it is a directory.
- `-s`: Check if file exists and is not empty.
- `-x`: Check if file is executable.

### 4. Visual / Diagram Explanation

```
Start
   ↓
Test [ -f config.yml ]
   ├── True?  → Read File
   └── False? → Create Default File or Error
```

### 5. Code Examples

```bash
#!/bin/bash

DIR_PATH="/var/www/html"

if [[ -d "$DIR_PATH" ]]; then
    echo "Directory exists. Entering..."
    cd "$DIR_PATH"
else
    echo "Directory missing. Creating..."
    mkdir -p "$DIR_PATH"
fi
```

### 6. Real-World Example

A startup script checks if a `.lock` file exists. If it does, the script knows another instance is already running and exits to prevent conflicts.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Assuming a file exists just because you created it in a previous run.
  - ✅ **Correction:** Always verify existence before operations.

### 8. Quick Revision Summary

- `-f`: Is file?
- `-d`: Is directory?
- `-r`: Is readable?
- `! -d`: Is NOT a directory?

---

## 10. Exit Codes

### 1. Simple Explanation

Every command returns a secret number when it finishes. `0` means "I did it successfully!" Any other number (1-255) means "Something went wrong."

### 2. Why This Matters in DevOps

CI/CD Pipelines (like Jenkins or GitHub Actions) rely entirely on exit codes. If your script exits with `0`, the pipeline turns green (Pass). If it exits with `1`, the pipeline turns red (Fail).

### 3. Key Concepts

- **`$?`:** The variable holding the exit code of the *last* command.
- **`exit 0`:** Explicitly end script with success.
- **`exit 1`:** Explicitly end script with failure.

### 4. Visual / Diagram Explanation

```
Command Runs → Finishes → Sets $? to 0 or 1 → Script checks $? → Decides next step
```

### 5. Code Examples

```bash
#!/bin/bash

ls /non/existent/folder
# Capturing the result
STATUS=$?

if [[ $STATUS -ne 0 ]]; then
    echo "Command failed with code $STATUS"
    exit 1 # Tell the system this script failed
fi
```

### 6. Real-World Example

A script attempts to upload a build artifact. If the upload command fails (non-zero exit), the script stops and sends an alert to Slack instead of continuing to the "deploy" step.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Checking `$?` too late.
  - ✅ **Correction:** `$?` only holds the result of the *immediately preceding* command. Save it to a variable if you need it later.

### 8. Quick Revision Summary

- `0` = Success.
- `1-255` = Error.
- `$?` stores the last code.
- Use `exit 1` to fail a script.

---

## 11. Pipes & Redirects

### 1. Simple Explanation

- **Pipe (`|`):** Passes the output of one command to the input of another (like a bucket brigade).
- **Redirect (`>`):** Saves output to a file (overwrites).
- **Append (`>>`):** Adds output to the end of a file.

### 2. Why This Matters in DevOps

Log management and data processing. You often need to filter logs (`grep`) and save them to a file for audit trails.

### 3. Key Concepts

- **Standard Out (1):** Normal output.
- **Standard Error (2):** Error messages.
- **`2>&1`:** Redirect errors to the same place as standard output.

### 4. Visual / Diagram Explanation

```
Command A Output → | → Command B Input → > → File on Disk
```

### 5. Code Examples

```bash
#!/bin/bash

# Pipe: Find "error" in logs and count lines
cat app.log | grep "error" | wc -l

# Redirect: Save list of files to a text file (Overwrites)
ls > file_list.txt

# Append: Add a log line to a file (Keeps existing data)
echo "Backup finished" >> backup.log

# Redirect Errors: Send errors to a separate file
mkdir /root/test 2> errors.txt
```

### 6. Real-World Example

`grep "ERROR" /var/log/syslog > errors_today.txt` searches system logs for errors and saves them to a file for a developer to review.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Using `>` when you meant `>>`.
  - ✅ **Correction:** `>` deletes current file content! Use `>>` to add to it.

### 8. Quick Revision Summary

- `|`: Connects commands.
- `>`: Writes (overwrites) to file.
- `>>`: Appends to file.
- `2>`: Redirects error messages.

---

## 12. Environment Variables

### 1. Simple Explanation

Global variables set by the OS or the user that exist outside your script but affect how it runs. They configure the environment (e.g., who is the user? where are the commands installed?).

### 2. Why This Matters in DevOps

**Configuration Management.** You never hardcode passwords or API keys. You pass them as environment variables so the same script works in Dev (test key) and Prod (live key) without code changes.

### 3. Key Concepts

- **`export`:** Makes a variable available to child scripts/processes.
- **`env` / `printenv`:** Lists all current environment variables.
- **Common Vars:** `$PATH`, `$USER`, `$HOME`, `$PWD`.

### 4. Visual / Diagram Explanation

```
OS Environment (KEY=123)
   ↓
Script Starts
   ↓
Script reads $KEY
   ↓
Script finishes
```

### 5. Code Examples

```bash
#!/bin/bash

# Accessing a standard env variable
echo "Running as user: $USER"

# A script expecting an API key from the environment
if [[ -z "$API_KEY" ]]; then
    echo "Error: API_KEY is missing!"
    exit 1
fi

echo "Connecting using key: $API_KEY"
```

### 6. Real-World Example

In a Docker container, you set `DATABASE_URL` as an environment variable. The Bash entrypoint script reads `$DATABASE_URL` to configure the application before starting it.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Defining a var without `export` and expecting a sub-script to see it.
  - ✅ **Correction:** Use `export VAR=value` if child processes need it.

### 8. Quick Revision Summary

- `export VAR=value` makes it global.
- Used for Secrets/Config.
- `$PATH` tells shell where to find programs.
- Avoid hardcoding secrets; use env vars.

---

## 13. Debugging Scripts

### 1. Simple Explanation

When your script breaks (and it will), you need tools to see exactly what is happening under the hood. Bash has built-in modes to show you every command it executes.

### 2. Why This Matters in DevOps

**Root Cause Analysis.** When a deployment fails at 3 AM, you need to see exactly which command failed and why, without guessing.

### 3. Key Concepts

- **`set -x`:** Prints every command before executing it.
- **`set +x`:** Turns debugging off.
- **`shellcheck`:** An external tool that scans your code for syntax errors and bad practices.

### 4. Visual / Diagram Explanation

```
Script with set -x
   ↓
Prints "+ command"
   ↓
Executes command
   ↓
Prints "+ next command" ...
```

### 5. Code Examples

```bash
#!/bin/bash

# Turn on debugging
set -x

echo "This command is printed to console before running"
var="test"
echo "Variable is $var"

# Turn off debugging
set +x
```

### 6. Real-World Example

A build server keeps failing. You add `set -x` to the build script. The logs now show that the variable `$BUILD_DIR` was empty, causing `rm -rf $BUILD_DIR/` to try and delete the wrong files.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Debugging by adding `echo "here"` everywhere.
  - ✅ **Correction:** `set -x` is much faster and more informative.

### 8. Quick Revision Summary

- `set -x`: Print commands (trace).
- `set -e`: Stop on error.
- Use `ShellCheck` to lint code.
- Check logs for `+` signs (debug output).

---

## 14. Cron Jobs & Scheduling

### 1. Simple Explanation

Cron is a time-based job scheduler. It's an alarm clock for your servers. You tell it "Run this backup script every day at 2 AM," and it does it automatically.

### 2. Why This Matters in DevOps

**Maintenance.** Automating backups, cleaning up old logs, checking disk space, or sending status reports.

### 3. Key Concepts

- **Crontab:** The file where schedules are listed (`crontab -e`).
- **Syntax:** `Minute Hour Day Month DayOfWeek Command`
- **`*`:** Means "every".

### 4. Visual / Diagram Explanation

```
Cron Daemon checks time → Matches entry in Crontab → Executes Script → Saves output to mail/log
```

### 5. Code Examples

```bash
# Edit crontab
crontab -e

# Example Cron Entries:

# Run every minute
* * * * * /path/to/script.sh

# Run at 2:30 AM every day
30 2 * * * /path/to/backup.sh

# Run every Monday at 5 PM
0 17 * * 1 /path/to/report.sh
```

### 6. Real-World Example

A database dump script is scheduled via cron to run every night at midnight. If the server crashes the next day, the data is safe because of the automated backup.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Using relative paths in scripts run by cron.
  - ✅ **Correction:** Always use absolute paths (`/home/user/script.sh`, not `./script.sh`) because cron doesn't know your "current" folder.

### 8. Quick Revision Summary

- `crontab -e` to edit.
- Format: `Minute Hour Day Month DayOfWeek Command`.
- Use absolute paths.

---

## 15. Writing Production-Safe Scripts

### 1. Simple Explanation

Writing a script that works on your laptop is easy. Writing a script that is safe to run on a critical production server requires "defensive coding" to prevent disasters (like accidentally deleting files).

### 2. Why This Matters in DevOps

**Reliability.** A "fragile" script might delete the wrong folder if a variable is empty. Production-safe scripts fail safely and predictably.

### 3. Key Concepts

- **Bash Strict Mode:** `set -euo pipefail`
  - `-e`: Exit on error.
  - `-u`: Exit if a variable is unset (prevents `rm -rf /$EMPTY/*`).
  - `-o pipefail`: Catch errors inside pipes.
- **Quoting:** Always quote variables `"$VAR"` to handle spaces in filenames.

### 4. Visual / Diagram Explanation

```
Script Start → Enable Strict Mode → Check Pre-requisites (Vars set?) → Run Logic → Clean Exit
```

### 5. Code Examples

```bash
#!/bin/bash

# The "Safety Net" - Unofficial Bash Strict Mode
set -euo pipefail

# If $DIRECTORY is not set, the script stops here (due to -u)
# instead of deleting the root directory.
rm -rf "${DIRECTORY:?}/tmp"

echo "Script finished successfully"
```

### 6. Real-World Example

A cleanup script uses `set -u`. A developer forgot to set the `TARGET_DIR` variable. Instead of running `rm -rf /` (because the variable expanded to nothing), the script stopped with an "unbound variable" error, saving the server.

### 7. Common Beginner Mistakes

- ❌ **Mistake:** Assuming network commands (`curl`/`wget`) always work.
  - ✅ **Correction:** Strict mode (`set -e` or `pipefail`) ensures the script stops if the download fails.

### 8. Quick Revision Summary

- Use `set -euo pipefail`.
- Quote all variables `"$VAR"`.
- Check for dependencies.
- Fail fast, fail safe.

---

⭐ If these notes helped you, give the repo a star!

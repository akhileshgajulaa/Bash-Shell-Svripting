# Day 2 — Shell Scripting Notes: Variables & Command-Line Arguments

Today's focus is **variables, variable assignment, variable types, and command-line arguments**. These are the foundation for writing useful Bash scripts.

## 1. What is a Variable in Shell Scripting?

A **variable is a name used to store a value**.

For example:

```bash
name="Akhilesh"
```

Here:

- `name` → variable
- `Akhilesh` → value

We can use the variable later:

```bash
echo $name
```

Output:

```
Akhilesh
```

**Simple definition for interview**

> A variable in shell scripting is a named storage location used to hold a value that can be used and manipulated during script execution.

## 2. Syntax of a Variable

The basic syntax is:

```bash
variable_name=value
```

Example:

```bash
name="Akhilesh"
age=24
city="Hyderabad"
```

To access the value:

```bash
echo $name
echo $age
echo $city
```

Output:

```
Akhilesh
24
Hyderabad
```

**Important**

When assigning a variable, **don't put spaces around `=`**.

❌ Wrong:

```bash
name = "Akhilesh"
name= "Akhilesh"
name ="Akhilesh"
```

✅ Correct:

```bash
name="Akhilesh"
```

## 3. Rules for Declaring Variables

Bash has some important naming rules.

**Rule 1 — Variable name can contain letters**

```bash
name="Akhilesh"
```

**Rule 2 — Numbers are allowed**

```bash
name1="Akhilesh"
```

But a variable **cannot start with a number**.

❌ Wrong:

```bash
1name="Akhilesh"
```

✅ Correct:

```bash
name1="Akhilesh"
```

**Rule 3 — Underscore is allowed**

```bash
first_name="Akhilesh"
server_name="web-server"
```

**Rule 4 — No spaces in variable names**

❌ Wrong:

```bash
first name="Akhilesh"
```

✅ Correct:

```bash
first_name="Akhilesh"
```

**Rule 5 — Avoid special characters**

Variable names should generally contain:

- `A-Z`
- `a-z`
- `0-9`
- `_`

Example:

```bash
app_name="ecommerce"
server_ip="10.0.1.10"
```

## 4. Variable Assignment

There are different ways to assign values.

**String**

```bash
name="Akhilesh"
```

**Number**

```bash
age=24
```

**Path**

```bash
app_path="/opt/myapp"
```

**Command output**

We can store the output of a command in a variable.

```bash
current_date=$(date)
```

Then:

```bash
echo "$current_date"
```

Example output:

```
Tue Sep 8 10:30:00 IST 2026
```

This is called **command substitution**.

Another example:

```bash
files=$(ls)
echo "$files"
```

## 5. How to Access a Variable?

Use `$` before the variable name.

```bash
name="Akhilesh"
echo $name
```

Output:

```
Akhilesh
```

You can also use:

```bash
echo "$name"
```

**Recommended practice**

Prefer:

```bash
echo "$name"
```

because quoting variables helps prevent unexpected word splitting and glob expansion.

## 6. Curly Braces `{}` with Variables

You can use:

```bash
${variable}
```

This is especially useful when adding text immediately after a variable.

Example:

```bash
name="Akhilesh"
echo "${name}DevOps"
```

Output:

```
AkhileshDevOps
```

Without braces:

```bash
echo "$nameDevOps"
```

Bash may interpret `nameDevOps` as the variable name.

So use:

```bash
"${name}DevOps"
```

## 7. Types of Variables in Shell

This is an **important interview point**.

Unlike languages such as Java, Bash does **not normally have strongly typed variables**.

For example:

```bash
name="Akhilesh"
age=24
```

Bash variables are generally treated as strings, although Bash supports arithmetic operations when used in an arithmetic context.

**Common practical categories**

**1. String**

```bash
name="Akhilesh"
```

**2. Integer / number**

```bash
age=24
```

Arithmetic:

```bash
a=10
b=20
sum=$((a+b))
echo "$sum"
```

Output:

```
30
```

**3. Array**

Bash supports arrays:

```bash
servers=("web1" "web2" "web3")
```

Access:

```bash
echo "${servers[0]}"
```

Output:

```
web1
```

**4. Environment variables**

Examples:

- `PATH`
- `HOME`
- `USER`
- `SHELL`
- `PWD`

Check:

```bash
echo "$HOME"
echo "$USER"
echo "$PATH"
```

## 8. Local Variables vs Environment Variables

This is useful for DevOps.

**Shell variable**

```bash
app="ecommerce"
```

This variable belongs to the current shell environment.

**Environment variable**

Use `export`:

```bash
export app="ecommerce"
```

Now child processes can access it.

Example:

```bash
export APP_ENV="production"
echo "$APP_ENV"
```

Output:

```
production
```

You can see environment variables with:

```bash
env
```

or:

```bash
printenv
```

**Simple difference**

```
variable
  ↓
available in current shell

export variable
  ↓
available to current shell + child processes
```

## 9. Read-Only Variables

Bash also allows variables that cannot be changed after being declared.

```bash
readonly APP_NAME="ecommerce"
```

Trying to change it:

```bash
APP_NAME="test"
```

will produce an error.

You can check:

```bash
readonly
```

## 10. Command-Line Arguments

This is **very important for DevOps scripts**.

Command-line arguments allow us to pass values to a script when executing it.

For example:

```bash
./deploy.sh production
```

Here:

- `deploy.sh` → script
- `production` → argument

Inside the script, we can access `production` using:

```bash
$1
```

## 11. Positional Parameters

Bash provides special variables for command-line arguments.

| Variable | Meaning |
|---|---|
| `$0` | Script name |
| `$1` | First argument |
| `$2` | Second argument |
| `$3` | Third argument |
| `$#` | Number of arguments |
| `$@` | All arguments |
| `$*` | All arguments |
| `$?` | Exit status of previous command |

## 12. Example of Command-Line Arguments

Create:

```bash
vim deploy.sh
```

Script:

```bash
#!/bin/bash
echo "Script name: $0"
echo "Environment: $1"
echo "Application: $2"
echo "Number of arguments: $#"
```

Make executable:

```bash
chmod +x deploy.sh
```

Run:

```bash
./deploy.sh production ecommerce
```

Output:

```
Script name: ./deploy.sh
Environment: production
Application: ecommerce
Number of arguments: 2
```

## 13. Understanding `$0`

Suppose you run:

```bash
./deploy.sh production
```

Then:

```bash
echo "$0"
```

returns something like:

```
./deploy.sh
```

So: `$0` → script name.

## 14. Understanding `$1`, `$2`, `$3`

If we execute:

```bash
./deploy.sh production ecommerce ap-south-1
```

Then:

- `$1` → `production`
- `$2` → `ecommerce`
- `$3` → `ap-south-1`

Example:

```bash
echo "Environment: $1"
echo "Application: $2"
echo "Region: $3"
```

Output:

```
Environment: production
Application: ecommerce
Region: ap-south-1
```

## 15. Understanding `$#`

`$#` tells us **how many arguments were passed**.

Example:

```bash
./deploy.sh production ecommerce ap-south-1
```

Inside the script:

```bash
echo "$#"
```

Output:

```
3
```

## 16. Understanding `$@`

`$@` represents **all command-line arguments**.

Example:

```bash
#!/bin/bash
echo "Arguments: $@"
```

Run:

```bash
./script.sh one two three
```

Output:

```
Arguments: one two three
```

A particularly useful pattern is:

```bash
for arg in "$@"
do
    echo "$arg"
done
```

This processes each argument individually.

## 17. `$@` vs `$*`

This is a common interview question.

Both represent all positional arguments, but when quoted they behave differently.

**Prefer:**

```bash
"$@"
```

because it preserves each argument as a separate word.

For example, if you run:

```bash
./script.sh "hello world" test
```

With `"$@"`, the arguments remain:

```
hello world
test
```

as two separate arguments.

**For most scripts, use `"$@"` when you want to iterate over or forward all arguments.**

## 18. Real DevOps Example

Imagine you create a deployment script: `deploy.sh`.

Instead of hardcoding:

```bash
environment="production"
```

you can pass the environment from the command line:

```bash
./deploy.sh production
```

Script:

```bash
#!/bin/bash
environment="$1"
echo "Deploying application to $environment environment"
```

Run:

```bash
./deploy.sh dev
```

Output:

```
Deploying application to dev environment
```

Run:

```bash
./deploy.sh staging
```

Output:

```
Deploying application to staging environment
```

Run:

```bash
./deploy.sh production
```

Output:

```
Deploying application to production environment
```

This makes the script **reusable**.

## 19. Command-Line Arguments in CI/CD

This becomes very useful in DevOps.

For example:

```bash
./deploy.sh production v1.5.0
```

Here:

- `$1` → `production`
- `$2` → `v1.5.0`

Script:

```bash
#!/bin/bash
ENVIRONMENT="$1"
VERSION="$2"

echo "Environment: $ENVIRONMENT"
echo "Version: $VERSION"

# deployment commands...
```

A CI/CD pipeline can call the same script with different values:

```bash
./deploy.sh dev v1.5.0
```

or:

```bash
./deploy.sh production v2.0.0
```

**One script → multiple environments.**

That's a very important DevOps use case.

## 20. Important Example — Variable + Argument

```bash
#!/bin/bash
ENVIRONMENT="$1"
APP_NAME="$2"

echo "Starting deployment..."
echo "Application: $APP_NAME"
echo "Environment: $ENVIRONMENT"
echo "Deployment completed."
```

Run:

```bash
./deploy.sh production ecommerce
```

Output:

```
Starting deployment...
Application: ecommerce
Environment: production
Deployment completed.
```

## 21. Day-2 Quick Revision

```
VARIABLE
  ↓
name="Akhilesh"

ACCESS
  ↓
echo "$name"

COMMAND OUTPUT
  ↓
date=$(date)

ENVIRONMENT VARIABLE
  ↓
export APP_ENV="production"

COMMAND-LINE ARGUMENTS
  ↓
./deploy.sh production ecommerce

$0 → Script name
$1 → First argument
$2 → Second argument
$3 → Third argument
$# → Number of arguments
$@ → All arguments
$* → All arguments
$? → Previous command exit status
```

**Most Important Rules to Remember**

```bash
# Correct
name="Akhilesh"

# Wrong
name = "Akhilesh"

# Access variable
echo "$name"

# Command substitution
today=$(date)

# Environment variable
export APP_ENV="production"

# Command-line arguments
./deploy.sh production ecommerce
# $1 → production
# $2 → ecommerce
```

## 🎯 Day-2 Interview Answer

> In Bash, variables are used to store and reuse values. Bash variables are generally untyped, although arithmetic operations can be performed on numeric values. Variables are assigned using `variable=value` without spaces around `=`. Shell scripts can also accept command-line arguments using positional parameters such as `$1`, `$2`, `$#`, and `$@`. This makes scripts reusable, especially in DevOps and CI/CD automation.

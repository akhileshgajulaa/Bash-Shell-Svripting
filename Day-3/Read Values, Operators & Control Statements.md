**Day 3 — Shell Scripting Notes**

**Read Values, Operators & Control Statements**

Today we move from **variables** to making scripts **interactive and intelligent**.

The main idea is:

Read input

↓

Store in variable

↓

Check condition using operators

↓

Take decision

↓

Execute required command

**1\. Reading Values in Shell Scripting**

We can take input from the user using the read command.

**Basic syntax**

read variable_name

Example:

# !/bin/bash

echo "Enter your name:"

read name

echo "Hello \$name"

Run:

./script.sh

Output:

Enter your name:

Akhilesh

Hello Akhilesh

**read -p**

Instead of using a separate echo, we can directly display the prompt:

# !/bin/bash

read -p "Enter your name: " name

echo "Hello \$name"

**Reading multiple values**

# !/bin/bash

read -p "Enter your first name and age: " name age

echo "Name: \$name"

echo "Age: \$age"

Input:

Akhilesh 24

Output:

Name: Akhilesh

Age: 24

**2\. Reading Passwords**

For sensitive input, use -s.

read -s -p "Enter password: " password

echo

echo "Password received"

\-s means the input is **not displayed on the terminal**.

Note: This only hides the input while typing; it does not encrypt the value.

**3\. Operators in Shell Scripting**

Operators are used to perform operations or compare values.

Important categories:

Arithmetic operators

Comparison operators

Logical operators

String operators

**4\. Arithmetic Operators**

Arithmetic operators are used with numbers.

| **Operator** | **Meaning**       |
| ------------ | ----------------- |
| +            | Addition          |
| \-           | Subtraction       |
| \*           | Multiplication    |
| /            | Division          |
| %            | Modulus/remainder |
| \*\*         | Power             |

**Example**

a=10

b=5

echo \$((a + b))

echo \$((a - b))

echo \$((a \* b))

echo \$((a / b))

echo \$((a % b))

Output:

15

5

50

2

0

The usual Bash arithmetic syntax is:

\$((expression))

**5\. Comparison Operators**

Comparison operators are mainly used to compare numbers.

| **Operator** | **Meaning**           |
| ------------ | --------------------- |
| \-eq         | Equal                 |
| \-ne         | Not equal             |
| \-gt         | Greater than          |
| \-lt         | Less than             |
| \-ge         | Greater than or equal |
| \-le         | Less than or equal    |

Example:

age=24

if \[ "\$age" -ge 18 \]; then

echo "You are eligible"

fi

Output:

You are eligible

**Easy way to remember**

\-eq → equal

\-ne → not equal

\-gt → greater than

\-lt → less than

\-ge → greater/equal

\-le → less/equal

**6\. Important: \[ \] in Conditions**

You will frequently see:

if \[ "\$age" -ge 18 \]; then

The spaces are important.

✅ Correct:

\[ "\$age" -ge 18 \]

❌ Wrong:

\["\$age" -ge 18\]

Think of \[ ... \] as Bash's test syntax.

**7\. String Operators**

String operators are used to compare text.

| **Operator** | **Meaning**           |
| ------------ | --------------------- |
| \=           | Strings are equal     |
| !=           | Strings are not equal |
| \-z          | String is empty       |
| \-n          | String is not empty   |

**Example — Equal**

name="Akhilesh"

if \[ "\$name" = "Akhilesh" \]; then

echo "Name matched"

fi

**Not equal**

environment="dev"

if \[ "\$environment" != "production" \]; then

echo "This is not production"

fi

**Check empty string**

name=""

if \[ -z "\$name" \]; then

echo "Name is empty"

fi

**Check non-empty string**

name="Akhilesh"

if \[ -n "\$name" \]; then

echo "Name is provided"

fi

**8\. Logical Operators**

Logical operators allow us to combine multiple conditions.

| **Operator** | **Meaning** |
| ------------ | ----------- |
| &&           | AND         |
| \`           |             |
| !            | NOT         |

**AND — &&**

Both conditions must be true.

Example:

age=25

has_id="yes"

if \[ "\$age" -ge 18 \] && \[ "\$has_id" = "yes" \]; then

echo "Allowed"

else

echo "Not allowed"

fi

Think:

Age >= 18

AND

ID = yes

↓

Allowed

**OR — ||**

At least one condition must be true.

day="Saturday"

if \[ "\$day" = "Saturday" \] || \[ "\$day" = "Sunday" \]; then

echo "Weekend"

else

echo "Weekday"

fi

**NOT — !**

Used to reverse a condition.

status="stopped"

if \[ ! "\$status" = "running" \]; then

echo "Application is not running"

fi

**9\. Control Statements**

Control statements allow a script to **make decisions**.

The important ones are:

if

if-else

if-elif-else

case

**10\. if Statement**

Syntax:

if \[ condition \]; then

commands

fi

Example:

age=25

if \[ "\$age" -ge 18 \]; then

echo "You are an adult"

fi

If the condition is true, the command executes.

**11\. if-else**

Use else when you want to execute something when the condition is false.

age=16

if \[ "\$age" -ge 18 \]; then

echo "Eligible"

else

echo "Not eligible"

fi

Output:

Not eligible

**12\. if-elif-else**

When you have multiple conditions:

marks=75

if \[ "\$marks" -ge 90 \]; then

echo "Grade A+"

elif \[ "\$marks" -ge 75 \]; then

echo "Grade A"

elif \[ "\$marks" -ge 60 \]; then

echo "Grade B"

else

echo "Need improvement"

fi

Output:

Grade A

**13\. Daily-Life Example — ATM**

Let's create a simple ATM-like example.

# !/bin/bash

read -p "Enter your PIN: " pin

if \[ "\$pin" = "1234" \]; then

echo "PIN is correct"

echo "Welcome to ATM"

else

echo "Incorrect PIN"

fi

**Flow**

User enters PIN

↓

Is PIN correct?

↙ ↘

YES NO

↓ ↓

Welcome Denied

This is a simple example of using:

- read
- variable
- string comparison
- if-else

**14\. Daily-Life Example — Shopping Discount**

# !/bin/bash

read -p "Enter shopping amount: " amount

if \[ "\$amount" -ge 5000 \]; then

echo "You get 20% discount"

elif \[ "\$amount" -ge 2000 \]; then

echo "You get 10% discount"

else

echo "No discount"

fi

Example:

Enter shopping amount: 3500

You get 10% discount

**15\. Daily-Life Example — Login**

# !/bin/bash

read -p "Enter username: " username

read -s -p "Enter password: " password

echo

if \[ "\$username" = "admin" \] && \[ "\$password" = "admin123" \]; then

echo "Login successful"

else

echo "Invalid username or password"

fi

This demonstrates:

read

-

string comparison

-

AND operator

-

if-else

**For real applications, don't hard-code passwords like this.** This is only a learning example.

**16\. case Statement**

case is useful when we have **multiple possible values**.

It is similar to switch statements in some programming languages.

**Syntax**

case "\$variable" in

value1)

commands

;;

value2)

commands

;;

\*)

default commands

;;

esac

Important:

case → starts

esac → ends

esac is simply case spelled backward.

**17\. Daily-Life Example — Menu**

# !/bin/bash

echo "1. Tea"

echo "2. Coffee"

echo "3. Juice"

echo "4. Water"

read -p "Choose an option: " choice

case "\$choice" in

1.

echo "You selected Tea"

;;

1.

echo "You selected Coffee"

;;

1.

echo "You selected Juice"

;;

1.

echo "You selected Water"

;;

\*)

echo "Invalid option"

;;

esac

If the user enters:

2

Output:

You selected Coffee

**18\. Real-Time DevOps Use Case #1 — Check Service**

This is a very useful beginner DevOps script.

Suppose we want to check whether an application service is running.

# !/bin/bash

service_name="nginx"

if systemctl is-active --quiet "\$service_name"; then

echo "\$service_name is running"

else

echo "\$service_name is not running"

fi

**What happens?**

Check nginx

↓

Is it running?

↙ ↘

YES NO

↓ ↓

Running Not running

**19\. Real-Time DevOps Use Case #2 — Restart Service Automatically**

We can make the previous example more useful.

# !/bin/bash

service_name="nginx"

if systemctl is-active --quiet "\$service_name"; then

echo "\$service_name is running"

else

echo "\$service_name is down"

echo "Starting \$service_name..."

sudo systemctl start "\$service_name"

if systemctl is-active --quiet "\$service_name"; then

echo "\$service_name started successfully"

else

echo "Failed to start \$service_name"

fi

fi

This is a simple example of **automated monitoring and recovery**.

**20\. Real-Time DevOps Use Case #3 — Environment-Based Deployment**

This is closer to CI/CD.

# !/bin/bash

environment="\$1"

if \[ -z "\$environment" \]; then

echo "Usage: \$0 &lt;dev|staging|production&gt;"

exit 1

fi

if \[ "\$environment" = "dev" \]; then

echo "Deploying to DEV environment"

elif \[ "\$environment" = "staging" \]; then

echo "Deploying to STAGING environment"

elif \[ "\$environment" = "production" \]; then

echo "Deploying to PRODUCTION environment"

else

echo "Invalid environment"

exit 1

fi

Run:

./deploy.sh dev

Output:

Deploying to DEV environment

Run:

./deploy.sh production

Output:

Deploying to PRODUCTION environment

**21\. Real-Time DevOps Use Case #4 — Better with case**

The same deployment selection can be written using case.

# !/bin/bash

environment="\$1"

case "\$environment" in

dev)

echo "Deploying to DEV"

;;

staging)

echo "Deploying to STAGING"

;;

production)

echo "Deploying to PRODUCTION"

;;

\*)

echo "Invalid environment"

echo "Usage: \$0 &lt;dev|staging|production&gt;"

exit 1

;;

esac

This is cleaner when there are many possible values.

**22\. Real-Time DevOps Use Case #5 — Check Disk Usage**

This is a very practical Linux/DevOps example.

# !/bin/bash

usage=\$(df / | awk 'NR==2 {print \$5}' | tr -d '%')

echo "Disk usage: \$usage%"

if \[ "\$usage" -ge 80 \]; then

echo "WARNING: Disk usage is high"

elif \[ "\$usage" -ge 90 \]; then

echo "CRITICAL: Disk usage is very high"

else

echo "Disk usage is normal"

fi

**Important correction**

When checking thresholds, you normally want the **higher threshold first**:

if \[ "\$usage" -ge 90 \]; then

echo "CRITICAL"

elif \[ "\$usage" -ge 80 \]; then

echo "WARNING"

else

echo "NORMAL"

fi

So the better version is:

# !/bin/bash

usage=\$(df / | awk 'NR==2 {print \$5}' | tr -d '%')

echo "Disk usage: \$usage%"

if \[ "\$usage" -ge 90 \]; then

echo "CRITICAL: Disk usage is very high"

elif \[ "\$usage" -ge 80 \]; then

echo "WARNING: Disk usage is high"

else

echo "Disk usage is normal"

fi

**23\. Real-Time DevOps Use Case #6 — Check Application URL**

You can use curl to check whether an application is responding.

# !/bin/bash

url="<http://localhost:8080>"

if curl -s --fail "\$url" > /dev/null; then

echo "Application is UP"

else

echo "Application is DOWN"

fi

**Flow**

curl application

↓

HTTP request successful?

↙ ↘

YES NO

↓ ↓

UP DOWN

This type of check can be used as part of monitoring or deployment validation.

**24\. Real-Time DevOps Use Case #7 — Docker Container Check**

# !/bin/bash

container="myapp"

if docker ps --format '{{.Names}}' | grep -q "^\${container}\$"; then

echo "\$container is running"

else

echo "\$container is not running"

fi

This demonstrates how shell scripting can automate a Docker health check.

**25\. Combining read + Operators + if**

Let's create one complete beginner example.

# !/bin/bash

read -p "Enter CPU usage percentage: " cpu

if \[ "\$cpu" -ge 90 \]; then

echo "CRITICAL: CPU usage is very high"

elif \[ "\$cpu" -ge 80 \]; then

echo "WARNING: CPU usage is high"

else

echo "CPU usage is normal"

fi

Example:

Enter CPU usage percentage: 95

CRITICAL: CPU usage is very high

This is a good example to understand how DevOps monitoring scripts work.

**26\. if vs case**

**Use if**

When you're checking:

Greater than

Less than

Equal to

Multiple conditions

Ranges

Example:

if \[ "\$cpu" -ge 80 \]; then

**Use case**

When you're matching one variable against several **specific values/patterns**.

Example:

case "\$environment" in

dev)

...

;;

staging)

...

;;

production)

...

;;

esac

**Easy way to remember**

if

↓

Condition-based decision

case

↓

Value-based selection

**27\. Day-3 Complete Revision**

read

↓

Take input from user

Operators

↓

Perform calculations / comparisons

Comparison

↓

\-eq -ne -gt -lt -ge -le

String

↓

\= != -z -n

Logical

↓

&& || !

Control statements

↓

if

if-else

if-elif-else

case

DevOps usage

↓

Service checks

Disk monitoring

Application health checks

Deployment automation

Docker checks

CI/CD automation

**Commands/Syntax to Practice Today**

\# Read

read -p "Enter name: " name

\# Arithmetic

sum=\$((10 + 20))

\# Number comparison

if \[ "\$age" -ge 18 \]; then

\# String comparison

if \[ "\$env" = "production" \]; then

\# AND

if \[ "\$cpu" -ge 80 \] && \[ "\$memory" -ge 80 \]; then

\# OR

if \[ "\$env" = "dev" \] || \[ "\$env" = "staging" \]; then

\# Empty string

if \[ -z "\$name" \]; then

\# Case

case "\$env" in

dev)

echo "Development"

;;

production)

echo "Production"

;;

\*)

echo "Invalid"

;;

esac

**🎯 Interview line for Day 3**

**In shell scripting, I can use read to accept user input, variables to store values, operators to perform calculations and comparisons, and control statements such as if-else and case to make decisions. In DevOps, these concepts are useful for automation tasks such as service health checks, deployment scripts, disk monitoring, Docker checks, and CI/CD automation.**

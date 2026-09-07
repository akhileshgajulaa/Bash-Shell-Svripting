# Day-1: Shell Scripting for DevOps Engineers

## 1. What is Shell?

A **shell is a command-line interpreter** that allows us to interact with the Linux operating system.

For example, when we run:

```bash
ls
cd /var/log
pwd
mkdir test
```

the shell takes these commands and asks the Linux OS to execute them.

**Simple flow**

```
User
  ↓
Shell
  ↓
Linux Kernel
  ↓
Hardware / Resources
```

Example:

```bash
ls -l
```

The shell receives `ls -l`, executes the command, and displays the result.

## 2. What is Shell Scripting?

**Shell scripting means writing multiple Linux commands in a file and executing them together as a program.**

Instead of manually running:

```bash
mkdir backup
cp app.log backup/
tar -czf backup.tar.gz backup/
```

we can put everything into a script:

```bash
#!/bin/bash
mkdir backup
cp app.log backup/
tar -czf backup.tar.gz backup/
```

Then execute the script.

**Simple definition for interview**

> Shell scripting is the process of writing a sequence of Linux commands in a script file to automate repetitive tasks.

## 3. Why do DevOps Engineers Need Shell Scripting?

Shell scripting is very important in DevOps because DevOps involves **automation**.

You will frequently work with:

- Linux servers
- AWS EC2
- Docker
- Kubernetes
- CI/CD pipelines
- GitHub Actions
- Jenkins
- Application deployments
- Log management
- Monitoring
- Backup
- Server administration

Many of these tasks can be automated using shell scripts.

**Example**

Suppose you need to:

1. Pull latest code
2. Build application
3. Create Docker image
4. Push image to ECR
5. Deploy to Kubernetes

Instead of manually executing commands every time, a script can automate them.

```bash
#!/bin/bash
git pull
mvn clean package
docker build -t myapp .
docker push myapp:latest
kubectl apply -f deployment.yaml
```

**Interview answer**

> As a DevOps engineer, I learn shell scripting because Linux is widely used for servers and DevOps tools. Shell scripting helps me automate deployments, backups, log management, server administration, monitoring tasks, and CI/CD activities.

## 4. Default Shells in Linux

Linux supports multiple shells.

Common shells are:

| Shell | Command       | Description                                          |
|-------|---------------|-------------------------------------------------------|
| Bash  | `/bin/bash`   | Most commonly used                                     |
| sh    | `/bin/sh`     | Bourne shell / shell-compatible interface               |
| Dash  | `/bin/dash`   | Lightweight shell, commonly `/bin/sh` on Debian/Ubuntu   |
| Zsh   | `/bin/zsh`    | Powerful interactive shell                              |
| Ksh   | `/bin/ksh`    | Korn shell                                              |
| Fish  | `/usr/bin/fish` | User-friendly shell                                    |
| Csh   | `/bin/csh`    | C-like syntax                                           |

**Most important for DevOps: Bash**

You should learn Bash first.

## 5. How to Check Available Shells?

Linux maintains a list of supported login shells in `/etc/shells`. Run:

```bash
cat /etc/shells
```

Example output:

```
/bin/sh
/bin/bash
/usr/bin/bash
/bin/dash
/usr/bin/dash
/bin/zsh
```

## 6. How to Check Which Shell We Are Currently Using?

There are several ways.

**Method 1 — `$SHELL`**

```bash
echo $SHELL
```

Example output:

```
/bin/bash
```

This normally shows your **default login shell**.

**Method 2 — `ps`**

```bash
ps -p $$ -o comm=
```

Example output:

```
bash
```

This is useful for identifying the **currently running shell**.

**Method 3**

```bash
echo $0
```

Example output:

```
bash
```

**Important interview point**

`echo $SHELL` and `ps -p $$ -o comm=` are not exactly the same thing.

`$SHELL` generally tells you the user's configured login shell, while `ps` tells you the shell process currently running.

## 7. How to Check User's Default Shell?

You can use:

```bash
grep "^$USER:" /etc/passwd
```

Example output:

```
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
```

The last field, `/bin/bash`, is the user's default shell.

Another command:

```bash
getent passwd $USER
```

## 8. How to Install Extra Shells?

**For Ubuntu/Debian**

Install Zsh:

```bash
sudo apt update
sudo apt install zsh
```

Check:

```bash
zsh --version
```

Install Fish:

```bash
sudo apt install fish
```

Check:

```bash
fish --version
```

Install Ksh:

```bash
sudo apt install ksh
```

**For RHEL/CentOS/Amazon Linux**

Package managers can differ by distribution/version, but commonly:

```bash
sudo dnf install zsh
```

or:

```bash
sudo yum install zsh
```

Check:

```bash
zsh --version
```

## 9. How to Switch Shell?

There are two meanings of "switch shell."

**Method 1 — Temporarily switch**

If Bash is running:

```bash
zsh
```

Now you are inside Zsh. Check:

```bash
echo $0
```

To return:

```bash
exit
```

You return to Bash.

**Example flow**

```
bash
  ↓
zsh
  ↓
exit
  ↓
bash
```

## 10. How to Change Default Shell Permanently?

Use:

```bash
chsh -s /bin/zsh
```

Then log out and log in again. Check:

```bash
echo $SHELL
```

You may see:

```
/bin/zsh
```

For Bash:

```bash
chsh -s /bin/bash
```

**Important:** `chsh` changes your **default login shell**, not just the shell for the current terminal.

## 11. What Are the Prerequisites for Learning Shell Scripting?

You don't need programming experience to start. But you should know basic Linux commands.

**Level 1 — Linux basics**

```bash
pwd
ls
cd
mkdir
touch
cp
mv
rm
cat
less
head
tail
```

**Level 2 — File permissions**

Understand `chmod`, `chown`.

Example:

```bash
chmod +x script.sh
```

**Level 3 — Text processing**

```bash
grep
sed
awk
cut
sort
uniq
wc
```

**Level 4 — Linux concepts**

Understand:

- Files/directories
- Processes
- Environment variables
- PATH
- Permissions
- Users/groups
- Pipes
- Redirection

For example:

```bash
cat app.log | grep ERROR
```

**Level 5 — Basic programming concepts**

Understand:

- Variables
- Conditions
- Loops
- Functions
- Exit status
- Input/output

## 12. Basic Shell Script Structure

A basic Bash script looks like this:

```bash
#!/bin/bash
# This is a comment
echo "Hello World"
```

Let's understand each part.

**`#!/bin/bash`**

This is called a **shebang** or **hashbang**.

```bash
#!/bin/bash
```

It tells Linux: execute this script using `/bin/bash`.

Another example:

```bash
#!/bin/sh
```

means use `/bin/sh`.

For Bash scripting, normally use:

```bash
#!/bin/bash
```

## 13. First Shell Script

Create a file:

```bash
vim hello.sh
```

Add:

```bash
#!/bin/bash
echo "Hello World"
```

Save it.

## 14. How to Run Shell Script?

There are multiple ways.

**Method 1 — Using Bash**

```bash
bash hello.sh
```

This doesn't require execute permission on the script.

**Method 2 — Using `./`**

First give execute permission:

```bash
chmod +x hello.sh
```

Then:

```bash
./hello.sh
```

This is very commonly used.

**Method 3 — Absolute path**

```bash
/bin/bash hello.sh
```

## 15. Why Do We Need `chmod +x`?

When you execute:

```bash
./hello.sh
```

Linux needs execute permission. Check permissions:

```bash
ls -l hello.sh
```

Before:

```
-rw-r--r-- hello.sh
```

After:

```bash
chmod +x hello.sh
```

you may see:

```
-rwxr-xr-x hello.sh
```

The `x` means **execute permission**.

## 16. Running Shell Script in Debug Mode

This is very important when troubleshooting scripts.

Use:

```bash
bash -x hello.sh
```

Example script:

```bash
#!/bin/bash
name="Akhilesh"
echo "Hello $name"
```

Run:

```bash
bash -x hello.sh
```

Output will look approximately like:

```
+ name=Akhilesh
+ echo 'Hello Akhilesh'
Hello Akhilesh
```

The `+` lines show the commands being executed.

## 17. Debug Mode Inside the Script

You can also use:

```bash
set -x
```

Example:

```bash
#!/bin/bash
set -x
name="Akhilesh"
echo "Hello $name"
```

Turn debugging off:

```bash
set +x
```

Example:

```bash
#!/bin/bash
set -x
echo "Starting application"
set +x
echo "Application started"
```

## 18. Debugging Options You Should Know

**Execute entire script in debug mode**

```bash
bash -x script.sh
```

**Syntax check without executing**

```bash
bash -n script.sh
```

This checks syntax. If there is no output, syntax is generally valid.

**Very useful combination**

```bash
bash -n script.sh
bash -x script.sh
```

Think:

- `-n` → Check syntax
- `-x` → Show commands while executing

## 19. Types of Comments in Shell Script

Shell scripting mainly uses comments beginning with `#`.

**Single-line comment**

```bash
# This is a comment
echo "Hello"
```

Everything after `#` on that line is ignored.

**Inline comment**

```bash
echo "Hello" # Print greeting
```

**Multiple-line comment**

Shell doesn't have a dedicated multiline-comment syntax like some programming languages.

A common technique is:

```bash
: <<'COMMENT'
This is a
multi-line comment.
COMMENT
```

But for normal scripts, it's often better to simply use `#` on each line:

```bash
# This script performs
# application deployment
# and restarts the service.
```

## 20. Important Shell Concepts for Day 1

You should remember these commands:

| Requirement | Command |
|---|---|
| Check current shell | `echo $SHELL` |
| Check running shell | `ps -p $$ -o comm=` |
| List shells | `cat /etc/shells` |
| Install Zsh | `sudo apt install zsh` |
| Temporarily switch | `zsh` |
| Return to previous shell | `exit` |
| Change default shell | `chsh -s /bin/zsh` |
| Create script | `vim script.sh` |
| Execute with Bash | `bash script.sh` |
| Make executable | `chmod +x script.sh` |
| Execute directly | `./script.sh` |
| Debug | `bash -x script.sh` |
| Syntax check | `bash -n script.sh` |

## 21. Simple DevOps Example

Suppose your application is running on an EC2 server.

You manually execute:

```bash
cd /opt/myapp
git pull
mvn clean package -DskipTests
sudo systemctl restart myapp
sudo systemctl status myapp
```

Instead, create `deploy.sh`:

```bash
#!/bin/bash
cd /opt/myapp
git pull
mvn clean package -DskipTests
sudo systemctl restart myapp
sudo systemctl status myapp
```

Then:

```bash
chmod +x deploy.sh
```

Run:

```bash
./deploy.sh
```

Now one command performs the deployment.

**This is the main reason DevOps engineers use shell scripting: automation.**

## 22. Interview Questions From Day 1

**Q1. What is Shell?**

Shell is a command-line interpreter that provides an interface between the user and the Linux operating system.

**Q2. What is Shell scripting?**

Shell scripting is writing a sequence of shell/Linux commands into a file so that tasks can be executed automatically.

**Q3. Which shell is commonly used?**

Bash is one of the most commonly used shells in Linux environments and is widely used for scripting and DevOps automation.

**Q4. How do you check the current shell?**

```bash
echo $SHELL
```

For the currently running shell:

```bash
ps -p $$ -o comm=
```

**Q5. How do you execute a shell script?**

```bash
bash script.sh
```

or:

```bash
chmod +x script.sh
./script.sh
```

**Q6. How do you debug a shell script?**

```bash
bash -x script.sh
```

**Q7. How do you check shell-script syntax?**

```bash
bash -n script.sh
```

**Q8. What is shebang?**

```bash
#!/bin/bash
```

The shebang specifies which interpreter should be used to execute the script.

**Q9. Why is shell scripting important for DevOps?**

It helps automate repetitive tasks such as deployments, backups, log processing, server configuration, monitoring, and CI/CD operations.

## Day-1 Quick Revision

```
Shell
  ↓
Command-line interpreter

Shell scripting
  ↓
Multiple commands written in a script
  ↓
Automation

Most important shell
  ↓
Bash

Check default shell
  ↓
echo $SHELL

Check running shell
  ↓
ps -p $$ -o comm=

Available shells
  ↓
cat /etc/shells

Install Zsh
  ↓
sudo apt install zsh

Switch temporarily
  ↓
zsh

Change default shell
  ↓
chsh -s /bin/zsh

Script
  ↓
#!/bin/bash
echo "Hello"

Run
  ↓
bash script.sh

Executable
  ↓
chmod +x script.sh
./script.sh

Debug
  ↓
bash -x script.sh

Syntax check
  ↓
bash -n script.sh
```

## Your Day-1 Learning Target

Don't try to learn advanced scripting today. Make sure you can comfortably do this:

```bash
#!/bin/bash
echo "Starting deployment"
name="Akhilesh"
echo "Hello $name"
echo "Deployment completed"
```

Then practice:

```bash
bash script.sh
bash -x script.sh
chmod +x script.sh
./script.sh
bash -n script.sh
```

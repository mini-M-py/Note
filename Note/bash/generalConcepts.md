# Programming concepts for bash scripts

Now that you know the basics of Bash commands, variables, and file handling, you’re ready to **write simple scripts** and learn programming constructs like loops and conditionals.

## Bash Programming Basics: Loops, Conditionals, and More

This article teaches you how to write Bash scripts using conditionals, loops, and functions to automate tasks and create simple programs.

## 1. Writing Your First Script

### Shebang

- **Shebang**: This tells the system what to run the commands with.

```bash
#!/bin/bash
```

you could use `#!/usr/bin/bash` or `#!/usr/bin/env bash` as well.

### Create and Run Script

I am showing nano to create and open file. Add shebang and then add chain of commands that you want to run.

```bash
$ nano script.sh
$ chmod +x script.sh
$ ./script.sh
```

## 2. Variables & Input

As we already discussed in intro, we can dynamically define variables and use as per our needs.

```bash
name="Alice"
echo "Hello, $name!"

read -p "Enter your age: " age
echo "You are $age years old."
```

## 3. Conditional Statements

### If / Else Statements

If / Else can be defined in the following way and used as per our usage.

```bash
if [ "$age" -ge 60 ]; then
    echo "You are a elder citizen."
elif [ "$age" -ge 18 ]; then
    echo "You are an adult."
else
    echo "You are a minor."
fi
```

### Case Statements

Case Statement let us run different commands for each given case of a variable.

```bash
read -p "Enter a number (1-3): " num
case $num in
  1) echo "One";;
  2) echo "Two";;
  3) echo "Three";;
  *) echo "Invalid number";;
esac
```

## 4. Loops

### For Loop

```bash
for i in {1..5}; do
  echo "Number $i"
done
```

### While Loop

```bash
count=1
while [ $count -le 5 ]; do
  echo "Count $count"
  ((count++))
done
```

### Until Loop

```bash
count=1
until [ $count -gt 5 ]; do
  echo "Count $count"
  ((count++))
done
```

## 5. Functions

```bash
greet() {
  echo "Hello, $1!"
}

greet "Alice"
```

## 6. Practical Example

```bash
#!/bin/bash
for file in *.txt; do
  echo "Processing $file"
  wc -l $file
done
```

## 7. Tips for Better Scripts

- Use comments: `# This is a comment`
- Quote strings to avoid errors: `"Hello $name"`
- Debug with: `set -x` (shows command execution)

## 8. Next Steps

You now have the basics of Bash scripting. You can explore:

- Arrays
- String manipulation
- Scheduling tasks with `cron`
- Writing more complex automation scripts

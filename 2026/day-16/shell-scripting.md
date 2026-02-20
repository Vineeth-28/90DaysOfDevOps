
# Day 16 – Shell Scripting Basics

## 📌 Objective

Today I started learning shell scripting fundamentals:
- Understanding the shebang (`#!/bin/bash`)
- Working with variables, echo, and read
- Writing basic if-else conditions

---

# 🔹 Task 1: Your First Script

## File: hello.sh

```bash
#!/bin/bash

echo "Hello, DevOps!"
````

### Make it executable

```bash
chmod +x hello.sh
```

### Run the script

```bash
./hello.sh
```

### Output

```
Hello, DevOps!
```

### What happens if we remove the shebang?

If the shebang (`#!/bin/bash`) is removed:

* The script may run using the default system shell instead of bash.
* Some bash-specific features may not work.
* It may fail if executed directly (`./hello.sh`).

The shebang tells the system which interpreter should execute the script.

---

# 🔹 Task 2: Variables

## File: variables.sh

```bash
#!/bin/bash

NAME="Vineet"
ROLE="DevOps Engineer"

echo "Hello, I am $NAME and I am a $ROLE"
```

### Run

```bash
chmod +x variables.sh
./variables.sh
```

### Output

```
Hello, I am Vineet and I am a DevOps Engineer
```

---

### Single Quotes vs Double Quotes

```bash
echo 'Hello $NAME'
echo "Hello $NAME"
```

Output:

```
Hello $NAME
Hello Vineet
```

Difference:

* Single quotes (' ') → Variables are NOT expanded.
* Double quotes (" ") → Variables ARE expanded.

---

# 🔹 Task 3: User Input with read

## File: greet.sh

```bash
#!/bin/bash

read -p "Enter your name: " NAME
read -p "Enter your favourite tool: " TOOL

echo "Hello $NAME, your favourite tool is $TOOL"
```

### Example Output

```
Enter your name: Vineet
Enter your favourite tool: Docker
Hello Vineet, your favourite tool is Docker
```

---

# 🔹 Task 4: If-Else Conditions

## File: check_number.sh

```bash
#!/bin/bash

read -p "Enter a number: " NUM

if [ $NUM -gt 0 ]; then
    echo "Number is Positive"
elif [ $NUM -lt 0 ]; then
    echo "Number is Negative"
else
    echo "Number is Zero"
fi
```

---

## File: file_check.sh

```bash
#!/bin/bash

read -p "Enter filename: " FILE

if [ -f "$FILE" ]; then
    echo "File exists."
else
    echo "File does not exist."
fi
```

---

# 🔹 Task 5: Combine It All

## File: server_check.sh

```bash
#!/bin/bash

SERVICE="nginx"

read -p "Do you want to check the status of $SERVICE? (y/n): " ANSWER

if [ "$ANSWER" = "y" ]; then
    if systemctl is-active --quiet $SERVICE; then
        echo "$SERVICE is running."
    else
        echo "$SERVICE is not running."
    fi
else
    echo "Skipped."
fi
```

### Example Output

```
Do you want to check the status of nginx? (y/n): y
nginx is running.
```

---

# 📚 What I Learned

1. The shebang defines which interpreter executes the script.
2. Variables must not have spaces around `=`.
3. Double quotes expand variables, single quotes do not.
4. `read` allows interactive user input.
5. If-else conditions enable decision-making in scripts.


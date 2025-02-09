# 🚀 **Bash Scripting Crash Course (Detailed + Use Cases)**
This crash course will cover Bash scripting concepts in depth, with **practical examples and real-world use cases**.

---

## **1️⃣ Positional Arguments (Command-Line Arguments)**
Bash scripts can accept arguments when executed.

### **Syntax**
```bash
#!/bin/bash
echo "Script Name: $0"
echo "First Argument: $1"
echo "Second Argument: $2"
echo "All Arguments: $@"
echo "Total Arguments: $#"
```

### **Run the script**
```bash
bash script.sh Hello World
```

### **Output**
```
Script Name: script.sh
First Argument: Hello
Second Argument: World
All Arguments: Hello World
Total Arguments: 2
```

### **Use Case**
✅ **Automating file operations**  
```bash
#!/bin/bash
if [ $# -ne 2 ]; then
  echo "Usage: $0 <source> <destination>"
  exit 1
fi
cp "$1" "$2"
echo "File copied!"
```
🔹 Run: `bash script.sh file1.txt file2.txt`  
🔹 Copies `file1.txt` to `file2.txt`.

---

## **2️⃣ Output/Input Redirection**
Redirecting input and output is crucial in automation.

### **Redirection Operators**
| Symbol | Description |
|--------|-------------|
| `>` | Redirect output (overwrite) |
| `>>` | Append output |
| `<` | Read from file |
| `2>` | Redirect error messages |
| `&>` | Redirect both stdout & stderr |
| `|` | Pipe output |

### **Examples**
```bash
echo "Hello World" > file.txt  # Write to file
echo "Append this" >> file.txt  # Append
cat < file.txt  # Read input
ls non_existing_folder 2> error.log  # Redirect error
ls | grep ".txt"  # Pipe output to grep
```

### **Use Case**
✅ **Logging script output**
```bash
#!/bin/bash
echo "Script started at $(date)" >> log.txt
```

---

## **3️⃣ Test Operators (File, String, Numeric Comparisons)**

### **Comparison Operators**
| Type | Operator | Example |
|------|---------|----------|
| Numeric | `-eq` (equal) | `[ $a -eq $b ]` |
| Numeric | `-ne` (not equal) | `[ $a -ne $b ]` |
| Numeric | `-gt` (greater than) | `[ $a -gt $b ]` |
| Numeric | `-lt` (less than) | `[ $a -lt $b ]` |
| File | `-f` (is file) | `[ -f "file.txt" ]` |
| File | `-d` (is directory) | `[ -d "dir" ]` |
| String | `=` (equals) | `[ "$a" = "$b" ]` |
| String | `-z` (empty) | `[ -z "$var" ]` |

### **Example**
```bash
#!/bin/bash
if [ -f "/etc/passwd" ]; then
  echo "File exists!"
else
  echo "File not found!"
fi
```

---

## **4️⃣ If/Elif/Else (Conditional Statements)**

### **Example**
```bash
#!/bin/bash
read -p "Enter a number: " num

if [ $num -gt 10 ]; then
  echo "Greater than 10"
elif [ $num -eq 10 ]; then
  echo "Exactly 10"
else
  echo "Less than 10"
fi
```

### **Use Case**
✅ **Check if a service is running**
```bash
#!/bin/bash
if pgrep "nginx" > /dev/null; then
  echo "Nginx is running"
else
  echo "Nginx is not running"
fi
```

---

## **5️⃣ Case Statements**
Used when multiple conditions exist.

### **Example**
```bash
#!/bin/bash
read -p "Enter a color: " color
case $color in
  red) echo "You chose red" ;;
  blue) echo "You chose blue" ;;
  *) echo "Invalid choice" ;;
esac
```

### **Use Case**
✅ **Simple command-line menu**
```bash
echo "Choose an option:"
echo "1. Show date"
echo "2. Show uptime"
read choice
case $choice in
  1) date ;;
  2) uptime ;;
  *) echo "Invalid choice" ;;
esac
```

---

## **6️⃣ Arrays**
Bash supports arrays to store multiple values.

### **Example**
```bash
fruits=("apple" "banana" "cherry")
echo "First fruit: ${fruits[0]}"
echo "All fruits: ${fruits[@]}"
```

### **Use Case**
✅ **Batch processing files**
```bash
files=("file1.txt" "file2.txt" "file3.txt")
for file in "${files[@]}"; do
  echo "Processing $file"
done
```

---

## **7️⃣ For Loop**
Used for iteration.

### **Example**
```bash
for i in {1..5}; do
  echo "Iteration $i"
done
```

### **Use Case**
✅ **Backup multiple files**
```bash
for file in *.txt; do
  cp "$file" backup/
done
```

---

## **8️⃣ Functions**
Functions allow code reuse.

### **Example**
```bash
greet() {
  echo "Hello, $1!"
}
greet "Shamail"
```

### **Use Case**
✅ **Repeated actions like restarting a service**
```bash
restart_service() {
  sudo systemctl restart nginx
  echo "Nginx restarted!"
}
restart_service
```

---

## **9️⃣ Exit Codes**
Every command returns a status code (`0` = success).

### **Example**
```bash
ls /non_existing_directory
echo $?  # Non-zero if failed
```

### **Use Case**
✅ **Error handling**
```bash
mkdir /root/test 2>/dev/null
if [ $? -ne 0 ]; then
  echo "Permission denied!"
fi
```

---

## **🔟 AWK (Text Processing)**
Processes text files column-wise.

### **Example**
```bash
echo "Shamail 25" | awk '{print $1}'
```
🔹 Output: `Shamail`

### **Use Case**
✅ **Extract usernames from `/etc/passwd`**
```bash
awk -F':' '{print $1}' /etc/passwd
```

---

## **1️⃣1️⃣ SED (Stream Editor)**
Used for modifying text.

### **Example**
```bash
echo "Hello World" | sed 's/World/Bash/'
```
🔹 Output: `Hello Bash`

### **Use Case**
✅ **Replace text in a file**
```bash
sed -i 's/old/new/g' file.txt
```

---

# 🎯 **Final Notes**
✅ **Run scripts**: `bash script.sh arg1 arg2`  
✅ **Make scripts executable**:  
```bash
chmod +x script.sh
./script.sh
```
✅ **Debug a script**:  
```bash
bash -x script.sh
```
✅ **Check syntax**:  
```bash
bash -n script.sh
```

---
🚀 **With these concepts, you're ready to write powerful Bash scripts!**  

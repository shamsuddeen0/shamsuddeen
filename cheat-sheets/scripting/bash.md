# 🐚 Bash Scripting for Cybersecurity

**"If you can script it, you can scale it."**

Bash (Bourne Again Shell) is a powerful scripting language used extensively in Linux/Unix systems for automation and security tasks. As a security professional, I use it to automate scans, parse logs, and build tools on the fly.

---

## 📋 Table of Contents
- [Basic Syntax](#-basic-syntax)
- [Variables](#-variables)
- [Input/Output](#-inputoutput)
- [Conditionals](#-conditionals)
- [Loops](#-loops)
- [Functions](#-functions)
- [File Operations](#-file-operations)
- [String Manipulation](#-string-manipulation)
- [Arrays](#-arrays)
- [Security Scripts](#-security-scripts-my-collection)
- [Best Practices](#-best-practices)
- [Resources](#-resources)

---

## 🛠️ Basic Syntax

### Shebang and Execution
```bash
#!/bin/bash
# This is a comment

# Make script executable
chmod +x script.sh

# Run script
./script.sh
bash script.sh
```
Basic Commands
```bash
# Print to console
echo "Hello World"
printf "Formatted: %s\n" "text"

# Exit status (0 = Success, 1 = Error)
exit 0
echo $?  # Check last exit status
```
### 📦 Variables
```bash
# Variable assignment (no spaces around =)
name="hacker"
age=25

# Use variables
echo "Name: $name"
echo "Name: ${name}"

# Command substitution
current_date=$(date)
files=$(ls -l)

# Arithmetic
count=$((10 + 5))
count=$((count * 2))

# Special variables
$0  # Script name
$1  # First argument
$2  # Second argument
$#  # Number of arguments
$@  # All arguments as separate words
$$  # Process ID
$?  # Exit status of last command
```
### 🔀 Input/Output
Reading Input
```bash
# Read user input
read -p "Enter your name: " name

# Read password (hidden)
read -s -p "Enter password: " password

# Read with timeout
read -t 5 -p "Enter quickly: " input
```
Redirection
```bash
# Output redirection
echo "text" > file.txt      # Overwrite
echo "text" >> file.txt     # Append

# Error redirection
command 2> error.log        # Redirect stderr
command 2>&1                # Redirect stderr to stdout
command &> all.log          # Redirect both

# Here document (Multi-line input)
cat << EOF
Multi-line
text
EOF
```
### ⚖️ Conditionals
If Statements
```bash
# Basic if
if [ condition ]; then
    echo "True"
fi

# If-elif-else
if [ condition1 ]; then
    echo "Condition 1"
elif [ condition2 ]; then
    echo "Condition 2"
else
    echo "Default"
fi

# One-liner
[ condition ] && echo "True" || echo "False"
```
Test Operators
```bash
# File tests
-e file    # File exists
-f file    # Regular file
-d file    # Directory
-r file    # Readable
-w file    # Writable
-x file    # Executable

# String tests
-z string  # Empty string
-n string  # Non-empty string
str1 = str2   # Equal
str1 != str2  # Not equal

# Numeric tests
$a -eq $b  # Equal
$a -ne $b  # Not equal
$a -gt $b  # Greater than
$a -lt $b  # Less than
```
Case Statements
```bash
case $port in
    22) echo "SSH" ;;
    80) echo "HTTP" ;;
    *)  echo "Unknown port" ;;
esac
```
### 🔄 Loops
For Loops
```bash
# C-style for loop
for ((i=0; i<10; i++)); do
    echo "Count: $i"
done

# Iterate over files
for file in *.txt; do
    echo "Processing: $file"
done

# Range
for i in {1..10}; do
    echo "$i"
done
```
While Loops
```bash
# Basic while loop
count=0
while [ $count -lt 10 ]; do
    echo "Count: $count"
    ((count++))
done

# Infinite loop
while true; do
    echo "Running..."
    sleep 1
done
```
### 🔧 Functions
```bash
# Definition
scan_target() {
    echo "Scanning $1..."
}

# Call function
scan_target "192.168.1.1"

# Return values
is_root() {
    if [ $EUID -eq 0 ]; then
        return 0 # True/Success
    else
        return 1 # False/Error
    fi
}
```
### 📂 File Operations
```bash
# Check if file exists
if [ -f "file.txt" ]; then
    echo "File exists"
fi

# Read file line by line
while IFS= read -r line; do
    echo "$line"
done < file.txt

# Find files
find /path -name "*.txt"
```
### 📝 String Manipulation
```bash
string="Hello World"

# Length
echo ${#string}

# Substring
echo ${string:0:5}  # First 5 characters

# Replace
echo ${string/World/Universe}

# Remove suffix
filename="image.jpg"
echo ${filename%.*} # Output: image
```
### 🧱 Arrays
```bash
# Create array
arr=(one two three)

# Access elements
echo ${arr[0]}          # First element
echo ${arr[@]}          # All elements

# Loop through array
for item in "${arr[@]}"; do
    echo "$item"
done
```
### 🛡️ Security Scripts (My Collection)

These are practical scripts for recon and monitoring.

1. Simple Port Scanner

Use when Nmap is unavailable.

```bash
#!/bin/bash

scan_port() {
    local host=$1
    local port=$2
    
    timeout 1 bash -c "echo >/dev/tcp/$host/$port" 2>/dev/null
    if [ $? -eq 0 ]; then
        echo "[+] Port $port is open"
    fi
}

read -p "Enter host: " target
for port in {1..1024}; do
    scan_port "$target" "$port"
done
```
# 2. Log Monitor

Watches auth logs for failed login attempts.

```bash
#!/bin/bash

LOGFILE="/var/log/auth.log"
KEYWORDS=("Failed password" "Invalid user" "authentication failure")

tail -f "$LOGFILE" | while read line; do
    for keyword in "${KEYWORDS[@]}"; do
        if echo "$line" | grep -q "$keyword"; then
            echo "[!] Alert: $line"
        fi
    done
done
```
#3. Backup Script
```bash
#!/bin/bash

SOURCE="/home/user/data"
DEST="/backup"
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_FILE="backup_$DATE.tar.gz"

echo "Starting backup..."
tar -czf "$DEST/$BACKUP_FILE" "$SOURCE"

if [ $? -eq 0 ]; then
    echo "Backup completed: $BACKUP_FILE"
else
    echo "Backup failed!"
    exit 1
fi
```
# 4. System Information Gathering
```bash
#!/bin/bash

echo "=== System Information ==="
echo "Hostname: $(hostname)"
echo "OS: $(uname -s)"
echo "Kernel: $(uname -r)"
echo "Uptime: $(uptime -p)"

echo -e "\n=== Network Information ==="
ip addr show | grep "inet " | awk '{print $2}'

echo -e "\n=== Disk Usage ==="
df -h | grep "^/dev"

echo -e "\n=== Top Processes ==="
ps aux --sort=-%mem | head -10
```
# 5. User Enumeration
```bash
#!/bin/bash

echo "=== User Enumeration ==="
echo -e "\n[*] Current user:"
whoami

echo -e "\n[*] User privileges:"
id

echo -e "\n[*] Sudo privileges:"
sudo -l 2>/dev/null

echo -e "\n[*] Users with shell access:"
grep -v "nologin\|false" /etc/passwd | cut -d: -f1
```
# 6. Network Connection Monitor
```bash
#!/bin/bash

echo "Monitoring network connections..."
watch -n 2 '
echo "=== Active Connections ==="
netstat -tunap 2>/dev/null | grep ESTABLISHED

echo -e "\n=== Listening Ports ==="
netstat -tulnp 2>/dev/null | grep LISTEN
'
```
# 7. File Integrity Checker

Detects if files have been modified.

```bash
#!/bin/bash

WATCH_DIR="/etc"
HASH_FILE="/tmp/file_hashes.txt"

# Create initial hashes
if [ ! -f "$HASH_FILE" ]; then
    echo "Creating initial hash database..."
    find "$WATCH_DIR" -type f -exec sha256sum {} \; > "$HASH_FILE"
    echo "Done. Run again to check for changes."
    exit 0
fi

# Check for changes
echo "Checking for file changes..."
find "$WATCH_DIR" -type f -exec sha256sum {} \; | while read hash file; do
    stored_hash=$(grep " $file$" "$HASH_FILE" | cut -d' ' -f1)
    
    if [ -z "$stored_hash" ]; then
        echo "[!] New file: $file"
    elif [ "$hash" != "$stored_hash" ]; then
        echo "[!] Modified: $file"
    fi
done
```
# 8. Simple Password Cracker (Educational)
```bash
#!/bin/bash

crack_password() {
    local hash=$1
    local wordlist=$2
    
    while IFS= read -r password; do
        computed_hash=$(echo -n "$password" | md5sum | cut -d' ' -f1)
        
        if [ "$computed_hash" = "$hash" ]; then
            echo "[+] Password found: $password"
            return 0
        fi
    done < "$wordlist"
    
    echo "[-] Password not found"
    return 1
}

read -p "Enter MD5 hash: " hash
read -p "Enter wordlist path: " wordlist
crack_password "$hash" "$wordlist"
```
# 9. Subdomain Enumeration
```bash
#!/bin/bash

enumerate_subdomains() {
    local domain=$1
    local wordlist=$2
    
    while IFS= read -r subdomain; do
        result=$(host "$subdomain.$domain" 2>/dev/null)
        
        if echo "$result" | grep -q "has address"; then
            ip=$(echo "$result" | grep "has address" | awk '{print $4}')
            echo "[+] Found: $subdomain.$domain -> $ip"
        fi
    done < "$wordlist"
}

read -p "Enter domain: " domain
read -p "Enter wordlist: " wordlist
enumerate_subdomains "$domain" "$wordlist"
```
### 🧠 Best Practices

Use meaningful variable names:

Bad: x=10

Good: port_number=10

Quote variables: Always use "$var" to handle spaces correctly.

Check command success:

```bash
command
if [ $? -eq 0 ]; then echo "Success"; else echo "Failed"; fi
```

Use ShellCheck: Always scan scripts with ShellCheck.

Fail Fast: Use set -e at the top to exit immediately on error.

Validate Input: Never trust user input.

Absolute Paths: Use /bin/ls instead of ls in critical scripts to avoid path hijacking.

### 📚 Resources


- [Bash Manual](https://www.gnu.org/software/bash/manual/)
- [ShellCheck](https://www.shellcheck.net/)
- [Bash Guide for Beginners](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)


### ⚠️ Legal Notice

WARNING: Only use these scripts on systems you own or have explicit permission to test. Unauthorized use is illegal.
Pro Tip: Always test your bash scripts in a safe environment before running them in production. Use bash -x script.sh to debug scripts by showing each command as it executes.

# 1. Basics
## This is called shebang, this tells the system which interpreter to use and it must be on the first line of the script.
#!/bin/bash

## For running a script we must have to give it execute permission, and then run it
## chmod +x script.sh
## for running
##./script.sh
### Comments
Single line:
# This is a comment
echo "Hello" # prints hello (for inline comments)
### Variables

name="Arpit"
<<usecase
 Use:
 $VAR (Unquoted / Raw Use), The variable is expanded, but no protection to white spaces, and special chars 
"$var" The variable is expanded, but it is treated as a single "word" or argument,it preserves spaces
'$VAR' No expansion occurs. The string is treated literally.Everything between the single quotes, including $ and \ (backslash), is treated as a literal character.
usecase

echo $name
echo "$name"
echo '$name'

## Reading Input

### Reading User Input, this commands takes input from user amd store it in name var which can be used later
read -p "Enter your name: " name
echo "Hello $name"

<<comment
 When running a script, you can pass values to it:
 ./script.sh arg1 arg2
Special variables:

$0  # Name of the script
$1  # First argument
$2  # Second argument
$#  # Total number of arguments passed
$@  # All arguments as separate words
$?  # Exit status of the last executed command
comment

## 2. Operators and Conditionals
<<usecase
String Comparisons
[ "$a" = "$b" ]    # Equal
[ "$a" != "$b" ]   # Not equal
[ -z "$a" ]        # True if string is empty
[ -n "$a" ]        # True if string is not empty

 Integer Comparisons

[ "$a" -eq "$b" ]  # Equal
[ "$a" -ne "$b" ]  # Not equal
[ "$a" -lt "$b" ]  # Less than
[ "$a" -gt "$b" ]  # Greater than
[ "$a" -le "$b" ]  # Less than or equal
[ "$a" -ge "$b" ]  # Greater than or equal

 File Test Operators

[ -f file.txt ]   # File exists and is regular file
[ -d folder ]     # Directory exists
[ -e file.txt ]   # File or directory exists
[ -r file.txt ]   # Read permission
[ -w file.txt ]   # Write permission
[ -x file.sh ]    # Execute permission
[ -s file.txt ]   # File exists and not empty

if, elif, else Syntax
if [ condition ]; then
  # code
elif [ another_condition ]; then
  # code
else
  # code
fi

for closing of any if, fi is required, and for executing a code in section then is required

Logical Operators

[ "$a" -gt 5 ] && echo "Greater than 5" // this checks both the conditions
[ "$a" -lt 5 ] || echo "Not less than 5" // it executes even if one statement is correct
[ ! -f file.txt ]   # NOT operator

Case Statement ( like switch)

read -p "Enter option: " choice

case "$choice" in  start)
    echo "Starting service"
    ;;
  stop)
    echo "Stopping service"
    ;;
  restart)
    echo "Restarting service"
    ;;
  *)
    echo "Invalid option"
    ;;
esac

usecase
ubuntu@ip-172-31-36-82:~/scripts$ 

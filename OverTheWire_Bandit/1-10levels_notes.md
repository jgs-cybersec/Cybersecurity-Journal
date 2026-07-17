## Bandit Level 0 → Level 1 

### Level Goal

The password for the next level is stored in a file called **readme** located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

### Linux Command

` ssh bandit0@bandit.labs.overthewire.org -p 2220`

## Bandit Level 1 → Level 2 [Filename which is also a special charcter]

### Level Goal

The password for the next level is stored in a file called **-** located in the home directory.

### Linux Command

` cat ./-`

**Description:**

`.` --> Shows the current directory

`/` --> separator

Basically this is used to tell Linux terminal that to not treat `-` as special charcter.

## Bandit Level 2 → Level 3 [Filename containing spaces]

### Level Goal

The password for the next level is stored in a file called **--spaces in this filename--** located in the home directory.

### Linux Command

` cat './--spaces in this filename--'`

**Description:**

Single qoute the filename to treat it as a single filename. Otherwise each word in the filename spaces, in, the, filename are considered as separate filename and terminal startes to search for each on of it.

`./` is used to consider the -- characters as part of filename not special characters.

## Bandit Level 3 → Level 4 [Accessing hidden files]

### Level Goal

The password for the next level is stored in a hidden file in the **inhere** directory.

### Linux Command

`ls -a`

` cat hidden`

**Description:**

`-a` --> to list all files (including hidden files) in the directory.

## Bandit Level 4 → Level 5 [Identify the human-readable file]

### Level Goal

The password for the next level is stored in the only **human-readable file** in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

### Linux Command

` cat file ./*`

**Description:**

The command displays all files and it's type. Only one will be **ASCII TEXT** that means readable. Others will be of data type which points binary text.

## Bandit Level 5 → Level 6 [Find a file with specifications]

### Level Goal

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

1. human-readable
2. 1033 bytes in size
3. not executable

### Linux Command

`find . -type f -size 1033c ! -executable`

` cat <filename>*`

**Description:**

`find` --> command to find something.

`.` --> represents current directory.

`-type f` --> File type need to be found.

`-size 1033c` --> Size of the file and `c` is used to represent bytes.

`! -executable` --> `!` is to show NOT.

## Bandit Level 6 → Level 7 [Find a file in the whole server]

### Level Goal

The password for the next level is stored **somewhere on the server** and has all of the following properties:

1. owned by user bandit7
2. owned by group bandit6
3. 33 bytes in size

### Linux Command

`find / -user bandit7 -group bandit6 -size 33c 2>/dev/null`

` cat <filename>*`

**Description:**

`/` --> Repressents the root or server.

`-user bandit7` --> File is used by bandit7

`-group bandit6` --> File is owned by bandit6

`2>` -->  The errors.

`/dev/null` --> Blackhole of Linux. All the errors are moved to this blackhole.

## Bandit Level 7 → Level 8 [exploring the content in a file]

### Level Goal

The password for the next level is stored in the file **data.txt** next to the word **millionth**

### Linux Command

`grep "millionth" data.txt`

**Description:**

`grep` --> Search for a word

### Bandit Level 8 → Level 9 [Data filtering using data manipulation tools]

### Level Goal

The password for the next level is stored in the file data.txt and is **the only line of text that occurs only once**.

### Linux Command

`sort data.txt | uniq -u`

**Description:**

`sort` --> Reads the file and arrange all the lines in alphabetical and numerical order.

`uniq` --> Filers out consecutive duplicate lines.

`-u` --> Only prints the line which is unique.

`|` --> Pipe command which is used to give the first statements output as input to the next statement to the pipe.

## Bandit Level 9 → Level 10 [Extracting human readable text from a binary file]

### Level Goal

The password for the next level is stored in the file **data.txt** in one of the **few human-readable strings, preceded by several ‘=’ characters**.


### Linux Command

`strings data.txt | grep "=="`

**Description:**

`strings` --> To extract readable text.

`==` --> double equal to symbol is used to eliminate assignment(a=1) statements from search and output.







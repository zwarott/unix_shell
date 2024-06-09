# Basic Unix Commands

## Table of Contents

- [Terminal Administration](#terminal-administration)
- [File System Navigation](#file-system-navigation)
- [File and Directory Information and Manipulation](#file-and-directory-information-and-manipulation)
- [Text Information and Manipulation](#text-information-and-manipulation)
- [File Compression and Archiving](#file-compression-and-archiving)
- [System Information](#system-information)
- [Networking](#networking)
- [User Management](#user-management)
- [Package Management](#package-management)
- [Process Management](#process-management)
- [Environment Administration](#environment-administration)


## Terminal Administration

### :question: man 
Everytime you do not know how to use certain command, type below command to get the manual:
```
man <command>
```

### :grey_question: tldr
Get a quick overview of a certain command. Require installation of tldr pages.
```
pip install tldr
```
What is `cd` command and how to use it?
```
tldr cd
```

### :star2: clean
Clear the screen (equivalent to pressing Control-L in Bash shell)
```
clear
```
Clear the screen but keep the terminal's scrollback buffer
```
clear -x
```

### :books: history
Display the commands history list with line numbers
```
history
```
Clear the commands history list (only for  current bash shell)
```
history -c
```


## File System Navigation

### :left_right_arrow: pwd
Whenever you feel lost in the filesystem, call the `pwd` command to know where you are.   
Print the current directory path
```
pwd
```

### :open_file_folder: dirname
Calculate the parent directory of a given path
```
dirname <path/to/file>
```

### :bookmark: basename
Show only the file name from a path
```
basename <path/to/file>
```

### :evergreen_tree: tree
Visually displays the directory structure of a file system in a tree-like format. Require installation
```
pip install treelib
```
Displays directories only
```
tree -d
```
A tree-like structure showing directories and files up to two levels deep
```
tree -L 2
```
Display the size of files and directories within up to two levels deep
```
tree --du -h -L 2
```
Display occurrence of specific file pattern within the directory structure
```
tree -P '*.txt' -L 6
```

### :bookmark_tabs: cd
Change directory → root Directory
```
cd /
```
Change directory → home directory (or type simple `cd`)
```
cd ~
```
Change directory → directory one level back
```
cd ..
```
Change directory → directory two level back
```
cd ../..
```
Change directory → previous directory you last browsed
```
cd -
```

### :clipboard: ls
   
List files in current directory
```
ls
```
List files in selected directory (on Desktop)
```
ls ~/Desktop
```
List files one per line in current directory
```
ls -1
```
List all files, including hidden files in current directory
```
ls -a
```
List all files (including hidden files) one per line
```
ls -1a
```
Long format list of all files in current directory   
* Including permission, ownership, size and modification date
```
ls -l
```
Including hidden files
```
ls -la
```
Human readable file sizes in current directory   
* Long format list with size displayed using human readable units (such as KB, MB, GB) → sorted alphabetically
```
ls -lh
```
Sorted by file sizes descending
```
ls -lhS
```
Sorted by files sizes descending including hidden files
```
ls -lhaS
```
Sorted by modification date (oldest first)

```
ls -lhtr
```
The `*` (asterisk) can be used as a wildcard to match zero or more characters
```
ls *.txt
```
The `?` (question mark) can be used to match a single character.
```
ls ????_?????. txt
```
The `[]` (square brackets) can be used to match any number of characters inside them.
```
ls t[o]do_*.???
```


## File and Directory Information and Manipulation

### :heavy_plus_sign: :file_folder: mkdir
Create a directory using `mkdir` command   
Create a new directory in current directory
```
mkdir new_folder
```
Create multiple directories in current directory 
```
mkdir folder_1 folder_2 folder_3
```
Create multiple nested directories in current directory 
```
mkdir -p folder_1/folder_11
```
Create project root folder and subdirectories
```
mkdir -p nhl_analysis/{scrapers,models,database/versions}
```

### :x: :file_folder: rmdir
Delete a folder using `rmdir` command. The folder you delete must be empty!   
Use `rm -r` to remove non-empty directories or see rm part!   
Delete a directory from current directory
```
rmdir new_folder
```
Delete multiple directories in current directory at once
```
rmdir folder_1 folder_2 folder_3
```
Remove the target and its parent directories (useful for nested directories)
```
rmdir -p folder_1/folder_11
```
Delete a directory with files in them (in current directory)
```
rm -r folder_1
```

### :file_folder: mv
Move or rename files and directories using `mv` command.   
Rename file in current directory
```
mv file_1.txt file_2.txt
```
Move files into another directory, keeping the filenames
```
mv file_1.txt file_2.txt file_3.txt ~/Documents/folder_1
```
Move all files by certain pattern from one folder to another one
```
mv name_patter.* target_folder/
```
Prompt for confirmation before overwriting existing files, regardless of file permissions
```
mv -i file_1.txt file_2.txt file_3.txt ~/Documents/folder_1
```
Move files in verbose mode, showing files after they are moved and prompt for confirmation before overwriting existing files, regardless of file permissions
This is a better choice than command above, because we get information about file overwriting!   
```
mv -vi file_1.txt file_2.txt file_3.txt ~/Documents/folder_1
```
If there are not the same files we do not confirm to move the files. We can move all files from the directory using * after selected directory.
```
mv -vi folder_111/* folder_111_copy/
```
Rename 99 files with specific pattern at once   
* You first declare two variables: replace_source and replace_target as placeholders for the space and the underscore characters.
* You loop over all the *.csv files in the current folder.
* For each filename, you create a new_filename by replacing each space by an underscore.
* And you rename the file from its current filename to the new filename with the mv command.
```
replace_source='_'
replace_target='file_'
for filename in ./*.csv; do
new_filename=${filename//$replace_source/$replace_target}
mv "$filename" "$new_filename"
done
```


## Text Information and Manipulation

### :eyes: grep
Find patterns in files using regular expressions using grep command.   
You can use grep to search in files, or combine it with pipes to filter the output of another command.   
`grep` stands for global regular expression print.      
   
Search for a pattern within a file
For example here's how we can find the occurences of the `wo` word in the `file_3.txt` file in current directory
```
grep "wo" file_3.txt
```
Show the line numbers
```
grep -n "wo" file_3.txt
```
Print 2 lines before, and 2 lines after the matched line   
One very useful thing is to tell grep to print 2 lines before, and 2 lines after the matched line, to give us more context. 
That's done using the `-C` option, which accepts a number of lines.
```
grep -nC 2 "wo" file_3.txt
```
Count the number of rows that contain at least one occurrence of certain pattern
```
grep ",Czech Republic," squad.csv | wc -l
```
Count searching pattern within a file
```
grep -c "wo" file_3.txt
```
Search inside a directory recursively   
Here it will search everything inside the current directory and its child directories.
```
grep -r "FILE" .
```

### :wc: wc
Count lines in file
```
wc -l file_3.txt
```
Count words in file
```
wc -w file_3.txt
```
Count characters (bytes) in file
```
wc -c file_3.txt
```
Count line, words, characters in file at once
```
wc file_3.txt
```
Use standard input to count lines, words and characters (bytes) in that order
```
ls -lh | wc
```
Count the number of files in a certain directory
```
ls -l ./squad/ | wc -l
```


## File Compression and Archiving
## System Information
## Networking
## User Management

### :raising_hand: who + whoami
Display the users logged in to the system
```
who
```
List the current terminal session details
```
who am i
```
Print the user name currently logged in to the terminal session
```
whoami
```

## Package Management
## Process Management
## Environment Administration






















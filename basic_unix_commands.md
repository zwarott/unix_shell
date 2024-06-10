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

### :star: touch
Create specific files in current directory
```
touch file_1.txt file_2.txt
```
Create 99 files a name them with specific pattern at once
```
for i in {1..100}
do
touch "test_$i".csv
done
```

### :x: rm
Delete a single file in current Directory
```
rm <file_name>
```
Delete multiple files in current directory
```
rm <file_name> <file_name> <file_name>
```
Delete a directory with files in them (in current directory)
```
rm -r <folder_1>
```
Interactively remove multiple files, with a prompt before every removal
```
rm -ri <folder_1>
```
Remove files in verbose mode, printing a message for each removed file
```
rm -rv <folder_1>
```
Remove files in verbose and interactive mode for control removing files
```
rm -rvi <folder_1>
```
Remove all files and directories from selected directory in verbose mode → quick way!
* zsh is required!
* The default directory is not deleted if we using * within command!
* If we do not use * within command, the folder with all contents are deleted and we do not get any notification from zsh!
```
rm -rv folder_1/*
```
* Remove all files from current directory using * → zsh notification!
```
rm -rv *
```
Remove all .DS_Stores from the repo
```
find . -name .DS_Store -print0 | xargs -0 git rm --ignore-unmatch
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

### :card_index: cp + ditto
Create file copy in current directory
```
cp file_1.txt file_1_copy.txt
```
Copy a file from current directory into another directory, keeping the filename
```
cp file_1_copy.txt ~/Documents/folder_1
```
Copy a file from current directory into another directory and change the filename
```
cp file_1_copy.txt ~/Documents/folder_1/file_1_backup.txt
```
Copy selected file to another location, in verbose (shows files as they are copied) and interactive (prompts user before overwriting) mode from current directory
```
cp -vi file_1_copy.txt ~/Documents/folder_1/file_1_backup.txt
```
Copy a directory with contents to another location, in verbose (shows files as they are copied) and interactive (prompts user before overwriting) mode from current Directory
* If the destination exists, the directory is copied inside it
* If there are not the same files we do not confirm to move the files → if there are we have to confirm
```
cp -vRi folder_111 ~/Documents/folder_1
```
* We can move all files from the directory using `*` after selected directory (without default directory)
```
cp -vRi folder_111/* ~/Documents/folder_1
```
* The same result if we want to copy a single file into different directory
```
cp -vRi folder_111/file_1.txt ~/Documents/folder_1/
```
We can use the `—r` flag to copy a directory. The following command will copy everything that is inside the `todo` folder to a folder called `bu`.
```
cp -r todo bu
```
Copy the contents of a folder from one place to another
```
ditto -v ~/Desktop/ ~/Downloads
```
Copy the contents of a existing folder from one place to another (and create new folder)
```
ditto -v path/to/directory/* path/to/new/created/directory/
```

### :mag_right: find
Find all the files under the current tree that have the `.shp` extension and print the relative path of each file matching
```
find . -name '*.shp'
```
Find directories under the current tree matching the name in current directory
```
find . -type d -name '*h*'
```
Find files matching a given pattern with specific paths in current directory
```
find . -name '*.shp' -path '*/shp/*'
```
Search files under multiple root trees
```
find ~/Document/GIS/STMAP_1935-36-37-38/ ~/Documents/GIS/STMAP/ -name '*hranice_n*.shp'
```
Find files matching a given pattern, excluding specific paths in current directory
```
find . -name '*.shp' -not -path '*/shp/*'
```
Search files that have more than 10 MB in current directory
```
find . -type f -size +10M
```
Search files bigger than 10 MB but smaller than 20 MB in current directory
```
find . -type f -size +10M -size -20M
```
Search files edited more than 3 days ago in current directory in current directory
```
find . -type f -mtime +3
```
Delete all the files edited in the last 24 hours in current directory
```
find . -type f -mtime -1 -delete
```
Find empty (0 byte) files and delete them in current directory
```
find . -type f -empty -delete
```
Run a command for each file (use `{}` within the command to access the filename) in current directory
* wc -l command counts lines in file
```
find . -name '*.csv' -exec wc -l {} \;
```
Remove all .DS_Stores from the repo
```
find . -name .DS_Store -print0 | xargs -0 git rm --ignore-unmatch
```

### :book: open
Open a file with the associated application in current directory
```
open text.txt
```
Open a certain directory in Finder app
```
open ~/Desktop
```
Open the current directory in Finder
```
open .
```
Run a graphical macOS [a]pplication
* after typing open -a we get list of available application to open.
```
open -a
```
Open all the files of a given extension in the current directory with the associated application
```
open *.png
```
[R]eveal a file in Finder
```
open -R text.txt
```

### :twisted_rightwards_arrows: xargs
Remove some specific files from a directory. Those files are listed inside a text file.
* Remove specific files that are written in to_remove.txt file. Their names are used as inputs to remove command, 
whereas `-p` flag asks us if we really want to remove these files.
```
cat to_remove.txt | xargs -p rm
```
Remove all .DS_Stores from the repo
```
find . -name .DS_Store -print0 | xargs -0 git rm --ignore-unmatch
```

### :sparkler: qlmanage
Display QuickLook for one or multiple files
```
qlmanage -p squad.csv
```

### :page_with_curl: :information_source: file
Give a description of the type of the specified file. Works fine for files with no file extension
```
file ops_20.csv
```

## Text Information and Manipulation

### :paw_prints: cat
Print the contents of a file in current directory to the terminal
```
cat file_1.txt
```
Concatenate several files into an output file in current directory
* Concatenated two text without space and default text from `file_3.txt` was removed
```
cat file_1.txt file_2.txt > file_3.txt
```
Append several files to an output file in current directory
* Appended two text without space and default text from `file_3.txt` was unchanged
```
cat file_1.txt file_2.txt >> file_3.txt
```
Number all output lines
* When watching source code files it's great to see the line numbers, and you can have cat print them using the `-n` option
```
cat -n _5t.csv
```
Add a number to non-blank lines only using `-b`
```
cat -b file_3.txt
```
Here we are sorting the `todo.txt` file in reverse order by combining the `cat` and `sort` command.
```
cat todo.txt sort -r
```

### :black_joker: echo
Create file with given message in current folder
```
echo "Hello World" > file_1.txt
```
Append a message to the existing file
```
echo "Python" >> file_1.txt
```

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

### :cancer: diff
Show me difference between content of two files
```
diff squad.csv squad_data.csv
```
Show me difference between content of two files — Git output
```
diff -c squad.csv squad_data.csv
```

### :arrow_up_down: head + tail 
Extract 20 lines starting at line 100 and save output into a new file
* This command counts the first line (header) as well
```
head -n 120 adult.csv | tail -n 20 > adult_sample.csv
```

### :bookmark_tabs: :high_brightness: sort + uniq
Count duplicate lines only
```
sort squad.csv | uniq -d | wc -l
```
Count unique lines only
```
sort squad.csv | uniq -u | wc -l
```
Sort in reverse and outputs the first 3 duplicates (include header)
```
sort squad.csv | uniq -c | sort -r | head -n 3
```

### :arrow_heading_up: pbcopy
Copy content of csv file to the clipboard
```
cat big.csv | pbcopy
```
Copy last row from csv file to the clipboard
```
cat big.csv | tail -1 | pbcopy
```
Place the contents of a specific file in the clipboard
```
pbcopy < path/to/file
```

### :arrow_heading_down: pbpaste
Use the contents of the clipboard as input to a command
```
pbpaste | cat
```
Write the contents of the clipboard to a file
```
pbpaste > path/to/file
```

### :arrow_down: :clipboard: awk
Extract column of text - print the 5th column   
`,` is column separator
```
awk -F, '{print $5}'
```

### :pencil2: sed
Replace all `NULL` values with no values `’’` and create backup file
* Backup file in format `squad.csvbak`
```
sed -i bak 's/,NULL/''/g' squad.csv
```
* Output save into a new file
```
sed "s/<string to replace>/<string to replace it with>/g" <source_file> > <target_file>
```
* Other option how to replace specific character by empty string
* :exclamation: Keep in mind, if source file is same as target file, output file will be empty!!!
```
sed "s/, ?,/,,/g" adult.csv >  adult.csv
```

### :scissors: cut
Select column to work on and display first 3 values including header as well   
`cut` takes two main flags: `-d` to specify the column delimiter and `-f` to specify the columns you want to work on
```
cut -d "," -f 2 squad.csv | head -3
```
Display only unique names from first name column (without header) and sort them
* There are 25 rows → so apply `tail -n 24` to eliminate header row
```
cut -d "," -f 2 squad.csv | tail -n 24 | sort | uniq -c
```
Remove specific column and result save into a new csv file   
* Remove last column (4th column)
```
cut -d "," -f1-3  goal_data.csv > goal_updated.csv
```
* Remove the second column
```
cut -d "," -f1,3-  goal_data.csv > goal_updated.csv
```

### :repeat: tr
* It is recommended to use this command for replacing characters of the same lengh
Replace all occurrences of a character in a file → only print the result
```
tr "find_character" "replace_character" < path/to/file
```
Replace all occurrences of a character in a file → replace in the file
```
tr "find_character" "replace_character" < path/to/old/file > path/to/new/file
```
Replace `,` in the `test_1.csv` by `;` and save results into `test_2.csv`
```
tr "," ";" < test_1.csv > test_2.csv
```


## File Compression and Archiving

### :postbox: tar
Create an archive named with the content of all the files in current directory (keeping original files)
```
tar -cf archive.tar *
```
Create an archive named with the content of all the files in current directory (keeping original files) – size comparison with additional compression
```
tar -cf archive.tar *
```
```
tar -czf archive.tar *
```
```
tar -czf archive.tar.gz *
```
```
tar -czf archive.tgz *
```
If it’s a large folder, you may want to monitor the process by adding the `v` flag
```
tar -czvf archive.tgz *
```
Lis[t] the contents of a tar [f]ile [v]erbosely
```
tar -tvf archive.tar
```
E[x]tract a (compressed) archive [f]ile into the current directory [v]erbosely
```
tar -xvf archive.tgz
```

### :inbox_tray: zip
Print a all archive contents
```
zip -sf ./aa.zip *
```
Add multiple files to zip compress in current directory
```
zip aaa.zip qgis_domeny/ qgis_vzorove_datove_struktury
```
Add files/directories to zip compress with processing overview and total compress info in current directory
```
zip -rv ./files.zip *
```
Add files/directories to zip compress with quiet processing in current directory
```
zip -r -q ./files.zip *
```
Archive all files/directories in current folder e[x]cluding specified ones
```
zip -r ./files.zip * -x ./file_1.txt
```

### :outbox_tray: unzip
List the contents of a zip file without extracting
```
unzip -l files.zip
```
Extract zip file(s) (for multiple files, separate file paths by spaces)
```
unzip files.zip
```
Extract zip files(s) to given path
```
unzip files.zip -d ~/Documents/
```


## System Information

### :minidisc: df
Display all filesystems and their disk usage in human-readable form
```
df -h
```
Display the filesystem and its disk usage containing the given file or directory in human-readable form
```
df -h /Users/zwarott/Documents/Python/Learning/whufc
```

### :symbols: type
What type of command `pwd` is?
```
type pwd
```


## Networking

### :arrow_down: curl  
Download the contents of a URL to a file
```
curl <path/to/file/on/web> -o <where/to/store/on/local/disk> 
```


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

### :top: top
Start top sorting processes by internal memory size
```
top -o rsize
```

### :runner: ps
Get information about running processes
```
ps
```


## Environment Administration

### :question: which
Locate a `python` executable fiel
```
which python
```
### :seedling: printenv + export + env
Display key-value pairs of all environment variables
```
printenv
```
Set up temporary variable
```
variable_name=variable_value
```
Print out temporary variable
```
echo $variable_name
```
Set up permanent variable (using zsh SHELL)
* which shell I use
```
echo $SHELL
```
* set up permanent variable
```
echo "export PYTHONPATH=." >> ~/.zshrc
```
* confirm the export command is written
```
cat ~/.zshrc
```
* execute the config file to set variable permanently
```
source ~/.zshrc
```
* check out if the variable is set permanently with
```
echo $PYTHONPATH
```
Remove variable from the environment
```
env -u variable_name
```

# Linux

## Content

[1. Installation Linux to PC](#1-installation-linux-to-pc)<br>
[2. Simple commands](#2-simple-commands)<br>
[3. Files And Directories Navigation](#3-files-and-directories-navigation)<br>
[4. Work with files](#4-work-with-files)<br>
[5. Work With Direstories](#5-work-with-direstories)<br>

## 1. Installation Linux to PC

## 1.1 Installation VM

1. Source for installation [Oracle VirtualBox](https://www.virtualbox.org/)
2. Download Linux operation system (**Ubuntu 22.04 LTS** for example)
3. Install to VM Linux -> all recomended settings but if tou want you can to change it after.
4. After installation Ubuntu starts in small window. To repeare this you can install additions from cd

![Alt text](images/cd_insert_additions.png)

## 1.2 Prepeare terminal

1. Terminal -> preference -> Profiles -> Edit ptofile

2. What's mean in terminal?

    ```linux
    username@linux:~$
    username - is a current user
    linux - is a current server
    ~ - we are in ROOT directory
    ```

## 2. Simple Commands

|Command|Description|
|-:|:-|
|uptime|Show current time, how much the PC is running, how users are connected, load average|
|uname|Show current OS|
|uname -a|More details of current OS|
|lscpu|Processsor information|
|clear| Clear of window in terminal|
|ls|List of current directory. Show names of all files and directories in current directory|
|ls -l|List of current directory in details|
|ls -la|List of current directory in details and hidden files, -a - ALL|
|echo|Show text. Using for programming scripts|
|echo $PATH|Environment variables. Show directories where Linux start searching commands from user|
|LALT+F3|Switch from GUI to text terminal|
|LALT+Fxx|New session where xx - number of your screen|
|LALT+F7|Switch back to GUI|
|man -k <word>|Show all commands and description of commands included key word. man - manual, -k - key word|
|CTRL+C|Cancel of some event|
|CTRL+Z|Go back from current process and this process still running in background|
|fg|Return to process which running on background|
|man \<command>|Full description of this command|
|/\<word>|Searching of word in file editor|
|q|Exit from file editor|
|info \<command>|Short description of this command|
|whatis \<command>|About command|
|whereis \<command>|Show path where is this command is placed|
|locate|Show path where is this command located. Used to find file|
|ps|Show which processes are running in current PC|
|ls -la -R /|List of all files, all directories in all disks|
|sudo|**S**uper**U**ser **DO** with admin permission. Need enter password|

## 3. Files And Directories Navigation

|Command|Description|
|-:|:-|
|cd \</path>|Change directory|
|cd /|Change directory to ROOT|
|pwd|Show you current directory path. **P**rint **W**orking **D**irectory|
|cd ..|Return back directory an one level up|
|cd ../..|Return back a two levels up|
|cd or cd ~|Return to home directory. ~ = /home/username|

## 4. Work with files

|Command|Description|
|-:|:-|
|cat \<filename>|Read the file|
|more \<filename>|Read file row-by-row. To read next row press Enter|
|less \<filename>|Read file, looks like "man": arrow_up/arrow_down to navigate, / to searching the word, q to quit from file|
|touch \<filename>|Create new file, if file is not exist|
|touch \<filename>|Update file with \<filename>|
|cp \</src_dir/filename> <dest_dir>|Copy file ***from*** source directory ***to*** target directory. Present absolute path to directories|
|rm \</src_dir/filename>|Remove file with \<filename>. Remove ***where*** and ***what***|
|cp \</src_dir/filename?> -v <dest_dir>|Copy file with name \<filename> and any symbol on place '?' **ONLY ONE SYMBOL!**. -v -> **V**erbouse for visualisation of process|
|cp -R \<src_dir> <dest_dir>|Copy all files from one directory to another directory. -R => recursevelly|
|mv \<filename> <new_filename>|Rename/replace file. dot before filename (\<.filename>) means that file is hidden. File will be replaced when \<new_filename> is directory absolute path.|

## 5. Work With Direstories


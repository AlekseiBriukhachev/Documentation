# Linux

## Content

[1. Installation Linux to PC](#1-installation-linux-to-pc)<br>
[2. Simple commands](#2-simple-commands)<br>
[3. Files And Directories Navigation](#3-files-and-directories-navigation)<br>
[4. Work with files](#4-work-with-files)<br>
[5. Work With Direstories](#5-work-with-direstories)<br>
[6. Links creating](#6-links-creating)<br>
[7. Commands *find, cut, sort, wc, I*](#7-commands-find-cut-sort-wc-i)<br>

## 1. Installation Linux to PC

### 1.1 Installation VM

1. Source for installation [Oracle VirtualBox](https://www.virtualbox.org/)
2. Download Linux operation system (**Ubuntu 22.04 LTS** for example)
3. Install to VM Linux -> all recomended settings but if tou want you can to change it after.
4. After installation Ubuntu starts in small window. To repeare this you can install additions from cd

![Alt text](images/cd_insert_additions.png)

### 1.2 Prepeare terminal

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
|ls -la|List of current directory in details and hidden files, **-a** -> ALL|
|echo|Show text. Using for programming scripts|
|echo $PATH|Environment variables. Show directories where Linux start searching commands from user|
|LALT+F3|Switch from GUI to text terminal|
|LALT+Fxx|New session where xx - number of your screen|
|LALT+F7|Switch back to GUI|
|man -k <word>|Show all commands and description of commands included key word. **man** -> manual, **-k** -> key word|
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
|cd or cd ~|Return to home directory. **~** = /home/username|

## 4. Work with files

|Command|Description|
|-:|:-|
|cat \<filename>|Read the file|
|more \<filename>|Read file row-by-row. To read next row press Enter|
|less \<filename>|Read file, looks like "man": **arrow_up/arrow_down** to navigate, **/** to searching the word, **q** to quit from file|
|touch \<filename>|Create new file, if file is not exist|
|touch \<filename>|Update file with \<filename>|
|cp \</src_dir/filename> <dest_dir>|Copy file ***from*** source directory ***to*** target directory. Present absolute path to directories|
|rm \</src_dir/filename>|Remove file with \<filename>. Remove ***where*** and ***what***|
|cp \</src_dir/filename?> -v <dest_dir>|Copy file with name \<filename> and any symbol on place **?** ***!!ONLY ONE SYMBOL!!***. **-v** -> verbouse for visualisation of process|
|cp -R \<src_dir> <dest_dir>|Copy all files from one directory to another directory. **-R** -> recursevelly|
|mv \<filename> <new_filename>|Rename/replace file. dot before filename (\<.filename>) means that file is hidden. File will be replaced when \<new_filename> is directory absolute path.|

## 5. Work With Direstories

|Command|Description|
|-:|:-|
|mdkdir \<dir_name>|Create directory|
|mkdir -p \<abs_path_to_dir/new_dir_name>|Create directory inside new created directory. **-p** -> parent|
|mv \<old_dir_name> <new_dir_name>|Rename/replace directory|
|rmdir \<dir_name>|Remove directory ***ONLY IF DIRECTORY IS EMPTY***|
|RM -R \<dir_name*>|Remove directory. **-R** -> recursevelly, **\*** -> any symbols after directory name. That's mean it will delete all directories started with **\<dir_name>**|
|cp -R \<dir_name_1> <dir_name_2>|Copy one direcory to another recursevelly|
|sudo rm -R / --no-preserve-root|Remove all in **ROOT** directory. ***!!!DANGEROUS KILL THE LINUX OS!!!***|

## 6. Links creating

What is "link" - link is like shortcut to directory or to file, virtual presenting of file or directory. 

1. Symbolic link

    `username@lnux:~/Documents$ ln -s \<on_what> <where> <link_name>`

    Description:
    |Part of command|Description|
    |-:|:-|
    |ln|Create link command|
    |-s|Symbolic link|
    |\<on_what>|File or directory of link created. Always recomended to write absolute path to file or directory|
    |\<where>|Where you want to placed this link|
    |\<link_name>|Name of link|

2. Link as duplicate

    Duplicate is create ONLY on file.

    `username@lnux:~/Documents$ ln \<filename> <filename_duplicate>`

    This create idle duplicate of file with the same size, creating date and other fields.

    ```
    -rw-rw-r-- 2 username username 153 Nov 21 09:16 file1.txt
    -rw-rw-r-- 2 username username 153 Nov 21 09:16 file1duplicate.txt
    ```
    Number after attributes `-rw-rw-r--` show how much duplicates has file. If you change one of two files it will be changed both files. If you delete one of file another file will stay without changing.

## 7. Commands *find, cut, sort, wc, I*

1. Command ***find***
    
    search for any files in a directory hierarchy

    `username@linux:~$ find <path> -name <filename>`

      Description:
    |Part of command|Description|
    |-:|:-|
    |find|Command|
    |\<path>|Where do you want to search file. Absolute path|
    |-name|Searching by filename. Can be another attribute|
    |\<filename>|Name of searching file. Can be for examples: |
    ||***"\*.txt"*** what means all files with extention txt|
    ||can be ***"file\*.txt"*** what means file with name start with ***file***|

2. Command ***wc*** - **W**ord **C**ount

    `username@linux:~$ wc \<filename>` 

    This comand is counting and present numbers of  raws, words and symbols in this file. This command can be used with different attributes:

    |Attribute|Description|
    |-:|:-|
    |-l| Present only number of raws|
    |-w|Present only number of words|
    |-s|Present only number of symbols|

3. Command ***sort***

    Used for sorting of file content without any changing of file - only present to display sorted content.

    `username@linux:~$ sort \<filename>`

    Using attribute **-n** - sorting of content by numbers order.

4. Command ***cut***

    Used for cutting and display only some content which we want to read. For this the first we need to find some delimiter between fields of one raw, for example **>** this symbol. 

    `username@linux:~$ cut -d ">" -f 3 \<filename>`

      Description:
    |Part of command|Description|
    |-:|:-|
    |cut|Command|
    |-d|Attribute delimiter|
    |">"|Delimiter what you want to use|
    |-f|Attribute number of fields|
    |3|Field bunber|
    |\<filename>|Name of file to analise|

We can start command by command in linux.

`username@linux:~$ cut -d ">" -f 3 \<filename> | sort`

| - is named ***pipe*** and it;s separate of commands. That's mean start first command and than after start second command and finally display the result of both commands.
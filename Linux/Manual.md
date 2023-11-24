# Linux

## Content

[1. Installation Linux to PC and introduction](#1-installation-linux-to-pc-and-introduction)<br>
[1.1 Installation VM](#11-installation-vm)<br>
[1.2 Prepeare terminal](#12-prepeare-terminal)<br>
[2. Work with terminal and base commands](#2-work-with-terminal-and-base-commands)<br>
[2.1 Base Commands](#21-base-commands)<br>
[2.2 Files And Directories Navigation](#22-files-and-directories-navigation)<br>
[2.3 Work with files](#23-work-with-files)<br>
[2.4 Work With Direstories](#24-work-with-direstories)<br>
[2.5 Links creating](#25-links-creating)<br>
[2.6 Commands *find, cut, sort, wc, | (pipe)*](#26-commands-find-cut-sort-wc--pipe)<br>
[2.7 Command *grep* and regular expressions](#27-command-grep-and-regular-expressions)<br>
[2.8 Redirection of output](#28-redirection-of-output)<br>

## 1. Installation Linux to PC and introduction

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

## 2. Work with terminal and base commands

### 2.1 Base Commands

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

### 2.2 Files And Directories Navigation

|Command|Description|
|-:|:-|
|cd \</path>|Change directory|
|cd /|Change directory to ROOT|
|pwd|Show you current directory path. **P**rint **W**orking **D**irectory|
|cd ..|Return back directory an one level up|
|cd ../..|Return back a two levels up|
|cd or cd ~|Return to home directory. **~** = /home/username|

### 2.3 Work with files

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

### 2.4 Work With Direstories

|Command|Description|
|-:|:-|
|mdkdir \<dir_name>|Create directory|
|mkdir -p \<abs_path_to_dir/new_dir_name>|Create directory inside new created directory. **-p** -> parent|
|mv \<old_dir_name> <new_dir_name>|Rename/replace directory|
|rmdir \<dir_name>|Remove directory ***ONLY IF DIRECTORY IS EMPTY***|
|RM -R \<dir_name*>|Remove directory. **-R** -> recursevelly, **\*** -> any symbols after directory name. That's mean it will delete all directories started with **\<dir_name>**|
|cp -R \<dir_name_1> <dir_name_2>|Copy one direcory to another recursevelly|
|sudo rm -R / --no-preserve-root|Remove all in **ROOT** directory. ***!!!DANGEROUS KILL THE LINUX OS!!!***|

### 2.5 Links creating

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

### 2.6 Commands *find, cut, sort, wc, | (pipe)*

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

5. Join commands with pipe

    We can start command by command in linux.

    `username@linux:~$ cut -d ">" -f 3 \<filename> | sort`

    | - is named ***pipe*** and it;s separate of commands. That's mean start first command and than after start second command and finally display the result of both commands.

### 2.7 Command *grep* and regular expressions

Command **grep** is using to search text in files. This command is case sensitive.

`username@linux:~/Documents$ grep \<search_word> <where_path>`

Description:
|Part of command|Description|
|-:|:-|
|grep|Command name|
|-i|Ignore case sensitive|
|linux|Word searched in file|
|./|Current directory|
|*|All files in the directory|

Regular expressions:
|Regular Expression|Description|
|-:|:-|
|[A-Z]*|Any words contains only capital letters|
|[0-9]*|Any numbers|
|[A-Za-z]*@[A-Za-z]*.com|Simple regular expression for searching of mails ends witn ***.com***|
|www\.[a-z]*\.com|Any web url ends with ***.com***|

### 2.8 Redirection of output

If we want to make some sorting for example and result of command *sort* save to another file we can use use redirection of output **\>** using this symbol.

`username@linux:~/Documents sort \<filename> > <new_filename>`

Description:
|Part of command|Description|
|-:|:-|
|sort|Awesome command which display result on terminal|
|\<filename>|Operated file|
|\<new_filename>|Target file to save the result of command operation. If file is not exist, file will create automatically. If you redirect output to file witch you operate (filename = new_filename) this file will be erase. **Reason:** this redirection first execute second part (create new file to save result) and after execute first part. And if you save result to the same file it will failed|

To append some content from another file use symbol **\>>**

`username@linux:~/Documents sort \<filename> >> <new_filename>`

Usefull command with ***grep*** - imagine we want to find some text in some directory which cam throw errors like permission denied or somethig like this and we want to save success result in one file and errors result in another file we can use next command:

`username@linux:~$ grep username /etc/* > good.txt 2> errors.txt`

Description:
|Part of command|Description|
|-:|:-|
|grep|Command|
|username|Searching word in files in directory|
|/etc/*|Awesome path where locate some file which we want to searched|
|>|Redirect of success result to file|
|good.txt|File with success result of searching|
|2>|Sort and redirect of error results of searching|
|error.txt|Resuy file with errors|
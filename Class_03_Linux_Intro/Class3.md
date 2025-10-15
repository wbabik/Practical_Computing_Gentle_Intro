# Class 3 

# Introduction to Linux command line, connecting to a remote Linux machine, moving around in the Linux system
  * [Why is it worth learning to work with the command line?](#why-is-it-worth-learning-to-work-with-the-command-line)
  * [Linux - basics](#linux---basics)
  * [How to open a terminal?](#how-to-open-a-terminal)
  * [Working in a Linux terminal](#working-in-a-linux-terminal)
      * [Exercise 1](#exercise-1)
      * [The anatomy of a command](#the-anatomy-of-a-command)
  * [Getting around in the Linux environment: commands to get you started.](#getting-around-in-the-linux-environment-commands-to-get-you-started)
      * [Exercise 2](#exercise-2)
      * [Now, let's inspect what we have created, and how to navigate!](#now-lets-inspect-what-we-have-created-and-how-to-navigate)
      * [Exercise 3](#exercise-3)
  * [Getting around in the Linux environment: more commands, and how to use them!](#getting-around-in-the-linux-environment-more-commands-and-how-to-use-them)
      * [Exercise 4](#exercise-4)
  * [Making your life easier, and working with real files!](#making-your-life-easier-and-working-with-real-files)
      * [Exercise 5](#exercise-5)
      * [Exercise 6](#exercise-6)
      * [Exercise 7](#exercise-7)

***
  
## Why is it worth learning to work with the command line?

For a computer user accustomed to working in the graphical mode (that is, almost every user), the ability to work in text mode may seem superfluous and old-fashioned. It is not so. First, many programs used in research (and not only) do not work in a graphic environment. Equally importantly, many tasks that are simple to do in the command line, are very difficult to do in the point-and-click Graphical User Interface (GUI). Think, how would you carry out the following task?:

We collected 20,112 text files in the `/dane/epidemia` directory on a remote server you will connect to in a couple of minutes. Each of the files contains information on one of the recent cases of hemorrhagic fever (HFRS) in Poland. The second line of each file contains the name of the city where the patient was diagnosed. The next line contains the date of diagnosis. It's your job to analyze the spread of the disease. At the first stage, information about the place and time of infection of all patients should be collected into a single file, so that the origin of the epidemic could be identified.   
Please think how many steps you need to copy the second and third lines from the file obtained for a single patient to one line of the summary file? How much time would it take for a very skilled person? How much time would such a person need to complete the entire task, working 8 hours a day?  
One solution to this task takes you to type a few lines of text in the terminal, and an average computer will complete the task for you in couple of seconds.  We will return to this task in Classes 5 and 6.  
&nbsp;  
  
## Linux - basics
**Linux** is a free operating system that, apart from graphical user environment (GUI), allows a very efficient work in the command line mode (terminal) using shell. **Shell** is the part of the operating system that is responsible for how the terminal looks and functions and how the system executes commands. The most commonly used type of shell is **bash** (Bourne again shell). Linux and Linux-like systems are ubiquitous in scientific computing, including computer clusters that are increasingly used in various areas of biology. The working knowledge of Linux command line is thus an important part of a biologist's toolbox.

So, in practical terms:
- **Terminal** is a window where you can enter commands to be executed by the computer - this can be your own computer or a remote machine you connect to and work on.
- **Shell** (in our case bash) is a program that executes commands.
- **Shell session** is the current state/environment in the shell/terminal, delimited by login/logout.  
  
**One of the most important goals of this course is to teach you to work in a terminal.**  
&nbsp;   
  
## How to open a terminal?
We assume that you work on a computer running Windows. If you are running Linux or MacOS, see below. Windows uses shell that is different from Linux shells, and we will not cover it during our course. Our first task will be to connect to a remote computer that runs Linux and start a terminal session which we will use for the rest of the class.  To do this, we will use the PuTTY program which you can download [here](https://www.putty.org/).

Please open PuTTY and:

- In the `Host Name (or IP address)` field, please enter:`149.156.165.148`
  This is the IP number of the `kontiki` server we'll use during the class.

- In the `Port` field, leave `22`. We also do not change the connection type (`SSH`).

- In the `Saved Sessions` field you can enter any name, this will be the name of your connection - please type the name `kontiki`.

- Then select `Translation` in the `Category` (left) and select `UTF-8` in the `Remote character set` field.

- Press `Open`, then you will be asked by the program to enter your username (e. g., user102 - **your username and password will be provided by the course instructor**) and your password.  **Remember! Uppercase letters are not the same as lowercase in Linux !!!** Please enter your username and password carefully. **Note:** When typing the password, no characters appear in the terminal window.

  You are now connected to the server and can work on it in the terminal. In the same way, you can connect to the server from any Windows computer connected to the Internet. PuTTY is free software.

If you have the Linux or MacOS operating system installed on your computer, you can open a terminal window like any other program. If you would like to connect to our server (to do your homework), use the ssh-client program. In the terminal enter:

`ssh 149.156.165.148 -l user102`  149.156.165.148 is the IP number our server and user102 is the user account name.

After pressing <kbd>Enter</kbd> you will be asked to enter your password.  
&nbsp;  
  
  
## Working in a Linux terminal 
After starting your shell session, you should see a **prompt**. It will look more or less like this:
```
user181@kontiki:/home/user181$
```   
It contains the user name, server name, current working directory, and an invitation to type a command. We are ready to get to work!  
&nbsp;  
  
#### Exercise 1
Please change your password. In the terminal, type the command:
  
`passwd` and press <kbd>Enter</kbd>
  
You will be guided through the steps of changing your password. Please enter your passwords carefully!  
  
**Remember!** Uppercase letters are not the same as lowercase in Linux ! The new password should be difficult to crack. Please make it at least 8 characters long, including a capital letter and a number.  

Remember or write down the new password! You will use it from now on.  
---   
&nbsp;  
  
#### The anatomy of a command
In the terminal, you type commands that have a specific syntax, e.g.:

`ls -l`

We check if we typed what we wanted (or correct the entered text - to navigate within the line use the arrows <kbd>→</kbd> <kbd>←</kbd>, a wrongly inserted letter can be removed with <kbd>Delete</kbd> or <kbd>Backspace</kbd> keys).
And then hit <kbd>Enter</kbd>  - only now is the command executed.
  
Let's break down the above command into its component parts:
- `ls`: what shell is supposed to do for us. This is the name of the program that performs an action in the shell. In the example, `ls` will show you the content of a directory.
- `-l`: how should the task be performed? In the example, the `-l` option tells `ls` to show not only the names of files and directories, but also some additional information about them (who owns them, what is their size, when were they last modified).
- We could add, as the third part of the command, the name of the directory, which content should be listed. As we did not do it, the content of the current working directory will be listed.

After pressing <kbd>Enter</kbd> , the required information will be displayed in the terminal.
&nbsp;  
  
  
## Getting around in the Linux environment: commands to get you started. 
  
> #### Copying and pasting in terminal
>
> Standard Windows <kbd>Ctrl</kbd> + <kbd> C</kbd> and <kbd>Ctrl</kbd>+<kbd>V</kbd> shortcuts for copying and pasting don't work in shell, because these combinations were assigned to different commands long ago before Windows was born. To copy text within terminal use<kbd>Ctrl</kbd>+<kbd>Shift</kbd> +<kbd>Ins</kbd> and to paste <kbd>Shift</kbd>+<kbd>Ins</kbd>.  You can mark text within terminal and use mouse right-click to insert it at the cursor position.  
&nbsp;  
  

#### Exercise 2
Please find your current working directory. Make three directories, and in one of them, a subdirectory.  
1. Type `pwd` and press <kbd>Enter</kbd>.  
This command, an abbreviation from *print working directory*, does just that!  
The absolute path to your working directory will be printed to the standard output, i.e., the terminal.  
  
2. Type `mkdir hiv genome scripts` and press <kbd>Enter</kbd>.  
The command `mkdir`, or an abbreviation from *make directory*, needs to be run with one or more parameters - the desired directory names. In this case, the command has resulted in the creation of three directories.

3. Type `ls -l` and press <kbd>Enter</kbd>.  
You can see that your home directory now contains three new directories - *hiv*, *genome*, *scripts*. Cool!  
  
3. Type `cd scripts` and press <kbd>Enter</kbd>.  
The command `cd`, or an abbreviation from *change directory*, needs to be run with a parameter, that is an instruction on what you want to change to! We will talk more about this in a moment. After executing `cd`, you can inspect the path in the prompt line, display again the current working directory (`pwd`) and list the directory contents (`ls -l`).  
  
4. Type `mkdir output_files` and press <kbd>Enter</kbd>.  
Within the parent directory *scripts*, you have created another directory. Our folder structure is getting complicated!  
---  
  
#### Now, let's inspect what we have created, and how to navigate!
> ### Files, directories (folders) and paths
> You can use both **absolute** and **relative** paths. Let's imagine we have the following directory system and we are currently in the `user102` directory:
>
> ```bash
>    
>    / (root) 
>    ├── data
>    └── home
>         ├── user101
>         ├── user102
>         │    ├── genome
>         │    ├── hiv
>         │    └── scripts
>         │          └── output_files
>         ├── user103
>         │   ...
>         │   ...
>         ├── user124
>         └── user125
> ```
>
> The absolute path to the `output_files` directory is then:
>
> `/home/user102/scripts/output_files`   
>
> Such a path always starts at the very top of the directory tree, with the so-called "root" symbolized by the `/` character.
> The relative path provides the path from your current directory:
>
> `scripts/output_files`
>
> Likewise, the absolute path to the result.txt file in the `output_files` directory is:
>
> `/home/user102/scripts/output_files/result.txt`
>
> The relative path is:
>
> `scripts/output_files/result.txt`
&nbsp;  
   
> The following shortcuts can be used in paths:
>
> `~` (tilde) is the home directory symbol (can be used instead of `/home/user102` here)
>
> `.` (period) is the symbol of the current directory
>
> `..` (two dots) is the parent directory symbol (one level up from the directory we are currently in).  
&nbsp;  
   

#### Exercise 3
1. Please list three different ways of changing your working directory from the `output_files` directory to the `scripts` directory. Use (1) absolute path; (2) relative path; (3) refer to your home directory.  
2. Now, list at least three ways of changing your working directory from the `scripts` directory to the `genome` directory.  
---  
&nbsp;  
  
## Getting around in the Linux environment: more commands, and how to use them!
  
> ### Commands, their options, and some caveats!
> **Important!** If something in the commands typed below is enclosed in `[]`, it means that it's not an obligatory part of the command syntax, but rather it's optional. Do not type parentheses in the terminal! For example, the command:
>
> `ls [options] [directory]`
> Means we can type in the terminal:
> 
> `ls`
> 
> Content of the current directory will then be displayed. Whereas the command:
>
> `ls -l`
> 
> will display content of the current directory in so-called long format. In turn, the command:
>
> `ls -l /home/user102/genome`
> 
> will display the contents of the genome directory, also in long format.  
&nbsp;  
  
> ### Spaces are important
> The command will not be understood by the shell if we enter a space where it shouldn't be (e. g., by typing `- l` instead of `-l` or `/ home / user102 / genome` instead of `/home/user102/genome`). Spaces, however, are necessary between the components of the command:
> 
> `ls -l /home/user102/genome` will work, while `ls-l/home/user102/genome` will throw an error
>
> **Error messages**
> Usually, an incorrectly typed command only results in a message that shell didn't understand and didn't carry out the command. If you accidentally type a command that causes the terminal to hang (no prompt, can't type anything), press <kbd>Ctrl</kbd> and <kbd>C</kbd> at the same time - this should terminate the  process. Remember this shortcut, you'll use it many times during the course!  
&nbsp;  
  
> ### Useful commands and utilities Part 1
> `pwd` </br> 
> (print working directory) - displays path to the current directory, starting with root
>
> `cd [directory]`
> (change directory) - go to the directory. cd without target directory gets the user to its home directory, in the case of user102 this will be `/home/user102` 
>
> `mkdir [options] directory`
> (make directory) Create a new directory named `directory`. By using the `-p` option, we can create the given directory and parent directories (if they do not already exist) with one command.
>
> `rmdir [options] directory`
> (remove directory) Removes an empty directory named `directory`.
>
> `touch [options] filename`
> Creates an empty file named `filename`.
>
> `mv [options] filename directory`
> `mv [options] file1 file2`
> (move) Moves the file named `filename` to the directory named `directory`. The command is also used to rename a file (`file1` → `file2`)
>
> `cp [options] filename directory`
> `cp -r directory1 directory2`
> (copy). Copies the file named `filename` to a directory named `directory`.
> The command with the `-r` option copies `directory1` and its content to directory named `directory2`.
>
> `rm [options] filename`</br>
> `rm -r directory`
> (remove) Removes a directory with the given name.
> `rm` with the `-r` option removes the directory and its content. **Warning!** Please be careful when deleting files and full directories. The `rm` command does not move them to the trash. Files and directories are permanently removed from the disk! 
> 
> `wc [options] filename`
> (word count) Returns the number of lines, words and characters contained in the file. The `-l` option gives only the number of lines, `-w` only the number of words, `-c` only the number of characters.
>
> `man [options] command`
> (manual) Opens the manual for the command. Man displays comprehensive documentation of the command/program, which may be quite technical. To get more limited, but often more accessible help, many programs support `--help` or `-h` option. Or use Google :)
>
> `passwd`
> (password) Allows the user to change his password, as we already did.
>
> `exit`
> Ends the session and closes the terminal.  
&nbsp;    
  
> ### Wildcards
> Often, you will want to execute the same command on several files or folders. You can do this using **wildcards**
> 
> `?` indicates any character, but only one, in the folder or file name.
> `ls file?.txt` will list *file1.txt* and *file2.txt*, but not *file10.txt*
>
> `*` indicates a series of characters of any length.
> `rm file*` will remove any files the name of which starts with *file*!
  
  
#### Exercise 4
1. Within the `scripts` directory create three empty files, *file1.txt* *file2.txt* *file3.txt*.
2. Move the newly created files to the `output_files` directory, and rename *file3.txt* to *results.txt*
3. Copy *results.txt* to the directory `genome` and save it under the new name, *genome_results.txt*
4. Copy the whole folder `output_files`, with all files, to the directory `genome`
5. From `output_files` in `scripts` directory, remove all files with *file* in their name.
6. Change your working directory to home directory, and from there, remove the *genome_results.txt* file that you had placed in the `genome` directory.
7. While within home directory, remove all files from the `genome/output_files/`, and then that directory itself.
---  

  
## Making your life easier, and working with real files!
  
> ### History
> Typing commands can be tiresome, but you can reuse the commands you typed previously. The commands that were typed in the terminal are remembered as **History**. To recall them, you can use the <kbd>↑</kbd> <kbd>↓</kbd> arrows, and then change only part of the command (arrows <kbd>→</kbd> <kbd>←</kbd>, <kbd>Backspace</kbd>, <kbd>Delete</kbd> keys). 
> Also, you can use the command `history` to list commands executed recently! 
> When reusing old commands, it is helpful to use shortcuts Ctrl+A, Ctrl+E - jumping to the beginning/end of the edited command.  
&nbsp;  
  
> ### Autocompletion
> Folder and file names are often long and difficult to type. Please check what happens when you enter just the first few letters of its name and press the <kbd>Tab</kbd> key. This is called the Tab completion or autocompletion feature. Use it as often as possible to do less typing and avoid typos. After completing the file name, you can go to the end of the line and finish typing the command (you can also continue to use Tab completion).  


 
#### Exercise 5 
Please display content of directory `/dane`. How do files and directories look like?   

---  
 

#### Exercise 6
Use autocompletion to copy the file `GCF_000001405.33 ...` from the directory `/dane` to
the `genome` directory you created. This is a file containing information about the human genome assembly.
We will use it as an example of a text file later on   

---
  
#### Exercise 7   
Please view the manual pages for the `ls` command. Which `ls` option will show all files,
including hidden files (hidden filenames start with a period on Linux)?</br>
When inside the manual, you can search its contents by typing:

`/phrase`</br>
and then pressing the <kbd>Enter</kbd> key. Pressing the <kbd>n</kbd> key will allow you to go to the place 
of the next occurrence of the searched phrase in the manual.

Search the manual for `size` and answer the question: 
Which `ls` command option should you use to list files and directories sorted by size?

To exit the manual, press <kbd>q</kbd>.

---

[Return to the top](#why-is-it-worth-learning-to-work-with-the-command-line)


# Automation with shell scripts
  * [Automation...](#automation)
  * [if conditional](#if-conditional)
      * [Exercise 1](#exercise-1)
      * [Exercise 2](#exercise-2)
  * [Loops: while until and for](#loops-while-until-and-for)
    * [Two similar loops: while and until](#two-similar-loops-while-and-until)
      * [Exercise 3](#exercise-3)
    * [for loop](#for-loop)
      * [Exercise 4](#exercise-4)
      * [Exercise 5](#exercise-5)
  * [Running jobs in the background with screen](#running-jobs-in-the-background-with-screen)
  * [Where to go next?](#where-to-go-next)

***

## Automation...  
is needed when you want to do some task on the large number of objects (files, directories, lines).  
During this class you will analyze data from more than 20,000 small text files using shell scripts. 
To make this task possible you need to add to your scripts two types of constructs:  loops and conditionals.   

**A loop** is a powerful programming tool that enables you to execute a set of commands repeatedly.  
**A conditional statement** enables you to control the flow of commands. In other words, you can use them to 
create branches and execute different commands on objects fulfilling (or not) some condition.  

***  

## `if` conditional

The `if` statement is used to construct commands that will be executed only if some conditions are fulfilled. The general syntax is:

``` bash
if [ condition ]	# Condition has to be enclosed in square braces [] and separated from braces with spaces 
then
	command1		#The commands will be executed only if the condition is TRUE
	command2
	...
fi
```

A bit more complex case:

``` bash
if [ condition1 ]
then
	command1		#commands 1 and 2 will be executed only if condition1 is fulfilled (TRUE)
	command2
elif [ condition2 ]
then
	command3		#command 3 will be executed if condition2 is TRUE (and condition1 is FALSE)
else
	command4		#command 4 will be executed if conditions 1 and 2 are FALSE
fi
	
```

> #### Conditions
>
> Conditions for text strings
>
> |    Condition     |            Meaning             | Example (condition is TRUE) |
> | :--------------: | :----------------------------: | :-------------------------: |
> |    `-n TEXT`     |     text string length > 0     |         `[ -n cat ]`        |
> |    `-z TEXT`     |  text string length equals 0   |          `[ -z ]`           |
> | `TEXT1 = TEXT2`  | two text strings are identical |      ` [ cat = cat ] `      |
> | `TEXT1 != TEXT2` | two text strings are different |       `[ Cat != cat ]`      |
>
> Conditions for integers
>
> |       Condition       |        Meaning        | Example (condition is TRUE) |
> | :-------------------: | :-------------------: | :-------------------------: |
> | `NUMBER1 -eq NUMBER2` | numbers are identical |       `[ 10 -eq 10 ]`       |
> | `NUMBER1 -gt NUMBER2` |  `NUMBER1 > NUMBER2`  |       `[ 10 -gt 5 ]`        |
> | `NUMBER1 -lt NUMBER2` |  `NUMBER1 < NUMBER2`  |       `[ 5 -lt 10 ]`        |
>
> Conditions for files
>
> |     Condition      |                       Meaning                        |
> | :----------------: | :--------------------------------------------------: |
> |     `-d FILE`      |            file exists and is a directory            |
> |     `-e FILE`      |                     file exists                      |
> |     `-s FILE`      |             file exists and is not empty             |
> | `-r (-w, -x) FILE` | file exists and has read (write, execute) permission |
>
> Condition can also take a form of equation, which is then enclosed in double braces:
>
> ``` bash
> if (( 10 % 2 == 0 ))		#if remainder from dividing 10 by 2 is 0, then..
> then ...				
> ```
>
> Note the double equals sign (`==`) in the above.
>
> **Combining conditions**
>
> If two conditions are to be met simultaneously we join them with `&&`:
>
> ``` bash
> if [ condition1 ] && [ condition2 ]
> then...
> ```
>
> If at least one of the conditions is to be met, we join them with `||`
>
> ``` bash
> if [ condition1 ] || [ condition2 ]
> then...
> ```

#### Exercise 1

All exercises in this class will use files in directory `/data/epidemy`. Copy this directory and its entire content into your home directory (`cp -r` ). The directory contains 20,112 text files. Each of these files describes a single case of hemorrhagic fever in Poland from summer 2021 (therefore file names start with `pacjent`, which is `patient` in Polish). All files have the following format (below file for patient1 is shown):

``` 
nr 1
Rzeszów
19.07.2021
comment
```

Line 1: patient number (id) - the same as in the file name

Line 2: town where the case was diagnosed

Line 3: date when the case was diagnosed

Line 4: comment - this line can be missing, can be present but empty, or can contain information about complications

Write script `epidemy1.sh`. This script should take as command line arguments ids (numbers) of two patients. If both were diagnosed the same day, then the script should print in terminal : `Diagnosed on the same day`. If the dates were different the script should print: `Diagnosed on different days`. Please test the script on patients 10015 and 1196 (the same date) and 10113 and 1595 (different dates).

**Tips (you don't have to use them, there's several ways of writing this script)**

1. Define variable with the name of the file for the first patient
2. Define variable with the name of the file for the second patient
3. Define two variables which will contain the third line of each file (use `sed -n` or `head` and `tail`)
4. Write `if` statement that will compare the values of the third lines assigned to the variables from p. 3 and, based on the result of this comparison, print the appropriate message.

---

> #### Testing condition in terminal
>
> Before entering a condition into your script, you can test it in terminal using `test`command.
>
> Condition in script: `[ 001 = 1 ]`
>
> Test in terminal: `test 001 = 1`
>
> `echo $?` will print the exit status of the last command: `0` for TRUE, `1` for FALSE.
>
> Is the above condition TRUE? Please check quickly in terminal.

#### Exercise 2

Doctors suspect that as the epidemy progressed, the symptoms were becoming milder. Write script `epidemy2.sh`, which takes patient number as command line argument and checks whether this patient experienced serious complications or died (nonempty comment line) and whether the patient was diagnosed at the early stage of epidemy (June). If both conditions are fulfilled the script should print `A serious case diagnosed in June 2021`, otherwise print `exiting...`

**Tips:**

1. Regular expression pattern for an empty line is `^$`
2. To get the month you can use `cut` with an appropriate column delimiter.

Please test your script on patients 9633 (conditions fulfilled) and 1 (conditions not fulfilled)

---

## Loops: `while` `until` and `for`

Loops execute a list of commands multiple times and are thus crucial for automation. In principle loops can run forever (and sometimes do, if they are incorrectly written), therefore we need to specify conditions for a loop to finish. The three types of loops we'll cover:

* `while` runs  as long as conditions are met

* `until` runs until conditions are met

* `for` runs for each item from a list of items
### Two similar loops: `while` and `until`

Let's write script `while_loop.sh`:

``` bash
#!/bin/bash
n=1									#define variable n, which counts the number of iterations
while [ $n -lt 11 ]					#define condition: loop will run as long as n < 11
do									#'do' starts the loop; three next lines contain commands to execute
	echo $n							#print current value of n
	echo passes through the loop	#print message, the same in each iteration
	(( n++ ))						#increase the value of n by 1
done								#'done' ends the loop
```

Conditions in loops are defined in the same way as in `if` statements. Please note variable `n` which counts the number of passes through the loop, and is called, surprisingly, **counter**. Counter is a general concept, common for most programming languages. Counter has to be **defined before loop**! - of course you can give it any name. Within the loop you have to **modify its value** `(( n++))`! What would happen if you din't modify the counter value?

You can increase counter in steps different from 1, using expression `(( n+=3 ))`. If instead of `+` you use `-` counter will decrease by 3 with each pass through the loop. 

Let's now write script `until_loop.sh`

``` bash
#!/bin/bash
n=1									#define variable n, which counts the number of iterations
until [ $n -gt 10 ]					#define condition: loop will run until n > 10
do									#'do' starts the loop; three next lines contain commands to execute
	echo $n							#print current value of n
	echo passes through the loop	#print message, the same in each iteration
	(( n++ ))						#increase the value of n by 1
done								#'done' ends the loop
```

Do scripts `while_loop.sh` and `until_loop.sh` produce identical results? How many times the message `passes through the loop` appears in terminal? Make sure that you understand the syntax of both scripts.

#### Exercise 3

Please modify the scripts:

* `while_loop.sh` so that it prints only even numbers in the range 2-10.
* `until_loop.sh` so that in prints numbers from 1 to 10 in **descending** order.

---

### `for` loop

In the `for` loop we define iterator, often named `i` that in consecutive passes through the loop takes the value of consecutive elements from the list of values:

``` bash
for i in Alice Alex John	#define list, its items (Alice, Alex, John) are separated with spaces
do							#'do' starts the loop
	echo $i has a cat		#the next line contains command to do: print the message
done						#'done' ends the loop
```

The list can be the result of a command. For example, you can use `ls` to get a list of file names:

``` bash
for f in $( ls *.tab )		#define list of files: all files with extension '.tab' in current directory
do
	echo $f					#print file name
	sort $f > s_"$f"		#sort file, save the result to a new file (what will be its name?)
done
```

The list can be a sequence of integers:

``` bash
for n in {5..13}			#define list of integers 5-13
do
	n1=$(( $n % 2 ))		#define new variable n1, it's value is the remainder from dividing n by 2
	echo $n1				#print n1
done
```

#### Exercise 4

Modify script `epidemy2.sh` so that it saves in file `June_difficult_cases.txt` names of all files that contain difficult cases (complications or death) diagnosed in June2021. Save the modified script as `epidemy3.sh`. How many files were there. **Tip**: it's a good idea to test the script on a portion of data (e. g., files `pacjent11*.txt`) as searching through all 20,112 files will take a while.

---

#### Exercise 5

Write script `epidemy4.sh` which will, from all text files in the directory `epidemy`, cut lines 2 and 3 (place and date of diagnosis) and will write them is a single line of the file `diagnosis.txt` in your home directory. The file `diagnosis.txt` should have two columns delimited with `tab`.

---

> #### Reading file line by line
>
> `read` command can be used to read file content line by line. To do that use a `while` loop:
>
> ``` bash
> while read i
> do
> 	echo $i | cut -f 1 -d ''
> done<text_file.txt
> ```
>
> The code above opens file `text_file.txt`, reads it line by line, cuts from each line the first column and prints it in terminal. The loop terminates while it reaches an empty line.

## Running jobs in the background with `screen`

So far our scripts were fast and we did not have to wait more than a few seconds for the to finish. In may real-life applications you have to process large files or perform time-consuming calculations. In such situations it's useful to be able to disconnect from a remote computer while leaving your script/program running in the background. For this you can use `screen`.

> #### Using `screen`
>
> `screen -S terminal_name` will open a virtual terminal session. You can now work in the same way as in a normal terminal. The difference is that you can run a command/script/program and leave the virtual terminal without interrupting the tasks running. In other words, after you disconnect from the remote computer your processes will continue. To disconnect, press the <kbd>Ctrl</kbd> and <kbd>a</kbd> keys simultaneously, and then still pressing <kbd>Ctrl</kbd> press <kbd>d</kbd>. After leaving the virtual terminal, you can also close the "normal" terminal (`exit`) and switch off your computer.
>
> To return to any of the virtual terminals of the screen program, enter the command:
>
> `screen -r terminal_name`
>
> To see the names of all created virtual terminals, enter:
>
> `screen -ls` or `screen -r`
>
> To get rid of any of the virtual terminals (when it commands issued in it have been executed), enter it, and then type the `exit` as in a "normal" terminal.

## Where to go next?

This completes our tour of Linux command line. We hope that now you're convinced that working in command line makes sense. To get a more thorough understanding of the command line, we highly recommend this [free book](http://linuxcommand.org/).

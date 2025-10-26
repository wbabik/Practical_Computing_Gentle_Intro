# Class 4

# Working in Linux shell I
  * [Wildcards and operations on many files](#wildcards-and-operations-on-many-files)
      * [Exercise 1](#exercise-1)
  * [Editing text files with nano](#editing-text-files-with-nano)
      * [Basic navigation and saving in Nano](#basic-navigation-and-saving-in-nano)
  * [Downloading files from the Internet](#downloading-files-from-the-internet)
  * [Standard input, output, redirection and pipe](#standard-input-output-redirection-and-pipe)
    * [Redirection](#redirection)
  * [Looking inside text files with cat, head, tail and less](#looking-inside-text-files-with-cat-head-tail-and-less)
  * [Searching for patterns with grep](#searching-for-patterns-with-grep)
      * [Exercise 2](#exercise-2)
  * [Extracting information from structured text files with cut, sort and uniq](#extracting-information-from-structured-text-files-with-cut-sort-and-uniq)
      * [Exercise 3](#exercise-3)
  * [Merging files with cat](#merging-files-with-cat)
      * [Exercise 4](#exercise-4)

***


## Wildcards and operations on many files

Linux provides an easy way to process at once a large number of files. For this purpose, you can use wildcards. These are characters with a special meaning that allow the user to refer to the entire set of files or directories on a single command . 

> ### The most commonly used wildcards
>
> `*` nothing or any character(s), their number is unlimited
>
> `?` any single character
>
> `[]` a set, or range of characters, e. g., `gr[ae]y` matches `gray` or `grey`, `[a-z]` matches all lowercase letters
>
> ### Examples
>
> `cp * /home/student02` will copy all files/directories from the current directory to the home directory of `student02` 
>
> `rm *.jpg` will remove all files with the extension `.jpg` from the current directory
>
> `mv A* directory1` will move all files starting with `A` to `directory1`
>
> `ls A???` will show all files/directories whose names are only 4 characters long and start with `A`

The principle of wildcard characters is quite similar to that of regular expressions. However, wildcards are used to search for a pattern in file and directory names, not inside text files. They are interpreted directly by the shell (and not by any particular program), therefore the meaning of the characters is slightly different than in regular expressions! Wildcards can be used in most programs that operate on files and directories  (`ls`, `cp`, `mv`, `rm` etc.)

> ### FASTA format
>
> One of the simplest and widely used formats for storing sequences of nucleic acid and protein sequences is FASTA, often saved in files with extensions `.fa`, `.fas` or `.fasta` . These are plain text files, each sequence has a title line starting with `>`, which can contain any description you want, and in next line or lines is the actual sequence. Sequences are separated by lines staring with `>` and each sequence can be written in a single or multiple lines:
>
> ```
> >seq1
> ACTGATAGTAGATTAGGATTGAGTTGACCCATCAACTCATAGATCGTACGCAGTCAGCTCAGACGAGACGACGACAGCAGACGAAGAATAGCAGACGACGACAGCAGCAGACGACAGAAGATAGATGGCAGAGAAGATGAAGAG
> >SEQ2 with a long title name containing # special % characters
> ACTGATAATGTATGATATGAGTA
> >seq3 written in multiple short lines
> ACTG
> ATGACTAGTA
> ACTAGG
> ```
>
> An easy way to count the number of sequences in FASTA file is to count the number of lines starting with `>`

#### Exercise 1

During today's class we will use genomic sequences of various lentiviruses (HIV and SIV) isolated from several hosts (designations of hosts are in file `/dane/hiv/hiv_gatunki.txt`). Virus sequences are in `/dane/hiv`.  

Sequences of viruses in `/dane/hiv` are in separate files, each of them with extension `.fasta`.
Do all files in the directory have extension `.fasta`? 
Please copy from `/dane/hiv` to the `~/hiv` directory only files containing sequences, i. e. with extension `.fasta`. 

---

## Editing text files with nano

Nano is an easy-to-use, versatile and simple text editor installed by default in Ubuntu and many other Linux distributions. In many cases, using nano is the most straightforward way of making quick edits to your system files and scripts.

`nano` or `nano FILENAME` starts the editor and creates a new file - although the second command can also be used to open an existing file. You will see a screen which looks like this    

<img width="1422" alt="Nano_screen" src="https://user-images.githubusercontent.com/12505600/119043659-8ff1aa00-b9b9-11eb-88e5-19efd3944bf8.png">

The main window contains the cursor and the text, which you can edit in a standard way.  
At the bottom of the editor window, there is useful information on keyboard shortcuts that let users perform some basic operations such as cut and paste text, exit the editor and launch help. Basically, you execute them using <kbd>Ctrl</kbd> + <kbd>LETTER</kbd>.  

For example, `^G`, or `Ctrl + g`, opens help.

#### Basic navigation and saving in Nano


`^A`, or `Ctrl + a` moves the cursor to the beginning of line in nano.  

`^E`, or `Ctrl + e` moves the cursor to the end of line in nano.  

`^Y`, or `Ctrl + y` moves down a page - to the next page in nano.  

`^V`, or `Ctrl + v` moves up a page - to the previous page in nano.  

`^_`, or `Ctrl + _` moves you to the specific line. You will be prompted to provide line number, confirm with Enter.

`^O`, or `Ctrl + o` allows you to save the file. Upon pressing this key combination, you will be prompted to type the file name, and/or confirm that you want to change the name. You will be given options such as selecting encoding, that you will be able to apply using `Alt + LETTER`, for example `Alt + M`.

<img width="1422" alt="Saving" src="https://user-images.githubusercontent.com/12505600/119045975-6d14c500-b9bc-11eb-8c7d-b5414a960bd8.png">

`^X`, or `Ctrl + x` closes Nano. You will be asked whether to save changes before exiting.

`^K`, or `Ctrl + k`, allows you to cut entire lines of text. Then, you can head to the line where you want to paste them, and apply `^U`, or `Ctrl + u`.   

You can also copy a particular string instead of full line. For this, first you will have to select that word/string by pressing `Ctrl + 6`, or `Alt + A` with the cursor at the beginning of the selection, and then moving to the end of selection. Now you can press `Ctrl + k` to cut and `Ctrl + u` to paste the word at your desired destination.  

`Ctrl + w` can be used to search for a specific term. You will be asked to enter the word which you want to search. Then, hit Enter and the tool will take you to the matched entry.  

`Ctrl + \` allows you to replace a word with another. Nano will ask you for the word which you want replaced, and then for the word you want it replaced with. After this, it will ask you to confirm the changes, and whether they should be applied to specific instances, or globally.  

All together, Nano is not the most intuitive and easy-to-use editor. But it is immediately available on almost any machine running Linux , has multiple additional options, and with a little practise, can greatly speed up your work. Learning it is definitely worth your effort!  

&nbsp;  


## Downloading files from the Internet

When working in terminal, you can easily download files from the Internet using `wget`. The basic usage is just:

`wget URL` where URL is the web address of the file you want to download.

For example, to download the README file explaining a part of NCBI genomic resources called RefSeq type:

`wget https://ftp.ncbi.nih.gov/genomes/refseq/README.txt`

`wget` is an advanced tool, allowing you to download files over unstable internet connections, recursive download of entire web pages and repositories and downloading in the background, when you are disconnected from the server. Consult the manual for additional information.

## Standard input, output, redirection and pipe

Each program that you run in the terminal takes input data, analyses it and returns its result and possibly an error message. To put it in other words, each program has three **data streams**. These streams have their names and numbers:

![stdin](Stdinout.png)

- STDIN (standard input) is the input provided by the user with keyboard or by another program
- STDOUT (standard output) is the result of the program operation, by default displayed in the terminal window. 
- STDERR (standard error) is a message about possible errors, it's also by default displayed in the terminal

### Redirection

Data streams can be redirected to files (effectively: saved to files) or to other programs. This technique is commonly used and extremely powerful, as it allows to combine several tools, each performing a simple task, into **pipelines**, together performing complex tasks

> #### Redirection examples
>
> `ls > list.txt` will write a list of files/directories in the current directory (i. e., the output from `ls` program) to the file `list.txt`. In which directory will this file be created? Why? Which path we used here?. **Caution!** If file `list.txt` already exists, its content will be overwritten.
>
> `ls >> list.txt` works similar to the previous command. The difference is that if `list.txt` already exists, using `>>` will **append** new data to the end of the file. 
>
> `ls 2> error.txt` will write any error message produced by `ls` to file `error.txt`
>
> `ls | less`  pipe symbol `|`  will send the output  of `ls` program, i. e.,  the list of files/directories in the current directory , to `less` program.  What will happen then? Why would you like to do something like this? In this way we constructed our first pipeline! More on pipe and pipelines later.

## Looking inside text files with `cat`, `head`, `tail` and `less`

Basically each computer running Linux has several tools to work with text files. These tools allow you to work with text files of unlimited size, which is not the case with standard office applications. Even opening a modest 100 MB text file in MS Word or MS Excel is slow and often causes the programs to crash. The Linux text viewing tools are very fast and provide many functionalities.

> #### Basic text viewing tools
>
> `cat` (concatenate) displays the content of the file (or multiple files) in the terminal. This basic function is quite versatile, and we'll see the use of `cat` in several contexts during this course.  
> What happens if you use `cat` to display the content of `README.txt` file you downloaded earlier? To see type: `cat README.txt`
> A useful option of `cat` command is `-T`, which displays `tab` in terminal as `^I` . With this option you can easily check whether the file is `tab`-delimited.
>
> `head` often we just want to have a quick look at the content of the file, and we can learn what we want from a few first lines. `head` is just for that - it displays by default 10  lines starting from the **beginning** of the file n the terminal. The number of lines to display can be changed using `-[number]` or `-n [number]`. 
> Display first 12 lines of `README.txt`
>
> `tail` as above, but displays lines from the **end** of the file. Sometimes we want to display the entire content of a file, skipping just first line, this can be done using `tail -n +2 [FILE]`, the command instructs `tail ` to start from the line number 2.
>
> `less` displays the content of a file in portions that fit the screen; you can move to another screen using <kbd>Space</kbd> or <kbd>PgDn</kbd>.  `less` allows also searching the content of a file by preceding the phrase to find with `/` and pressing <kbd>Enter</kbd>; pressing <kbd>n</kbd> finds another occurrence of the phrase.  You can quit `less` by pressing <kbd>q</kbd>. 

## Searching for patterns with `grep`

`grep` is the Linux utility that made regular expressions popular. `grep` searches for patterns in text files and displays lines containing the pattern. 

> #### Useful `grep` options
>
> The basic syntax of`grep` is as follows:
>
> `grep [OPTIONS] 'pattern'[FILE]`
>
> Below several useful options:
>
> `-n` displays also line numbers where the pattern occurred
>
> `-c` instead of displaying the lines where the pattern occurred, counts the lines and displays the count
>
> `-v` inverts the search, i. e., displays only lines that did not contain the pattern
>
> `-E` **extended** grep. `grep` by default supports only basic regular expressions. Using `grep` with `-E` options gives access to the full set of regular expressions. Also, syntax is then a bit simpler, for example to search for alternative, with basic syntax you have to use `\|`, while with `-E` it's enough to type `|`.  It's a good idea to use `grep -E` by default.
>  
> `-P` use Perl dialect of regular expressions.  It's useful because it allows to search for `tab` characters, which are, unfortunately not implemented in basic and extended grep. With `-P` you can search for `tab` using `\t`.
>  
> `-A number` displays the line with the pattern AND the requested number of subsequent lines (**after** the line containing the pattern). For example, you may want to search a `.fasta` file and output both the headings containing your search pattern, and the lines immediately after containing the sequences.  
>   
> `-B number` displays the line with the pattern AND the requested number of preceding lines (**before** the line containing the pattern).

> #### `grep` patterns
>
> There are two basic forms of patterns for `grep`:
>
> 1. Plain text, e. g., 'new' - `grep` will print lines containing **new**, **new**t or sto**new**ork. Plain text pattern can contain whitespaces: 'This is a valid pattern to search' 
> 2. Regular expressions as explained in Class 2.

#### Exercise 2

File ["Army_ant_COI_sequences.fasta"](https://www.dropbox.com/s/4ev6hq66yf3jgaj/Army_ant_COI_sequences.fasta?) contains barcode sequences of many specimens of several species of army ants, downloaded from Genbank. In each case, the sequence name contains genus, species, and isolate number. Use `wget` and the obove link to download the file to your home directory.
```
>KX983244.1 Eciton burchellii isolate 6 cytochrome oxidase subunit I (COI) gene, partial cds; mitochondrial
ATACTATACTTTATTTTTTCATTCTGAGCAGGAATATTAGGATCCTCAATAAGTATAATTATTCGCTTAGAACTAGGAACATGTGGGTCCCTTCTTAATAACGACGCT....
>KX983245.1 Cheliomyrmex sp. 1 PL-2016 isolate Che1 cytochrome oxidase subunit I (COI) gene, partial cds; mitochondrial
ATACTTTATTTTATCTTTTCTTTTTGAGCCGGAATATTAGGTTCATCAATAAGAATAATTATTCGACTAGAATTAGGAACTTGTGGATCATTAATTAATAATGACCAA....
```
* Display the heading lines. Now, count them. How many sequences are there in the file?

* How many sequences of *Eciton* are there?

* How many sequences of *Eciton* species other than *burchellii* are there? **Hint**: you can pipe `|` the output of a `grep` search to another `grep` search!

* 2.4. Display all sequences (headings + sequences) of *Labidus praedator*. Then, send them to a new file called **Labidus_praedator.fasta** (the file should be located in your home directory).

* 2.5. Display, and then export to a new file, all sequences (headings + sequences) where the nucleotide sequence matches a potential diagnostic primer `ACCTGTGGTTCATTACTC`, supposed to match only a single species. Which species that is? Export the output to a new file called **Primers.fasta** (the file should be located in your home directory).

* 2.6. We want to test another potential diagnostic primer for one of the species, `GGAAACTTYCTTGTACCA`. Note that it contains a degenerate position, `Y`, which according to the [IUPAC nucleotide code](https://www.bioinformatics.org/sms/iupac.html) represents either `T` or `C`. How many sequences does this primer match? Which species they belong to? How does the number of sequences matching the primer compare to the total number of sequences of that species?
---

## Extracting information from structured text files with `cut`, `sort` and `uniq`

As we saw in Class 2, text files are often structured into columns. Similarly, file names often consist of several fields containing information about various aspects of file content. Such columns/fields can be easily cut, sorted and unique items can be extracted using `cut`, `sort` and `uniq`. These three commands are often used together, with information passed between them with pipe `|`.

> #### Syntax
>
> `cut [OPTIONS] [FILE]`  cuts fragments from a text file. 
> `-c n1-n2` cuts from each line in the file characters from n1 to n2, counting from the beginning of the line
> `-f columns`  cuts particular columns from the file; if multiple columns are specified, they should either be separated by `,` or, if you want a range of consecutive columns, by `-`.  For example:  `cut -f 2` extracts the second column, `cut -f 2,4,6` extracts columns two, four and six, and `cut -f 2-5` extracts columns from two to five.
> By default, `cut` assumes that columns are separated by `tab`, but any delimiter can be used, by setting it with option `-d 'sep'`. For example to use underscore (`_`) as separator and extract columns from two to five you type `cut -f 2-5 -d '_'`.
>
> `sort [OPTIONS] [FILE]` sorts lines of a text file alphabetically (by default)
> `-n` allows sorting numerically
> `-k column,column` allows sorting according to a given column. By default columns are assumed to be separated by `tab`. If you want to sort by a particular column, remember to use its number twice, e. g., `sort -k 2,2`, if you use just `sort -k 2` sorting will be done according to the all columns starting from 2 concatenated together. You can easily sort by multiple columns, e. g., to sort numerically by column 3 and then by column 5 use `sort -n -k 3,3 -k 5,5.`
> `-t` sets the field/column separator, e. g., `-t  '_'` will use underscore as field separator.
>
> `uniq` outputs only **unique** lines if identical lines are adjacent, i. e., if the files was **sorted** first. `uniq` is used to filter out duplicates. Similar effect can be obtained with using `sort -c`, but using `unique` is more explicit and thus recommended.

> #### Example
>
> Let's use `wget` to download a file from the Internet to the home directory:
>
> `wget https://www.dropbox.com/s/foigp257imlrejc/Exons.bed` 
>
> **Remember!** To paste text in PuTTY terminal use <kbd>Shift</kbd> + <kbd>Ins</kbd>
>
> Now, let's have a look at the file content:
>
> `head Exons.bed`
>
> the beginning of the file is:
>
> ```PSMB8a_c112196_g1_i1    51      229     5end_incomplete
> PSMB8a_c112196_g1_i1    229     374     complete
> PSMB8a_c112196_g1_i1    374     486     complete
> PSMB8a_c112196_g1_i1    486     616     complete
> PSMB8a_c112196_g1_i1    616     821     complete
> PSMB8a_c112196_g1_i1    821     955     3end_incomplete
> PSMB9a_c109577_g1_i1    168     240     3end_incomplete
> PSMB9a_c109577_g1_i1    240     308     complete
> PSMB9a_c109577_g1_i1    308     440     complete
> PSMB9a_c109577_g1_i1    440     570     complete
> ```
>
> We see that the file contains four columns:
>
> - gene name
> - start 
> - stop
> - feature name
>
> We want to have a list of all gene names, and a list of all feature names, both including only unique names.
>
> To get the gene names we'll first `cut` the first column, then we'll `sort` this column, and then we'll use `uniq` to remove duplicates. The entire task will be done in a single line, using pipe `|` to use output from one program as input for another:
>
> `cut -f 1 Exons.bed | sort | uniq`
>
> produces the following output:
>
> ```AGPAT1_c248472_g1_i1_cds
> BRD2_c757_g1_i1_cds
> DAXX_c114877_g1_i1_cds
> KIFC1_c139688_g1_i1_cds
> PBX2_c2881_g1_i1_cds
> PSMB8a_c112196_g1_i1
> PSMB9a_c109577_g1_i1
> RGL2_c153162_g1_i1_cds
> RNF5_c3067_g1_i1_cds
> RXRBA_c149444_g1_i1_cds
> TAP1_c2675_g1_i1
> TAP2_c150845_g1_i1
> TAPBP_c134883_g1_i1
> ```
>
> Now, use a similar technique to get the list of feature names.

#### Exercise 3

Download file `Ex_02_2.txt` from the Internet using `wget` and the link: `https://www.dropbox.com/s/gruaw8vqgnwas8l/Ex_02_2.txt`. We used this file already in Class 2. 

* How many lines are in the file?

* Display the first few lines of the file with `head`. Is the output easy to read? Why? 

* Use `cat` to verify whether the file is `tab` delimited text.

* Use `cut ` together with head (and `|`) to display the first 5 columns and 30 lines. You should get something like this:
  ```
   ID      info    a0001   a0002   a0003
  3038    Visui_R_vul_1   0       0       0
  3039    Visui_R_vul_1   1       0       0
  3040    Visui_R_vul_1   1       0       0
  3041    Visui_R_vul_1   0       1       1
  3042    Visui_R_vul_1   0       1       1
  3043    Visui_R_vul_1   0       0       1
  3044    Visui_R_vul_1   1       1       0
  3045    Visui_R_vul_1   0       0       1
  3046    Visui_R_vul_1   0       0       0
  3047    Visui_R_vul_1   0       0       0
  3048    Visui_R_vul_1   0       1       0
  3049    Visui_R_vul_1   1       1       0
  3050    Visui_R_vul_1   0       1       1
  3051    Visui_R_vul_1   1       0       1
  7319    Solo2_R_vul_2   1       1       0
  7320    Solo2_R_vul_2   0       1       0
  7321    Solo2_R_vul_2   0       0       0
  7322    Solo2_R_vul_2   0       0       1
  7323    Solo2_R_vul_2   1       0       0
  7238    Solo1_R_vul_3   1       0       0
  7239    Solo1_R_vul_3   1       0       0
  7240    Solo1_R_vul_3   1       0       0
  7241    Solo1_R_vul_3   0       0       1
  7242    Solo1_R_vul_3   1       1       0
  7243    Solo1_R_vul_3   1       1       0
  7324    Paul1_R_vul_4   1       0       0
  7325    Paul1_R_vul_4   0       0       0
  7326    Paul1_R_vul_4   0       0       0
  7327    Paul1_R_vul_4   1       1       0
  ```

* The second column contains several fields delimited with underscore (`_`). Its first field contains population acronym (`Visui`, `Solo2` etc.).  Using  `tail`, `cut`, `sort`, `uniq` and `|` print the list of unique population acronyms. Then modify the command to save the list to the file `Population_acronyms.txt`. **Tip1**:  `tail` can be used to skip the first line, which is of no interest for you. **Tip2:** you can pipe output from `cut` to `cut` to divide a single column into multiple columns using a different delimiter.

---

## Merging files with `cat` 

`cat` concatenates all files provided as arguments and by default prints them to the terminal. By redirecting output to a file we can easily merge multiple files into one.

#### Exercise 4

* Use `ls` with `wc` and `|` to count the number of  `.fasta` files in `~/hiv`
* Use `cat` with redirection to concatenate all `.fasta` files from your `~/hiv` directory into file `hiv_all.fasta` in your home directory.

---


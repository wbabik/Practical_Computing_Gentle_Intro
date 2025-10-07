# Class 2

# Text files, text editors and regular expressions
  * [Text vs. binary files](#text-vs-binary-files)
  * [Notepad++](#notepad)
  * [End-of-line and other non-printable characters](#end-of-line-and-other-non-printable-characters)
  * [Encoding](#encoding)
  * [Delimited text](#delimited-text)
  * [Regular expressions](#regular-expressions)
      * [Exercise 1](#exercise-1)
      * [Exercise 2](#exercise-2)
  
***  
  

## Text vs. binary files

At the very basic level, there are two types of computer files: text files and everything else, usually called binary files. Loosely speaking, text files contain lines of text, very little else, and are human readable. The content of binary files, on the contrary, is not human readable, but to convey information meaningful for the user it has to be interpreted by a dedicated program (or run, if it's an executable file). The distinction between text and binary files may, at the beginning, seem a bit vague, but hopefully things will become clearer as we move on.

Text files (sometimes called also plain text) are commonly used for storing and exchanging between programs various types of information. Therefore, an understanding of their structure, types and quirks is essential for any biologist.

We'll start with an example.
To make things confusing, files we usually open and save in one of the most popular text editing program, MS Word, are actually not text files, but rather binary files containing text. When opened in MS Word the file looks like this:

![Word-in-Word](text_Word_in_Word.png)

When we open the same file in Windows Notepad, dedicated for plain text, we see this:

![Word-in-Notepad](text_Word_in_Notepad.png)

Not really useful, huh?
Only when we ask MS Word to save this file as text (try it under `Save As...`) we get a text file per se.
Interesting things appear when we ask Word to save this as text file - there are a few questions to answer, some choices related to encoding and end of lines. Obviously there's something more to learn about text files. After saving the file as text, we can see its content in Notepad:

![Text-in_Notepad](text_Text_in_Notepad.png)

## Notepad++
To explore text files in more detail we need an appropriate tool. In this class we'll use Notepad++ for Windows. If you use Mac you can try BBEdit, TextMate, CotEditor or Visual Studio Code (VS Code). If you use Linux you can use nano, gedit or VS Code. For the rest of the class we'll assume that you have Notepad++ installed on your system (as it is in our computer room). If you want to install it at your private machine you can get it [here](https://notepad-plus-plus.org/downloads/), you will probably want to install the newest 64-bit version. Install the English language version. VS Code is a poweful program used by many programmers and is working under all platforms but for the purpose of simple text operations during today's classes it might be an overkill.  

Notepad++ is a plain text editor with many features, today we will use only a few to learn more about the nature of text files.

## End-of-line and other non-printable characters

Download file from [here](https://www.dropbox.com/s/stfdyaudt0dg0lb/Text_file_01.txt?dl=0), save it in your course directory and open in Notepad++. You should see something like this:

![Text in Notepad++](Text_file_01_in_Notepad++.png)



There are two lines of text in the file, with small orange dots in place of whitespaces between words. When you select `View -> Show Symbol -> Show All Characters`, you will see, in addition to text some extra symbols. These are letters `CR` and `LF` on black background at the end of the lines. These are two normally invisible characters that are inserted into text file when you press <kbd>Enter</kbd> to end a line of text. Unfortunately, end-of-line (EOL) symbols are system-specific: in Windows they are `CRLF`, on older Macs `CR` only, and in Linux and newer Macs `LF` only. Although it may seem just a curiosity, and in many situations it indeed doesn't matter, we're introducing this information here because it is a common enough source of frustration. Things don't work as they should although everything seems in order, and the the problem turns out to be in the EOL. The problem is easy to fix if you are aware of it.

In Notepad++ you can easily do EOL conversion selecting from menu: `Edit -> EOL Conversion`. Some programs, including MS Word, give you the option of various EOL types when saving as plain text.

Another important non-printable character is tabulator or `tab` that you insert by pressing <kbd>Tab</kbd>. In Notepad++ it is normally  displayed as an orange arrow, but many other programs don't display anything, just blank space. 

## Encoding

As most of early development in computers occurred in English-speaking countries, the supported character sets were English, or, more generally speaking, Latin alphabet-centric. In early days of text files only slightly more than 200 (or even fewer than 100) printable characters were available in the ASCII standard. This led to the development of various text encoding standards to represent various alphabets and sets of characters. These were usually not inter-compatible. Fortunately now a de facto standard called **UTF-8** exists. It is fully compatible with ASCII, as ASCII is just a subset of UTF-8. UTF-8 has an enormous capacity - it can represent more than one million characters. Currently ca. 150 thousands are in use, details can be found [here](https://www.unicode.org/versions/stats/). The full set of UTF-8 characters together with their codes, i. e., numbers that represent each character, can be found [here](https://www.utf8-chartable.de/).
Try to always use UTF-8 in your text files.


> ### Insert a UTF-8 character in Notepad++
> So how to get access to this plenty of UTF-8 characters? Under Windows probably the simplest way is to use Character Map program which is installed by default. For example to insert small Greek &#x03B1; character, find its Unicode code point (`03B1`) go to Character Map, enter this code in `Go to Unicode` field, then `Select` and `Copy` and then the character can be pasted into Notepad++. The method is a bit cumbersome, but it gives you access to any UTF-8 character, however exotic. 


## Delimited text

Information stored in text files is often structured. One of the most common ways of structuring information is in a way similar to what you see in spreadsheets, where observations are in rows and various attributes of observations are in columns, that is a row contains multiple fields (see also previous class). This kind of information can easily be represented in **delimited text files**. In such files a special character is used to delimit fields. Two types of delimited text files are the most popular: 
* **csv** or **comma separated values** - here comma (`,`) is used as field separator. However, in some languages, e. g., in Polish, `,` is used as the decimal point in numbers. Therefore a dialect of csv exists that uses semicolon (`;`) as delimiter. The csv is extremely popular, but one needs to remember about its dialects to avoid unexpected results. A clear advantage of csv is that the delimiter is always a visible character. An example of csv as displayed in Notepad ++:<br/> ![csv_inN++](csv_in_Notepad++.png)
* **tsv** or **tab separated values** - here `tab` is used as delimiter. `tab`, often represented as `\t` is normally not a visible character, which sometimes makes recognition of tab-separated files not so straightforward. On the other hand, tsv files are often easier to read and there is no problem with dialects. **Important !** <kbd>Tab</kbd> is different from <kbd>Space</kbd> and you should **NEVER** try to used multiple spaces instead of `tab`. An example of tsv as displayed in Notepad ++:<br/> ![tsv_in_N++](tsv_in_Notepad++.png)



## Regular expressions

Regular expressions or regexp allow us to look for patterns in text files. They are an extremely powerful and versatile tool and we'll encounter them over and over again during this course. Here's a gentle introduction, some examples and exercises.

> ### Regular expression symbols
> 
> Below are the most common symbols, for a more complete list see [here](https://www.regular-expressions.info/refquick.html)
> 
> `.` any single character
> 
> `?` preceding character occurred 0 or 1 times (`Bla?` will match `Bl` or `Bla` but not `Blaa`)
> 
> `*` preceding character occurred 0 or more times (`Bla*` will match `Bl`, `Bla` or `Blaa`)
> 
> `+` preceding character occurred 1 or more times (`Bla+` will match `Bla` or `Blaa`, but not `Bl`)
> 
> `{n}`   preceding character occurred exactly n times
> 
> `{n,m}`  preceding character occurred at least n times, but not more than m times
> 
> `[abc]` any single character from a set
> 
> `[^abc]` any single character **not** from a set
> 
> `[a-j]` any single character from a range (other examples `[A-Z]`, `[0-9]` etc.)
>
> `^` beginning of line
>
> `$` end of line
> 
> `()` parentheses can be used to group patterns. As we see below parentheses are also used to **capture** parts of expression for subsequent use.
>
> `|` alternative (`Bl(a|e)` will match `Bla` or `Ble`, it's equivalent to `Bl[ae]`; `cat|dog` will match `cat` or `dog`)
> 
> If you want to search for a character that has a special meaning, e. g., `*`, you should **escape** it with `\`, for example to look for:
> 
> `*` use `\*`
> 
> `tab` use `\t`
> 
> `CR` use `\r`
> 
> `LF` use `\n`
> 
> **Important**! Unfortunately there are some differences in implementation of regular expressions between programs. These differences are not large, but can matter in everyday life. You'll find a complete reference [here](https://www.regular-expressions.info/reference.html), and we'll also highlight the issue throughout the course.

#### Exercise 1

Download text file from [here](https://www.dropbox.com/s/hbiixi3g2udpbek/Ex_02_1.txt?dl=0) and open it in Notepad++. The file contains information about height of persons and animals. Use Notepad++ `Search -> Find...`  with `Search Mode` set to `Regular expression` and `Match case` field checked to find the following (and write down the regular expressions you used):
* persons with (given) name starting with L (`L` at the beginning of line)
* persons with (given) name starting with L or animals with species name staring with l (`L` or `l` at the beginning of line)
* persons/animals taller than 2 meters (**tip**: use alternative and parentheses to group expressions)

---

> ### Searching and replacing with regular expressions
> You can **capture** a part of regular expression for subsequent use. This allows using regular expressions to find patterns and modify them. Imagine that you have three binomial Latin species names:
> ```
> Rana arvalis
> Rana dalmatina
> Rana temporaria
> ```
> You want to replace them with trinomial names (Genus species subspecies) of the nominal subspecies. To do it using a single Search-and-Replace command we note that we want to duplicate a string of characters preceded by space, i. e., `  [a-z]+`. We can capture this expression enclosing it in parentheses `( [a-z]+)`and then reuse it. Copy the three species names into Notepad++, so that each is in a separate line, then use `Search -> Replace ...` with `Search Mode` set to `Regular expression` to replace binominal to trinomial names. In the `Find what` field type `( [a-z]+)` and in the `Replace with` field type `\1\1` - in this way you refer to the first (and the only one in this case) captured group and you use it twice. To make your expression more robust you could use `( [a-z]+)$` as search pattern and `\1\1` as replace pattern- then you'd make sure than only the last word in the line is replicated.

#### Exercise 2
Download text file from [here](https://www.dropbox.com/s/gruaw8vqgnwas8l/Ex_02_2.txt?dl=0) and open it in Notepad++. This file contains long lines, you can toggle line wrapping selecting from menu `View -> Word wrap`. Answer the following questions
* what type of delimited file is this (csv, tsv, other?)
* what type of EOL is there?
* the first column contains 4-digit individual id, the second column contains information about species, population (as name and number) and geographic region as `_` separated fields in the form `popID_region_species_popNr`. Use regular expressions with Notepad++ `Search -> Replace ...` to change the order of the fields in the second column to `species_region_popID_popNr`.
* use `Search -> Replace ...` to change EOL into the Linux-style using regexp.

---


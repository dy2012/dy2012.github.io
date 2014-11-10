---
layout: post

title: Some tips for grep

tags: [shell, linux]

---
# Some tips for grep

>Global-Regular-Expression-Print(GREP) is a command line text search utility used in Unix & Unix-like system.
>
>>The "grep" command searches files or standard input for lines that match a given regular expression. It then prints the matching lines to the program's standard output.

### The basic options

* "-i" Ignore case sensitivity.

* "-b" Display block numbers at the begining of every line.

* "-n" Display matches lines and line numbers.

* "-v" Display lines that do not match.
* "-o" Show only the matched string.
* "-l" Display only the file names which matches the given pattern.
* "-r" Search a string recursively in all Directories.

####1.Grep for a string, but show the preceding 5 lines and following 5 lines as well as the matched the line.

> -B number to set how many lines before the match and -A number for the number of lines after the match.

	`grep -B number -C number searchstring file`
> -C  number to get the same amount of lines before and after the match.
    
	`grep -C number searchstring file`

####2, Checking for full words, not for sub-strings using -w.

	`grep -iw "string" file`

####3, Counting the number of matches.

	`grep -c "pattern" file`

####4, Search a string in Gzipped files.

	`zgrep -i searchstring file`

####5, Match regular expression in files.(egrep) 

	`grep -E`

####6, Search a Fixed Pattern String.(fgrep)

	`grep -F`



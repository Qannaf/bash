<p align="center">
  <img width="450" height="150" src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/82/Gnu-bash-logo.svg/1200px-Gnu-bash-logo.svg.png">
</p>

# bash Notes For Professionals

# Table of contents
1. [Chapter 1: Getting started with Bash](#1)
    1. [Hello World](#1a)
	1. [Hello World Using Variables](#1b)
	1. [Hello World with User Input](31c)
	1. [Importance of Quoting in Strings](#1d)
	1. [Viewing information for Bash built-ins](#1e)
	1. [Hello World in "Debug" mode](#1f)
	1. [Handling Named Arguments](#1g)
1. [](#1)
1. [](#1)

<a name="1"></a>

# Chapter 1: Getting started with Bash

<a name="1a"></a>
## 1.1. Hello World

* Interactive Shell

```BASH
echo "Hello World"
```

* Non-Interactive Shell
Follow these steps to create a Hello World script:

  * Create a new file called hello-world.sh

	```BASH
	nano helloWorld.sh
	```

  * Add this code:
	```BASH
	#!/bin/bash
	echo "Hello World"
	```

  * Execute the helloWorld.sh script from the command line using one of the following:

	```BASH
	./helloWorld.sh 	– most commonly used, and recommended
	/bin/bash helloWorld.sh
	bash helloWorld.sh 	– assuming /bin is in your $PATH
	sh helloWorld.sh
	```

<a name="1b"></a>

## 1.2. Hello World Using Variables
  * Create helloVariable.sh
	```BASH
	nano helloVariable.sh
	```
  * Add this code:
	```BASH
	#!/usr/bin/env bash
		printf "Hello, %s\n" "$1"			$1, which is the first command line argument
	#> Hello, Qannaf
	```
  * Execute the helloVariable.sh
	```BASH
	./helloVariable.sh Qannaf				output #> Hello, Qannaf
	```

<a name="1c"></a>

## 1.3. Hello World with User Input
  * Create helloUser.sh
	```BASH
	nano helloUser.sh
	```
  * Add this code:
	```BASH
	#!/usr/bin/env bash

	echo "Who are you?"
	read user
	echo "Hello, $user."

	echo "What are you doing?"
	read action
	echo "You are ${action}ing."


	echo "bye $user. :)"
	```

  * Execute the helloVariable.sh
	```BASH
	./helloUser.sh 				output #> Who are you?
							  Qannaf
							  Hello, Qannaf.
							  What are you doing?
							  learn
							  You are learning.
							  bye Qannaf. :)
	```

<a name="1d"></a>
## 1.4. Importance of Quoting in Strings	printString.sh

```BASH
variable="Qannaf"
#*Weak: uses double quotes: "
echo "Hello $variable"				
#> Hello Qannaf

#*Strong: uses single quotes: 
echo 'Hello $variable'				
#>Hello $variable

#You can also use escape to prevent expansion:
echo "Hello \$variable"				
#>Hello $variable
```

<a name="1e"></a>

## 1.5. Viewing information for Bash built-ins
```BASH
help <command>	This will display the Bash help (manual) page for the specified built-in.	For example, help unset 
To see a list of all built-ins with a short description, use help -d
```

<a name="1f"></a>

## 1.6. Hello World in "Debug" mode	debug.sh
  * See what was writting in debug.sh
	```BASH
	cat debug.sh						     		output
													#!/bin/bash
													echo "Hello World\n"
													var="s"
													v=$(expr 5 + $var)
	```
  * debug debug.sh file
	```BASH
	bash -x debug.sh 
	```

<a name="1g"></a>

## 1.7: Handling Named Arguments	handlingNameArg.sh
```BASH
#!/bin/bash
deploy=false
uglify=false
while (( $# > 1 )); do case $1 in
--deploy) deploy="$2";;
--uglify) uglify="$2";;
*) break;
esac; shift 2
done
$deploy && echo "will deploy... deploy = $deploy"
$uglify && echo "will uglify... uglify = $uglify"
# how to run
# chmod +x handlingNameArg.sh
# ./handlingNameArg.sh --deploy true --uglify false
#>will deploy... deploy = true
```

# Chapter 2: Script shebang
## 2.1: Env shebang
`````
#!/usr/bin/env bash
echo "Env shebang"
#>envShebang.sh							output: Env shebang
#>bash envShebang.sh
`````

## 2.2: Direct shebang
`````
#!/bin/bash
echo "Direct shebang"
#>directShebang.sh						output: Direct shebang
#>bash directShebang.sh
`````


## 2.3: Other shebangs
`````
#!/bin/bash something wrong
echo "This line never gets printed"			
#>otherShebang.sh						output: /bin/bash: something wrong: No such file or directory

`````

# Chapter 3: Navigating directories
## 3.1: Absolute vs relative directories
* Absolute
use the entire name, starting with a slash /:
```
cd /home/Qannaf//bash/section3
````
* relative
to change to a directory near your current directory
For example, if you are already in /home/Qannaf//bash/ you can enter the subdirectory section3 :
```
cd abc
```
* going "up" a directory
to go to the directory above the current directory 
For example, if you are already in /home/Qannaf//bash/section3 and wanted to go to already in /home/Qannaf//bash/ :
```
cd ..
```

## 3.2: Change to the last directory
```
cd -
```

## 3.3: Change to the home directory
* The default directory 
```
cd
```
* Explicit:
```
cd $HOME
```
* A shortcut for the home directory is ~, so that could be used as well.
```
cd ~
```

## 3.4: Change to the Directory of the Script
```
cd "$(dirname "$(readlink -f "$0")")"          this will be change the dirctory to /usr/bin
```
This command runs 3 commands:
1. readlink -f "$0" determines the path to the current script ($0)
2. dirname converts the path to script to the path to its directory
3. cd changes the current work directory to the directory it receives from dirname


# Chapter 4: Listing Files
```
Option Description
-a, --all 				List all entries including ones that start with a dot
-A, --almost-all 		List all entries excluding . and ..
-c 						Sort files by change time
-d, --directory 		List directory entries
-h, --human-readable 	Show sizes in human readable format (i.e. K, M)
-H 						Same as above only with powers of 1000 instead of 1024
-l 						Show contents in long-listing format
-o 						Long -listing format without group info
-r, --reverse 			Show contents in reverse order
-s, --size 				Print size of each file in blocks
-S 						Sort by file size
--sort=WORD 			Sort contents by a word. (i.e size, version, status)
-t 						Sort by modification time
-u 						Sort by last access time
-v 						Sort by version
-1 						List one file per line
```
* File Type
The file type can be one of any of the following characters.
Character File Type
```
- Regular file
b Block special file
c Character special file
C High performance ("contiguous data") file
d Directory
D Door (special IPC file in Solaris 2.5+ only)
l Symbolic link
M Off-line ("migrated") file (Cray DMF)
n Network special file (HP-UX)
p FIFO (named pipe)
P Port (special system file in Solaris 10+ only)
s Socket
? Some other file type
```
## 4.1: List Files in a Long Listing Format
```
ls -l 
```

## 4.2: List the Ten Most Recently Modified Files
```
ls -lt | head
```

## 4.3: List All Files Including Dotfiles
```
ls -a		or ls -A
ls -all
```

## 4.4: List Files Without Using `ls`

* display the files and directories that are in the current directory
```
printf "%s\n" *
```
* display only the directories in the current directory
```
printf "%s\n" */
```
* display only (some) image files
```
printf "%s\n" *.{gif,jpg,png}
printf "%s\n" *.{pdf,}
```

* iterate over them
```
for file in "${files[@]}"; do
echo "$file"
done
```

## 4.5: List Files
```
ls
```

## 4.6: List Files in a Tree-Like Format
```
tree /folderName	or		tree /f
tree -L 1 -d /tmp
```

## 4.7: List Files Sorted by Size
```
ls -l -S -r ./section1	-S option sorts the files in descending order of file size.
ls -l -S -r ./section1	-r option the sort order is reversed.
```

# Chapter 5: Using cat
```
Option Details
-n 	Print line numbers
-v 	Show non-printing characters using ^ and M- notation except LFD and TAB
-T 	Show TAB characters as ^I
-E 	Show linefeed(LF) characters as $
-e 	Same as -vE
-b 	Number nonempty output lines, overrides -n
-A 	equivalent to -vET
-s 	suppress repeated empty output lines, s refers to squeeze
```

## 5.1: Concatenate files
```
cat file1 file2 file3 > file_all
```
cat can also be used similarly to concatenate files as part of a pipeline, e.g.
```
cat file1 file2 file3 | grep foo
```

## Section 5.2: Printing the Contents of a File
* print the contents of a file.
	```
	cat file.txt
	```
* If the file contains non-ASCII characters
	````
	cat -v unicode.txt	This can be quite useful for situations where control characters would otherwise be invisible.
	```
* for interactive
	```
	less file.txt	or 	more file.txt
	```
* To pass the contents of a file as input to a command
	```
	tr A-Z a-z <file.txt # as an alternative to cat file.txt | tr A-Z a-z
	```
* In case the content needs to be listed backwards from its end 
	```
	tac file.txt
	```
* If you want to print the contents with line numbers, then use -n with cat:
	```
	cat -n file.txt
	```
* To display the contents of a file in a completely unambiguous byte-by-byte
	```
	printf 'Hëllö wörld' | xxd
	#>0000000: 48c3 ab6c 6cc3 b620 77c3 b672 6c64 H..ll.. w..rld
	```

## 5.3: Write to a file
* write to file
	```
	cat >file.txt	will let you write the text on terminal which will be saved in a file named file.		
	cat >>file.txt 	will do the same, except it will append the text to the end of the file.
	```
N.B: Ctrl+D to end writing text on terminal (Linux)

*stop condition
	```
	cat <<END >>file	
	cat <<stop>>file
	```

## 5.4: Show non printable characters	file.txt
```
cat -v file.txt	 	or
cat -vE file.txt 		#Useful in detecting trailing spaces.
```
e.g.
```
echo 'ض' | cat -vE		
echo 'ض' | cat -A
```

## 5.5: Read from standard input
```
cat < file.txt
printf "first line\nSecond line\n" | cat -n	
```
The echo command before | outputs two lines. The cat command acts on the output to add line numbers.

5.6: Display line numbers with output
* Use the --number flag to print line numbers before each line. Alternatively, -n does the same thing.
	```
	$ cat --number file.txt 	or 		cat file.txt | cat -n
	1 line 1
	2 line 2
	3
	4 line 4
	5 line 5
	```
* To skip empty lines when counting lines, use the --number-nonblank, or simply -b.
	```
	$ cat -b file
	1 line 1
	2 line 2
	3 line 4
	4 line 5
	```

## 5.7: Concatenate gzipped files
* Files compressed by gzip can be directly concatenated into larger gzipped files.
	```
	cat file1.gz file2.gz file3.gz > combined.gz
	```
* This is a property of gzip that is less efficient than concatenating the input files and gzipping the result:
	```
	cat file1 file2 file3 | gzip > combined.gz
	```
e.g:
``````
echo 'Hello world!' > helloWorld.txt
echo 'Hollo Qannaf!' > helloQannaf.txt
gzip helloWorld.txt
gzip helloQannaflloQ.txt
cat helloWorld.txt.gz helloQannaf.txt.gz > greetings.txt.gz
gunzip greetings.txt.gz
cat greetings.txt
``````
Which results in
``````
Hello world!
Hello Qannaf!
``````


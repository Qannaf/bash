# bash Notes For Professionals

# Chapter 1: Getting started with Bash
## 1.1. Hello World
* Interactive Shell
``````
echo "Hello World"
``````

* Non-Interactive Shell
Follow these steps to create a Hello World script:

  * Create a new file called hello-world.sh
	``````
	nano helloWorld.sh
	``````

  * Add this code:
	``````
	#!/bin/bash
	echo "Hello World"
	``````

  * Execute the helloWorld.sh script from the command line using one of the following:
	``````
	./helloWorld.sh 	– most commonly used, and recommended
	/bin/bash helloWorld.sh
	bash helloWorld.sh 	– assuming /bin is in your $PATH
	sh helloWorld.sh
	```````


## 1.2. Hello World Using Variables
  * Create helloVariable.sh
	``````
	nano helloVariable.sh
	``````
  * Add this code:
	``````
	#!/usr/bin/env bash
		printf "Hello, %s\n" "$1"			$1, which is the first command line argument
	#> Hello, Qannaf
	```````
  * Execute the helloVariable.sh
	``````
	./helloVariable.sh Qannaf				output #> Hello, Qannaf
	```````

## 1.3. Hello World with User Input
  * Create helloUser.sh
	```````
	nano helloUser.sh
	```````
  * Add this code:
	``````
	#!/usr/bin/env bash

	echo "Who are you?"
	read user
	echo "Hello, $user."

	echo "What are you doing?"
	read action
	echo "You are ${action}ing."


	echo "bye $user. :)"
	``````
  * Execute the helloVariable.sh
	``````
	./helloUser.sh 				output #> Who are you?
							  Qannaf
							  Hello, Qannaf.
							  What are you doing?
							  learn
							  You are learning.
							  bye Qannaf. :)
	```````

## 1.4. Importance of Quoting in Strings	printString.sh
`````
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
`````

## 1.5. Viewing information for Bash built-ins
`````
help <command>	This will display the Bash help (manual) page for the specified built-in.	For example, help unset 
To see a list of all built-ins with a short description, use help -d
`````

## 1.6. Hello World in "Debug" mode	debug.sh
  * See what was writting in debug.sh
	`````
	cat cat debug.sh								output
													#!/bin/bash
													echo "Hello World\n"
													var="s"
													v=$(expr 5 + $var)
	`````
  * debug debug.sh file
	```````
	bash -x debug.sh 
	```````

## 1.7: Handling Named Arguments	handlingNameArg.sh
`````
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
`````

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

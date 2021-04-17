# bash Notes For Professionals
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

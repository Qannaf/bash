# bash Notes For Professionals
## 1.1. Hello World
* Interactive Shell
````
echo "Hello World"
````

* Non-Interactive Shell
Follow these steps to create a Hello World script:
	1. Create a new file called hello-world.sh
````
Nona helloWorld.sh
````
	2. Add this code:
````
#!/bin/bash
echo "Hello World"
````

	3. Execute the helloWorld.sh script from the command line using one of the following:
````
./hello-world.sh – most commonly used, and recommended
/bin/bash hello-world.sh
bash hello-world.sh – assuming /bin is in your $PATH
sh hello-world.sh
`````
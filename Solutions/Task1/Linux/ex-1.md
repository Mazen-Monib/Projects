### Exercise 1: Getting Familiar with File Management

1. Create a directory named devops_project in your home directory.
	
**	cd 
	mkdir devops_project

2. Inside the devops_project folder, create the following structure using a single command:
    ```sh
    devops_project/
    ├── scripts/
    ├── bin/
        └── tools/
    └── logs/
    ```


**	sudo mkdir –p devops_project/{scripts,bin/tools,logs}


3. Create an empty file called deploy.sh under scripts/ folder.


**	  cd devops_project/scripts
	 touch deploy


4. Use the echo command to add the line #!/bin/bash at the beginning of ```deploy.sh```.


**	 sudo echo ‘#!/bin/bash’ > deploy.sh


5. Add to ```deploy.sh``` commands to save the size and permissions of the 
devops_project dir and sub-dirs to file ```logs/tree.txt``` using appropriate commands.


**	echo ‘du –h devops_project > devops_project/logs/tree’ >devops_project/scripts/deploy


6. Change the permissions to make the script executable for the owner only.


**	sudo chmod 100 devops_project/scribts/deploy.sh


7. Create a compressed archive of the entire devops_project/ directory using tar.


**	tar -czvf devops_project.tar.gz devops_project/


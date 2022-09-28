## How to create a new git repository?

  - create a directory to store the files of your new repository:  

	`mkdir test/`  

  - change the current wokring directory to the new directory:  

	`cd test`

  - create a file so your repository will not be empty:  

	`vim test.py`

  - initialize the current directory as a new repository with the following command:  

	`git init`  

  - add all the existing files to the repository:
	
	`git add .`  

  - optionally create a .gitignore file in which you can list all of the files which should not be tracked by git:

	`touch .gitignore`

  - you've just created a new file so let's also add this to the repository:
	
	`git add .gitignore`

  - the status of the repository can be checked with git status command, these changes have not been committed yet:

	```
	➜  test git:(master) ✗ git status
	On branch master

	No commits yet

	Changes to be committed:
	(use "git rm --cached <file>..." to unstage)
		new file:   .gitignore
		new file:   test.py

	```

  - lets commit the new changes with git commit, every commmit should contain a short message describing what was changed or updated in the repo. Commit messages can be written between double quotes with the -m option:

	```
	➜  test git:(master) ✗ git commit -m "Initial commit..."
	[master (root-commit) 4d05bed] Initial commit...
	2 files changed, 1 insertion(+)
	create mode 100644 .gitignore
	create mode 100644 test.py

	➜  test git:(master) git status
	On branch master
	nothing to commit, working tree clean

	```

  - the branh is called 'master' by default, ideally this should be changed with git branch command:

	```
	➜  test git:(master) git branch -M main
	➜  test git:(main) git status
	On branch main
	nothing to commit, working tree clean

	```

  - now that the repository is working locally it can be added to a remote repository manager like github:

	```

	➜  test git:(main) git remote add origin https://github.com/gaborracz/test.git

	```

  - the remote repository is still empty at this point so we shoud push the changes from our local repo:

	```

	➜  test git:(main) git push -u origin main
	Enumerating objects: 4, done.
	Counting objects: 100% (4/4), done.
	Delta compression using up to 8 threads
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (4/4), 301 bytes | 301.00 KiB/s, done.
	Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
	To https://github.com/gaborracz/test.git
	* [new branch]      main -> main
	Branch 'main' set up to track remote branch 'main' from 'origin'.
	
	```
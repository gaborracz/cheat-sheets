## What is SED and how to use it?

  - The sed utility reads the specified files, or the standard input if no files are specified, modifying the input as specified by a list of commands.  The input is then written to the standard output.

  - A single command may be specified as the first argument to sed.  Multiple commands may be specified by using the -e or -f options.  All commands are applied to the input in the order they are specified regardless of their origin.

  - replace all occurences in a text file, for example find all occurences of 'windows' in the file named test, replace them with 'linux' and write the changes to the test.new file:  

    `sed 's/windows/linux/g' test > test.new` or if you do not want to create a new file:  

    `sed -i "" "s/windows/linux/g" test`  



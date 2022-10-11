## What are hidden files and why do you need to view them?  
___  
</br>  

  - MacOS has Unix roots therefore if a file or folder name starts with a dot the OS will automatically hide it  
  - hidden files can be listed with `ls -a` option in terminal  
  - for example this output shows configuration files related to ZSH in the user's home directory:
  
     ```text

    ➜  ~ ls -la | grep zsh
    drwxr-xr-x   22 gaborracz  staff       704 Jul 19 07:51 .oh-my-zsh
    -rw-------    1 gaborracz  staff    136940 Oct 11 18:01 .zsh_history
    drwx------   56 gaborracz  staff      1792 Oct 11 17:10 .zsh_sessions
    -rw-r--r--@   1 gaborracz  staff      4783 Oct 11 13:48 .zshrc
    -rw-r--r--    1 gaborracz  staff       477 Jul 19 07:46 .zshrc.pre-oh-my-zsh
    ➜  ~ 

     ```

  - in order to make configuration changes to ZSH you need to edit `.zshrc` file, I like to do this with an editor which supports syntax highliting - like Notepad++ or VS Code. Problem is that by default you cannot browse hidden files.  

## Show hidden files - using terminal 
___  
</br>  

  - AppleShowAllFiles should be set to true with the following command:  
    
    `defaults write com.apple.Finder AppleShowAllFiles true`  

  - to take effect restart Finder:  
  
    `killall Finder`

## Simple script to do these steps:  
___  
</br>

  - I tend to forget things which I don't use regularly, so here is a simple script to do these two steps - I've used ZSH ability to create functions in the .zshrc file:  
  
    ```sh

    ### show hidden files ###

    function show-hidden-files() {
    defaults write com.apple.Finder AppleShowAllFiles true
    killall Finder
    }


    ### show hidden files ###

    function hide-hidden-files() {
    defaults write com.apple.Finder AppleShowAllFiles false
    killall Finder
    }

    ```  

  - after making any changes to .zshrc config file make sure to reload the terminal application or source the file with the following command:  

    `source .zshrc`  

  - now I can use these scripts to show or hide hidden files:  

    ```text

    ➜  ~ show-hidden-files
    ➜  ~ # hidden files are shown in Finder 
    ➜  ~ hide-hidden-files
    ➜  ~ # files are hidden again in Finder

    ```
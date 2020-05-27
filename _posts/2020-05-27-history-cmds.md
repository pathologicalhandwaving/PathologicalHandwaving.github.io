---
title: Hiding Shell History
date: 2020-05-27
tags:
  - bash
  - history
  - tracking
---

There are some situtations in which one might want to hide their shell history. Most of the time when I am asked to work on someone else's box I leave the bash history intact, (its polite). But sometimes you just need a clean or amended record, there are many ways to accomplish this. 

## During a Session

  * `set history +o` Can be run at any point in a session, results in all session commands not being written to the log.
  * `set history -o` Turns logging back on but also logs the `set history -o` command, which makes it obvious something was done.
  * `set history -c` Completely clears the history file. Very obvious you did something since everything is now gone.
  * `set history -r` Reads the history file, setting it back to how it was when you logged in. Edit the history file, issue command, close shell.


## Useful Variables

### `HISTFILE` Variable

The `HISTFILE` variable controls where the history file is stored, running `unset HISTFILE` will clear this location from memory so nothing will be stored.

To specify the history file location put the following in your `.bashrc`:

``` bash
export HISTFILE=/path/to/file
```


### `HISTCONTROL` Variable

The `HISTCONTROL` variable can be set in your `.bashrc` file. Flags:

  * `ignoredups` Ignore duplicate commands
  * `ignorespace` Ignore commands prefixed with a space.
  * `ignoreboth` Ignore duplicates and space prefixed commands.
  
  
  ``` bash
  export HISTCONTROL=ignoreboth
  ```
  
  
  ### `HISTIGNORE` Variable
  
  You can also ignore certain commands altogether:
  
  ``` bash
  export HISTIGNORE="kill*:ifconfig*:nmap*"
  ```
  
  ### `HISTFILESIZE` Variable
  
  Default size of the `HISTFILESIZE` variable is 500 commands.
  
  
  ``` bash
  export HISTFILESIZE=0
  ```
  
  
  ## Send to `/dev/null`
  
  
  ``` bash
  ln -sf /dev/null ~/.bash_history
  ```
  
  
  ## Overwrite `auth.log`
  
  
  ``` bash
  echo "" > /var/log/auth.log
  ```
  
  
 ## Kill Current Session
 
 
 ``` bash
 kill -9 $$
 ```
 
 
 ## Check Your History
 
 
 ``` bash
 history|more
 ```
  
  

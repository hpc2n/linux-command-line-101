# Hints and tricks 

This section contains some hints that might make working with Linux easier. 

## Tab auto-complete

If you press TAB on the keyboard after starting to type a command or a file, it will auto-complete if no other matches or else suggest possible matches. 

## Short-cuts on the CLI

CTRL-SOMEKEY refers to pressing down the CTRL key and then another key while continuing to hold down CTRL. 

Examples: 

- **CTRL-a**: Go to the beginning of the line
- **CTRL-e**: Go to the end of the line
- **CTRL-l**: Clear the terminal
- **TAB**: Auto-complete (i.e. start write a command or file name and then press TAB to auto-complete as far as possible
- **ARROW-UP**: Pressing the arrow-up key repeatedly will let you cycle through recent commands
- **CTRL-r**: you will get a prompt to write text to search in the list of recent commands. The list is saved in <code>.bash_history</code> in your $HOME. On some systems it might be called <code>.bash.history</code>

## Finding help 

You can often get more info on the usage of a Linux command.  This includes options and flags. Depending on the setup of your system either or both of the following should succeed:

- ``COMMAND --help``
- ``man COMMAND``

where COMMAND is the Linux command you want information about, like ``ls``, ``mkdir``, ``gcc``, etc. 

## Misc

- Type ``clear`` to clear the terminal
- Type ``history`` to see a list of the recent commands used in the terminal
    - You can change the number of saved commands by setting the environment variable HISTSIZE in your <code>.bashrc</code> file in your home directory. 
    - Example: Open <code>.bashrc</code> with <code>nano</code>. Somewhere (at the end for instance) add: <code>export HISTSIZE=NUMBER</code> where <code>NUMBER</code> is the number of commands to save, for instance 500. 

!!! warning Passwords in the history file

    If you enter a password (e.g. login for a computer or website) at the command prompt and hit returnm the password will be included into the <code>.bash_history</code> file.  This is not encrypted in any way.  In particular when using a shared system as offered by NAISS, it is best to reset the password to a new, save value on the computer or website where you have been using it.


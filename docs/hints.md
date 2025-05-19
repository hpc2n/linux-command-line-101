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
- **TAB**: Auto-complete (i.e. start write a command or file name and then press TAB to auto-complete, if possible)
- **ARROW-UP**: Pressing the arrow-up key repeatedly will let you cycle through recent commands
- **CTRL-r**: you will get a prompt to write text to search in the list of recent commands. The list is saved in <code>.bash.history</code> in your $HOME. 

## Finding help 

You can often get more info on flags/options and usage for a Linux command with

- ``COMMAND --help``
- ``man COMMAND``

where COMMAND is the Linux command you want information about, like ``ls``, ``mkdir``, ``gcc``, etc. 

## Misc

- Write 'clear' to clear the terminal
- write 'history' to see a list of the most recent commands written in the terminal
    - You can change the number of saved commands by setting the environment variable HISTSIZE in your <code>.bashrc file</code> in your home directory. 
    - Example: Open <code>.bashrc</code> with <code>nano</code>. Somewhere (at the end for instance) add: <code>export HISTSIZE=NUMBER"</code> where <code>NUMBER</code> is the number of commands to save, for instance 10000. 
- <code>man PROGRAM</code> will give you the manual for a specific program or command, if it exists
    - Example: <code>man gcc</code> will give open manual/help for the compiler <code>gcc</code>, containing flags to the compiler etc. **Note** that you need to first load a module that has gcc in. 


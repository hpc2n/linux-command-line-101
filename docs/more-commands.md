# More (advanced) commands. 

## Alias 

You will often have to write the same command again and again. If it is a longer command, it is reducing your productivity having to repeat it. Then you can use the <code>alias</code> command to create an 'alias' for your command.

To see the currently definted aliases, execute the 'alias' command:

```bash
$ alias
```

!!! Example "Example"

    This is how it might look when you run <code>alias</code>:

    ```bash
    b-an01 [~]$ alias
    alias cdn='cat >/dev/null'
    alias dir='ls -lAF'
    alias l='dir'
    alias ls='ls -F'
    ```

    As an example, this means that if you type 'dir' the actual command that is executed is 'ls -lAF'.

In order to create a new alias, you could write:

```bash
$ alias shortName="your custom command here"
```

!!! Warning

    The alias will only be valid in that shell, and only until you logout. Next time you will have to issue the 'alias' command again, unless you add it to either your <code>.bashrc</code> or <code>.bash.profile</code> file.

!!! Example "Adding a new alias to the .bashrc file, using 'nano' editor"

    1. Open the file: <code>nano ~/.bashrc</code>

    2. Inside the editor, scroll down to where your aliases are. If you do not have any, just add them at the end, like this
    ```bash
    #My custom aliases
    alias c="clear"
    alias ll="ls -alF"
    # Colourize ls output
    alias ls='ls --color=auto'
    # Colourize grep output
    alias grep='grep --color=auto'
    # Easily list my SLURM batch jobs
    alias jobs='squeue -u $USER'
    # Find all entries starting with d in the output from the ls -lahrt command
    alias ldir=’ls -lahrt | egrep "^d"’
    ```
    3. Save and Exit the file: <code>CTRL-x</code> (Press CTRL and hold it down while pressing x). Answer 'Y' to save.
    4. Next time you start a shell or after a new login your new alias is available. To make it available immediately, run
    ```bash
    $ source ~/.bashrc
    ```

## awk 

Powerful, but somewhat more advanced command!

This command finds patterns in a file and can perform arithmetic/string operations. You can use it to transform data files and produce formatted reports.

It allows the user to use variables, numeric functions, string functions, and logical operators.

Things ``awk`` can do:

- Scan a file line by line
- Split each input line into fields
- Compare input line/fields to pattern
- Perform action(s) on matched lines

!!! Example "Search for the pattern 'snow' in the file FILE and print out the first column"

    ```bash
    awk '/snow/ {print$1}' FILE
    ```

!!! Example "Print column 3 and 4 from file mydata.dat"

    ```bash
    awk '{print $3 "\t" $4}' mydata.dat
    ```

!!! Example "Print column 2 and 3 from file mydata.dat, but only those rows that contain the letter 'r'"

    ```bash
    awk '/r/ {print $2 "\t" $3}' mydata.dat
    ```

## chown - change ownership

To change ownership of a file or directory, use the command <code>chown</code>.

<div>
```bash
chown [OPTIONS] USER[:GROUP] FILE(s)
```
</div>

!!! Note "Examples"

    - <code>chown USERNAME FILE</code> the user with USERNAME becomes the new owner of FILE
    - <code>chown USERNAME DIRECTORY</code> the user with USERNAME becomes the new owner of DIRECTORY (but not any subdirectories)
    - <code>chown USERNAME:folk DIRECTORY</code> the user ownership is changed to USER and the group ownership to group "folk" for the directory DIRECTORY
    - <code>chown :folk DIRECTORY</code> the group ownership is changed to the group "folk" for the directory DIRECTORY
    - <code>chown -R USERNAME:folk DIRECTORY</code> the user ownership is changed to USERNAME and the group ownership is changed to group "folk" for the directory DIRECTORY and all subdirectories

!!! Warning

    As default, <code>chown</code> does not generate output on success and returns zero.



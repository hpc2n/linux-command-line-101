# Scripting


!!! note "Learning objectives"

    **Questions** 

    * What is a script?
    * What are file permissions?
    * How do I write a script? 
    * How do I execute a script?

    **Objectives** 

    * Learn how to make a simple script 
    * Get a brief introduction to **permissions**

This section will look at scripting. Scripting is used to perform complex or repetitive tasks without user intervention. All Linux commands which can be used on the commandline can also be used inside a script, including wild cards. 

The most common reason for making a script is probably to avoid writing the same command again and again.  On an HPC-sytem, such as the ones offered by NAISS, scripts are required to execute Linux commands and programs inside the batch system.

!!! Hint "Code along!" 

    Try out or code along for some of these examples. 

    You can use the contents of the directory ``/exercises/script`` that you got from the downloaded tarball (<a href="https://github.com/hpc2n/linux-command-line-101/raw/refs/heads/main/exercises.tar.gz">exercises.tar.gz</a>) to play with. If you have not done so already, right-click and save to download, or right-click and copy the url, then do ``wget THE-URL-YOU-COPIED`` in a terminal window to download it there. Then do <code>tar -zxvf patterns.tar.gz</code> to unpack.  

## Starting with a motivational example
We start scripting with a simple example.  The task at hand is to check how many lines of the file ``file.dat`` contain the string 'ABCD'.  This time we want to do this with a script.  

!!! Example to code along

    Use an editor, e.g. `nano` to create the file ``my_first.sh``. The file should contain the following:

    ```bash
    #!/bin/bash
    grep 'ABCD' file.dat > file_filtered.dat 
    wc -l < file_filtered.dat > output.dat
    ``` 

    With the following command, which will be explained in-depth further down, we can make the script executable 

    ```bash
    $ chmod u+x my_first.sh
    ```

    Now we can execute the script:

    ```bash
    $ ./my_first.sh
    ```
    
    You should get the number 2 as a result.  Confirm this by looking into the file ``file.dat``.  With a single line we executed both commands `grep` and `wc`. 

**What it does**

- First line of the script: telling the system it should be executed in the ``bash`` shell, since commands differ between shells (the program loader is told to run the program ``/bin/bash`` as first argument). ``#!`` are called **shebang**.  This has to be the first line. 
- second line: search for the string ``ABCD`` in the file ``file.dat``, then redirect the output to the file ``file_filtered.dat`` 
- third line: run the command ``wc -l`` with the file ``file_filtered.dat`` as input. It then redirects the output to the file ``output.dat``.  

We can now execute two Linux commands with a single line.

## Permissions  

We have used the command ``chmod`` in the above example.  

!!! note 

    The command <code>chmod</code> is used to change permissions for files and directories.

Permissions are needed to, among other things, make a file executable. 

**Let us take a look at an example** 

When running the command ``ls -la`` you should get an output similar to the below:

```bash
$ ls -la  
total 64
drwxr-xr-x 11 joachim  staff  352 Sep 29 16:47 .
drwxr-xr-x  6 joachim  staff  192 Sep 29 16:29 ..
-rwxr-xr-x  1 joachim  staff   99 Sep 29 17:30 analysis.sh
-rw-r--r--  1 joachim  staff  120 Sep 29 17:30 file.dat
-rw-r--r--  1 joachim  staff  128 Sep 29 17:30 file.txt
-rw-r--r--  1 joachim  staff  188 Sep 29 17:30 file2.dat
-rw-r--r--  1 joachim  staff   54 Sep 29 17:30 filtered_file.dat
drwxr-xr-x 13 joachim  staff  416 Sep 29 17:30 image
-rwxr-xr-x  1 joachim  staff  153 Sep 29 17:30 imagefind.sh
-rwxr--r--  1 joachim  staff   80 Sep 29 17:30 my_first.sh
-rwxr-xr-x  1 joachim  staff    9 Sep 29 17:30 program.sh
```

If you look at the left-most column, you see an example of **permissions**. 

!!! Note "There are three types of permission groups"

    - **owners**: these permissions will only apply to owners and will not affect other groups.
    - **groups**: you can assign a group of users specific permissions, which will only impact users within the group. The members of your storage directory belongs here.
    - **all users**: these permissions will apply to all users, so be careful with this.

!!! Note "There are three kinds of file permissions"

    - Read (r): This allows a user or a group to view a file (and so also to copy it).
    - Write (w): This permits the user to write or modify a file or directory.
    - Execute (x): A user or a group with execute permissions can execute a file. They can also view a subdirectory.

The permissions for a file, directory, or symbolic link has 10 "bits" and looks similar to this:

![Permissions](images/permissions.png){: style="width: 400px}

As shown, the first bit can be "-" (a file), "d" (a directory), or "l" (a link).

The following group of 3 bits are for the owner, then the next 3 for the group, and then the last 3 for all users. Each can have the r(ead), w(rite), and (e)x(ecute) permission set.

!!! Note "To change permissions, here are some examples"

    - owner (user)
        - **chmod u+rwx FILE/DIR** to add all permissions of a file with name FILE or a directory with name DIR
        - **chmod u-rwx FILE/DIR** to remove all permissions from a file with name FILE or a directory with name DIR
        - **chmod u+x FILE** to add executable permissions
        - **chmod u-wx FILE** to remove write and executable permissions
    - group
        - **chmod g+rwx FILE** to add all permissions to FILE
        - **chmod g-rwx FILE** to remove all permissions to FILE
        - **chmod g+wx FILE** to give write and execute permissions to FILE
        - **chmod g-x FILE** to remove execute permissions to FILE
    - others
        - **chmod o+rwx FILE** to add all permissions to FILE
        - **chmod o-rwx FILE** to remove all permissions to FILE
        - **chmod o+w FILE** to add write permissions to FILE
        - **chmod o-rwx DIR** to remove all permissions to DIR
    - all
        - **chmod ugo+rwx FILE/DIR** to add all permissions for all users (owner, group, others) to file named FILE or directory named DIR
        - **chmod a=rwx FILE/DIR** same as above
        - **chmod a=r DIR** give read permissions to all for DIR

!!! Note

    It is also possible to change the ownership of a file or a directory. We are not going to cover this here, but you can read about the command <code>chown</code> and how to use it in the "[More commands](../more-commands)" section under EXTRAS.

## More scripting 

Scripting is used to perform complex or repetitive tasks without user intervention.  All Linux commands can be used in a script including wild cards. 

!!! NOTE

    If it is just a one-line command you want to do again and again, then ['alias'](../more-commands#alias) is more suited for this. 

We go back to our example script ``my_first.sh``.  There is a second file named ``file2.dat`` which also needs to be processed by the script.   We could open an editor, change the contents of ``my_first.sh`` and re-run it.   This is not really convenient.  To create an improved script copy your script

```bash
$ cp my_first.sh count_ABCD.sh
```
and open the file ``count_ABCD.sh`` in an editor.  Change the argument of ``grep`` from ``file.dat`` to ``$1``

```bash
#!/bin/bash
grep 'ABCD' $1 > file_filtered.dat 
wc -l < file_filtered.dat 
``` 

Check that ``count_ABCD.sh`` has executable permissions and executed the script as follows:

```bash
$ ./count_ABCD.sh file.dat
```

This should give the same result of 2 as before.   When running the script ``count_ABCD.sh`` the ``$1`` gets replaced with the first argument you write after the name of the script. The file ``file2.dat`` can now be processed without changing the script:

```bash
$ ./count_ABCD.sh file2.dat
```
You should get 3 for the result.    We now might want to upgrade that we can search for another string than "ABCD".  

We copy
```bash
$ cp count_ABCD.sh count_string.sh
```
 and edit ``count_string.sh`` to become:

```bash
#!/bin/bash
grep $2 $1 > file_filtered.dat 
wc -l < file_filtered.dat 
``` 

We can now search for 'ABCD' in both files:

```bash
$ ./count_string.sh file.dat ABCD
    2
$ ./count_string.sh file2.dat ABCD
    3
```

alternatively you can search for the word 'line' by changing the input at the prompt

```bash
$ ./count_string.sh file.dat line
    1
$ ./count_string.sh file2.dat line
    3
```

## Commenting

It is useful to write comments into your script, to make their actions more understandable when e.g. you need to understand them in the future or want to share the with someone else.

!!! Note

    Bash treats lines starting with a ``#`` as a comment.
    
Obviously this excludes the shebang in the first line of the script.

Open ``count_string.sh`` in an editor and add comments

!!! Example "Commented version of count_string.sh"

    ```bash
    #!/bin/bash
    # return number of lines in a file containing a string
    # usage: ./count_string file_name string
    
    # search for lines with the string in the file
    grep $2 $1 > file_filtered.dat 

    # count the number of lines
    wc -l < file_filtered.dat 
    ``` 


## More advanced examples


!!! Example "Execute a command on the output of find"

    This example script ``imagefind.sh`` will find all files with the extention ``.png`` in ``$HOME/exercises/script/image`` and then copy them to a directory named ``myimages``. <br> 
    Then it searches for files with ``er`` as part of the name and redirects the output to a file named ``someimagesfiles.txt`` 

    ```bash
    #!/bin/bash
    find $HOME/exercises/script/image -type f -name "*.png" -exec cp {} myimages \; 
    find myimages -type f -name "*er*" > someimagesfiles.txt
    ``` 

!!! Example "Execute a command on output of find and loop over output files" 

    This example script will find all files with extension ``.eps`` in the current directory (and below) and then copy them to the directory ``figures``. <br> 
    Afterwards it creates a variable FIGFILES that contains the full path to the directory with the figures, and all the files in it. <br> 
    Then follows a loop over all files. <br> 
    Inside the loop we convert ``.eps`` files to ``.pdf`` files. The extra line before is just a way to avoid the newly created ``.pdf`` files ends up with extension ``.eps.pdf``.  

    ```bash 
    #!/bin/bash
    find . -type f -name "*.eps" -exec cp {} $HOME/figures \;
    FIGFILES="$HOME/figures/*"
    for f in $FIGFILES
    do
        g=${f%.*}
        ps2pdf -DEPSCrop "$f" "$g.pdf"
    done 
    ```


For more examples of (more useful) scripts, see for instance this <a href=https://www.hostinger.com/tutorials/bash-script-example" target="_blank">list of 25 Easy Bash Script Examples</a>. 

!!! note "Keypoints" 

    - You change permissions for files and directories with ``chmod``   
    - Scripting is used to perform complex or repetitive tasks without user intervention. All Linux commands can be used in a script including wild cards. 


# Modifying the file tree 

!!! note "Learning objectives"

    **Questions**

    - How do I create or remove files and directories?
    - How do I copy or rename files and directories? (You will see why these two operations are mentioned together shortly.)

    **Learning objectives**

    - Learn how to create and remove files and directories.
    - Learn how to copy and rename/move files and directories.
    - Learn to avoid a few common pitfalls that could cause files to be deleted or overwritten by mistake.

## Create and remove directories/files 

This section will show how to work with files and directories through the command line interface (CLI).

### Directories 

- **mkdir DIR**: Creates a directory DIR
    - **mkdir -p DIR/SUBDIR**: creates a directory DIR with the subdirectory SUBDIR
- **rm -r DIR**: Removes a directory DIR. The flag "-r" means recursively
    - You can also add "-f". This means ignore nonexistent files and arguments, and never prompt. 
    - You can add the option "-i". This means it will prompt before every removal. 

!!! example "Examples: creating and removing directories"

    Create a directory called ``mynewdir``

    ```bash
    mkdir mynewdir
    ```

    Create a directory called ``cooldir`` which has a subdirectory called ``fancydir``

    ```bash
    mkdir -p cooldir/fancydir
    ```

    Remove the directory ``mynewdir``

    ```bash
    rm -r mynewdir
    ```

### Files 

To create files, you would normally use an editor (``nano``, ``vim``, ``emacs``, etc.), but it is also possible to create an empty file with the command ``touch``.

```bash 
touch FILE
```

(The `touch` command is more often used to update the timestamps (specifically the latest access and modification times) of existing files.)

You can remove files with ``rm``. Again, you can use the flag/option ``-i`` to prompt before removing a file. Be aware that files removed with ``rm`` are deleted *permanently*---they generally cannot be restored (people have gotten lucky with system backup snapshots, but do not assume that those will be available).

!!! warning

    If you do not add the flag/option "-i" the file will be deleted without prompting. Be careful!

    Be **extra** careful using `rm -rf` with glob patterns (see [Wild Cards under The File System](../filesystem/#wild__cards) )! It is strongly recommended that you always test a pattern with `ls` and check that the output is what you expect before using `rm -rf` on that pattern.
    
!!! example "Examples"

    Create a file called ``file.txt``

    ```bash
    touch file.txt
    ```

    Remove the file ``file.txt``

    ```bash
    rm file.txt
    ```
    
### Examples

???+ faq "Reminder"

     - **mkdir DIR**: Create a directory DIR
     - **rm -rf DIR**: Remove a directory DIR. The flag "-r" means recursively and "-f" means do so without asking for each file and subdirectory. Useful, but dangerous. Be careful!
     - **cd**: Go to your home directory ($HOME)
     - **cd DIR**: Change directory to DIR
     - **cd ..**: Change directory to the parent directory of the current directory
     - **cd -**: go back to the previous working directory
     - **touch FILE**: create an empty file with the name FILE
     - **rm FILE**: remove the file with the name FILE
     - The command `pwd` tells you the current directory path.

!!! example "Creating directories, changing directories, removing directory and file, removing files by pattern"

    This example sequence will demonstrate some of the things we just learned, as well as the command `cd` and glob patterns from the previous section. 

    **HINT: Code-along!**

    ```bash
    [x_rebpi@tetralith1 ~]$ mkdir mytestdir
    [x_rebpi@tetralith1 ~]$ cd mytestdir/
    [x_rebpi@tetralith1 mytestdir]$ mkdir testdir1
    [x_rebpi@tetralith1 mytestdir]$ mkdir testdir2
    [x_rebpi@tetralith1 mytestdir]$ mkdir testdir3
    [x_rebpi@tetralith1 mytestdir]$ rm -rf testdir3
    [x_rebpi@tetralith1 mytestdir]$ cd testdir1
    [x_rebpi@tetralith1 testdir1]$ touch file1.txt
    [x_rebpi@tetralith1 testdir1]$ touch file2.sh
    [x_rebpi@tetralith1 testdir1]$ touch file3.c
    [x_rebpi@tetralith1 testdir1]$ touch file4.dat
    [x_rebpi@tetralith1 testdir1]$ touch file5.txt
    [x_rebpi@tetralith1 testdir1]$ rm file5.txt
    [x_rebpi@tetralith1 testdir1]$
    [x_rebpi@tetralith1 testdir1]$ cd ..
    [x_rebpi@tetralith1 mytestdir]$ cd testdir2/
    [x_rebpi@tetralith1 testdir2]$ touch meow.txt
    [x_rebpi@tetralith1 testdir2]$ touch catsmeow1.txt
    [x_rebpi@tetralith1 testdir2]$ touch homeowners_assoc.txt
    [x_rebpi@tetralith1 testdir2]$ ls *meow*.txt
    [x_rebpi@tetralith1 testdir2]$ rm -r *meow{,1}.txt
    
    ```

!!! Note

    This was done on Tetralith. You will notice that only the current (subdir) is shown in the prompt. At some other centres **all** the (sub)dirs would be shown.

    Example: HPC2N

    ```bash
    b-an01 [~]$ cd mytestdir
    b-an01 [~/mytestdir]$ cd testdir1
    b-an01 [~/mytestdir/testdir1]$
    ```

## cp - copy files/directories

This command is used to copy files or directories.

- **cp myfile.txt DIR/**: copy the file "myfile.txt" to the directory DIR
- **cp DIR1/ DIR2/**: copy the directory DIR1 into the directory DIR2 (Note: overwrites existing files with same name)
- **cp -R DIR1/ DIR2/**: copy the directory DIR1 and all subdirectories into the directory DIR2. 
- **cp -i file.txt DIR/**: Interactive. It will ask before overwriting if there is a file with the same name. 

!!! warning 

    If you do not add the option "-i", you risk overwriting any existing file with the same name. 

!!! example "Code-along"

    Go to the directory ``mytestdir`` under ``exercises`` directory that you got from the downloaded tarball. This is how the structure looks:

    ![folders of exercises directory structure](images/exercises-folders.png){: style="width: 500px;float: left"}
    <br><br style="clear: both;">

    1. Change to the subdirectory:

       ```bash
       cd exercises
       cd mytestdir
       ```
    2. Copy the file ``myfile.txt`` to the subdirectory ``testdir1``:

       ```bash
       cp myfile.txt testdir1
       ```
    3. Create a new directory called ``testdir3`` inside ``testdir1``

       ```bash
       cd testdir1
       mkdir testdir3
       ```
    4. Copy the new subdirectory ``testdir3`` to the directory ``testdir2``. Remember, "testdir2" is located outside "testdir1" and at the same "level". This can be done in more than one way. Remember you need the option ``-r`` (for recursive) when copying directories:
        a) "Go up one" and then copy:
           ```bash
           cd ..
           cp -r testdir1/testdir3 testdir2/
           ```
        b) Copy will standing inside ``testdir1``
           ```bash
           cp -r testdir3 ../testdir2
           ```
    5. If you give the full path while copying, this can be done from anywhere.

## mv - rename files/directories

The command <code>mv</code> is used to rename files and directories, and to **move** a file or directory to another location.

- **mv file1.txt file2.txt**: renames <code>file1.txt</code> to <code>file2.txt</code>
- **mv DIR1/ DIR2/**: renames directory <code>DIR1</code> to directory <code>DIR2/</code>
- **mv file1.txt DIR1/**: moves the file <code>file1.txt</code> into the directory <code>DIR1/</code>
- **mv DIR1 DIR2/**: (note lack of forward slash after <code>DIR1</code>) moves directory <code>DIR1</code> into directory <code>DIR2/</code>.
- **mv -i file1.txt file2.txt**: interactive. Asks before overwriting if there is already a file with the destination name.
- **mv -i DIR1/ DIR2/**: interactive. Asks before overwriting, if there is already a directory with that name.

!!! tip

    <code>mv</code> complains if there is already a file/directory with the new name. You can force the renaming with "-f" at the cost of the disappearence of the file that previously held the name.

### Exercise 

!!! example "Exercise"

    1. Create three files (touch)
    2. Create a directory and then create a subdirectory of that directory (mkdir, cd)
    3. Create a file in the subdirectory (touch)
    4. Create another file inside the directory you created and then move it to the subdirectory you created (touch, cd, mv)
    5. Rename one of the directories (mv)
    6. Delete/remove a file (rm)
    7. Delete/remove the subdirectory (rm)

??? note "Solution - click to reveal"

    1. I randomly name the files ``afile.txt``, ``bfile.txt``, ``cfile.txt``
    
       ```bash
       touch afile.txt
       touch bfile.txt
       touch cfile.txt
       ```
    2. I make the directory ``newdir`` and the subdirectory ``subdir``

       ```bash 
       mkdir newdir
       cd newdir
       mkdir subdir
       ```
    3. I create a file named ``newfile.dat``

       ```bash
       cd subdir
       touch newfile.dat
       ```
    4. I name the file ``secondfile.txt`` and move it into ``subdir``

       ```bash
       cd ..
       touch secondfile.txt
       mv secondfile.txt subdir
       ```
    5. I rename the first directory (top-level directory) I created, calling it ``fancydir``

       ```bash
       cd ..
       mv newdir fancydir
       ```
    6. I remove the file ``afile.txt`` while working in the directory outside of ``fancydir`` (previously called ``newdir``)

       ```bash
       rm fancydir/afile.txt
       ```
    7. I remove the subdirectory ``subdir`` while outside the directory ``fancydir``

       ```bash
       rm -r fancydir/subdir
       ```

!!! tip

    You can always check with ``pwd`` which directory you are working in!

## Symbolic links

A symbolic link is a pointer to another file or directory. Symbolic links are also called soft links, or just symlinks.

Symlinks are useful both for ease---you avoid using a long path each time you change to a directory, like your project directory---and to avoid changing hard links within other scripts or programs. It is good to avoid changing hardlinks if you, for instance, install a program or use a script that assumes the library it uses is called ``libcoolness.a`` and not ``libcoolness.2.0.a``. You can then just update the symlink instead of renaming the library or updating potentially many instances where it is mentioned in the program.

Command:

<div>
```bash
ln -s real-file-or-lib link-name
```
</div>

!!! example "Example (on Tetralith)"

    ```bash
    ln -s /proj/linux-intro/users/MYUSERNAME $HOME/myproj
    ```

    This creates a symbolic link named "myproj" in your home directory, pointing to the location /proj/linux-intro/users/MYUSERNAME. The directory "linux-intro" is the project storage directory for this course project. For user ``x_rebpi``, it would look like this:

    ```bash
    [x_rebpi@tetralith1 ~]$ ls -l
    total 2
    lrwxrwxrwx 1 x_rebpi x_rebpi   31 Sep 11 12:01 myproj -> /proj/linux-intro/users/x_rebpi
    drwxrwxr-x 4 x_rebpi x_rebpi 4096 Sep 11 11:43 mytestdir
    ```

!!! summary

    - You can create a directory named DIR with ``mkdir DIR``
    - You can remove a directory named DIR with ``rm -r DIR``
    - You can create an (empty) file named FILE with ``touch FILE``
    - You can remove a file named FILE with ``rm FILE``
    - The command to copy files and directories is ``cp``
    - The command to rename files and directories is ``mv``
    - Symbolic links are pointers to another file or directory
    - Always test glob patterns with ``ls`` before using the same patterns with ``rm -r`` to remove files in bulk.


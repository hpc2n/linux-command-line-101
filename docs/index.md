# Welcome to the course: Linux command line 101

!!! note "This material"
   
    Here you will find the content of the workshop "Command line 101".
   
    - Documentation about Linux at some of the Swedish HPC centres 
        - HPC2N: <a href="https://docs.hpc2n.umu.se/tutorials/linuxguide/" target="_blank">https://docs.hpc2n.umu.se/tutorials/linuxguide/</a>
        - UPPMAX: <a href="https://docs.uppmax.uu.se/getting_started/linux/" target="_blank">https://docs.uppmax.uu.se/getting_started/linux/</a>
        - LUNARC: <a href="https://lunarc-documentation.readthedocs.io/en/latest/guides/linux/linux_basics_intro/" target="_blank">https://lunarc-documentation.readthedocs.io/en/latest/guides/linux/linux_basics_intro/</a>
        - PDC: <a href="https://support.pdc.kth.se/doc/support-docs/basics/introduction/#basic-linux-for-new-hpc-users" target="_blank">https://support.pdc.kth.se/doc/support-docs/basics/introduction/#basic-linux-for-new-hpc-users</a> 
    - Documentation from Software Carpentry: <a href="https://swcarpentry.github.io/shell-novice/" target="_blank">https://swcarpentry.github.io/shell-novice/</a> 

!!! note "Prerequisites"

    - You need access to a Linux system. 
    - You will use your own computer or any other computer (including computing access at computing centers) you have access to and that runs Linux. 
    - The course project will be on Tetralith, for those that **do not have other access to a computer that runs Linux**.  
        - For those using Tetralith, there is a <a href="https://www.nsc.liu.se/support/getting-started/" target="_blank">Get started guide for NSC here</a>. 

!!! note "Learning outcome"

    - This NAISS course aims to give a brief, but comprehensive introduction to the Linux operating system.

    - What is Linux and why should I use it?
    - You will learn about
       - the command line interface (CLI)
       - navigating and modifying the file tree 
           - ls
           - mkdir
           - cd
           - mv
       - editors on the Linux system 
       - pipes, sorting, filters
           - redirection
           - pipes
           - etc. 
       - patterns
       - scripting
       - some handy hints and tricks 

    - This course will consist of lectures and type-alongs, as well as a few exercises where you get to try out what you have just learned.    

- This is the fourth instance of this course, and it has been somewhat reworked based on previous participant input. We would be grateful if you will fill the evaluation survey so we can further improve the course: <a href="https://forms.office.com/e/8UuxePqVci" target="_blank">https://forms.office.com/e/8UuxePqVci</a> 

!!! admonition "Cluster-specific approaches"

    The course is given by HPC2N (Kebnekaise), but will be done under NAISS on the NAISS system "Tetralith". There is a <a href="https://www.nsc.liu.se/support/getting-started/" target="_blank">Get started guide for NSC here</a>.   

    - The login node for Tetralith is ``tetralith.nsc.liu.se``.
    - It looks like this when I (``x_birbr`` on "Tetralith") login the first time from my computer "defiant":
    ```bash
    bbrydsoe@defiant:~$ ssh x_bibr@tetralith.nsc.liu.se
    The authenticity of host 'tetralith.nsc.liu.se (2001:6b0:17:140::1:10)' can't be established.
    ECDSA key fingerprint is SHA256:dwFmOFzy59e+OdZmMLAW3fj+GeMGACYwjPgc7LKZgSU.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added 'tetralith.nsc.liu.se,2001:6b0:17:140::1:10' (ECDSA) to the list of known hosts.
    Password:
    Verification code:
    ```
    - The verification code it asks about is a 2FA that you need to set. See here: <a href="https://www.nsc.liu.se/support/2fa/" target="_blank">https://www.nsc.liu.se/support/2fa/</a>.
    - You will probably not need it for the course, but the compute project ID is: naiss2025-22-934 
    - The project storage for the course project is in ``/proj/courses-fall-2025/users/YOUR-USERNAME`` 
        - Example, for the user ``x_birbr``, this would be: ``/proj/courses-fall-2025/users/x_birbr``

## Important info

- There is an "important info" page for this course, containing info on the course project, login info for Tetralith, etc. It can be found here: <a href="https://umeauniversity.sharepoint.com/:w:/s/HPC2N630/EdrR1siiThVNpuXKoSZXSeMBIZU71joLKZ-bf4sykjk0aA" target="_blank">https://umeauniversity.sharepoint.com/:w:/s/HPC2N630/EdrR1siiThVNpuXKoSZXSeMBIZU71joLKZ-bf4sykjk0aA</a>
- There is a Q/A page for use during the lectures. Since the lectures are recorded, you may get recorded if you ask questions in the Zoom, but you can always write questions on the Q/A and get answers there. It also has the advantage that you can go back and look at the answers later. The Q/A page can be found here: <a href="https://umeauniversity.sharepoint.com/:w:/s/HPC2N630/EccgkyKcHzhFqMVCq50yyA8BqZUF5Bre8r1bw_koAU4dvw" target="_blank">https://umeauniversity.sharepoint.com/:w:/s/HPC2N630/EccgkyKcHzhFqMVCq50yyA8BqZUF5Bre8r1bw_koAU4dvw</a> 

## Preliminary schedule

| Time | Topic | Activity | Teacher |
| ---- | ----- | -------- | ------- | 
| 9:00 | Welcome+Syllabus | | Joachim | 
| 9:10 | What is Linux? <br>Why should you use it? | Lecture | Joachim | 
| 9:20 | The command line (CLI) | Lecture+code along | Sahar |
| 9:30 | Navigating the File System | Lecture+code along+exercise | Sahar |
| 10:00 | Modifying the file tree | Lecture+code along+exercise | Sahar | 
| 10:25 | BREAK | | |
| 10:40 | Editors | Lecture+code along | Pedro | 
| 10:50 | Piping and filters | Lecture+code along+exercise | Pedro |
| 11:10 | Finding patterns | Lecture+code along+exercises | Pedro | 
| 11:25 | Scripting | Lecture+code along | Pedro | 
| 11:40 | Hints and tricks | Lecture+code along | Joachim |
| 11:50 | Summary   | | Joachim |
| 12:00 | END of course | | | 

## Preparations 

In order to type along and do the exercises, please prepare your course environment now: 

1. Login to the system you are using (Tetralith, your own computer, other system)
2. Create a directory to work in (``mkdir intro-linux``) and then switch to it (``cd intro-linux``)  
    - **NOTE** If you are working on Tetralith, first switch to your working directory: ``cd /proj/courses-fall-2025/users/YOUR-USERNAME``
3. Download the exercises with ``wget https://github.com/hpc2n/linux-command-line-101/raw/refs/heads/main/exercises.tar.gz`` 
4. Extract the exercises with ``tar zxvf exercises.tar.gz``
5. Enter the directory that was created: ``cd exercises``

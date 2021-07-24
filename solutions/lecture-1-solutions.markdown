---
layout: page
title: "Lecture 1 - The Shell"
nav_order: 2
permalink: /lecture-1-the-shell/
---
# Lecture 1 - Course overview + the shell
\
[View lecture](https://www.youtube.com/watch?v=Z56Jmr9Z34Q){: .btn .mr-2 }
[View lecture notes](https://missing.csail.mit.edu/2020/course-shell/){: .btn }

## Exercises
{: .fs-6}
---
1.  For this course, you need to be using a Unix shell like Bash or ZSH. If you
    are on Linux or macOS, you don't have to do anything special. If you are on
    Windows, you need to make sure you are not running cmd.exe or PowerShell;
    you can use [Windows Subsystem for
    Linux](https://docs.microsoft.com/en-us/windows/wsl/) or a Linux virtual
    machine to use Unix-style command-line tools. To make sure you're running
    an appropriate shell, you can try the command `echo $SHELL`. If it says
    something like `/bin/bash` or `/usr/bin/zsh`, that means you're running the
    right program.
    {: .fw-500 }

    As mentioned ealier I am using zsh in Ubuntu-20.04 using WSL2 on a Windows 10 machine.
    `echo $SHELL` gives me this output `/usr/bin/zsh`. If you are using bash you'll get the following output `/usr/bin/bash`.

1.  Create a new directory called `missing` under `/tmp`.
    {: .fw-500 }


    ```shell
    mkdir /tmp/missing
    ```

1.  Look up the `touch` program. The `man` program is your friend.
    {: .fw-500 }

    ```shell
    man touch 
    ```

1.  Use `touch` to create a new file called `semester` in `missing`.
    {: .fw-500 }

     ```shell
    touch /tmp/missing/semester
    ```



1.  Write the following into that file, one line at a time:
    {: .fw-500 }
    ```
    #!/bin/sh
    curl --head --silent https://missing.csail.mit.edu
    ```
    The first line might be tricky to get working. It's helpful to know that
    `#` starts a comment in Bash, and `!` has a special meaning even within
    double-quoted (`"`) strings. Bash treats single-quoted strings (`'`)
    differently: they will do the trick in this case. See the Bash
    [quoting](https://www.gnu.org/software/bash/manual/html_node/Quoting.html)
    manual page for more information.
    {: .fw-500 }

    ```shell
    echo '#!/bin/sh' > semester ; echo 'curl --head --silent https://missing.csail.mit.edu' >> semester
    ```
    `echo '#!/bin/sh' > semester` writes the first line as a literal string to `semester` as we are using single quotes. Double quotes are special in bash/zsh. They are used for variable expansion and other things.\
    `;` is used to string together multiple commands such that they are executed sequentially from left to right.\
    `echo 'curl --head --silent https://missing.csail.mit.edu' >> semester` appends the 2nd line to the 1st one in the file. Notice the `>>` operator.

1.  Try to execute the file, i.e. type the path to the script (`./semester`)
    into your shell and press enter. Understand why it doesn't work by
    consulting the output of `ls` (hint: look at the permission bits of the
    file).
    {: .fw-500 }

    `ls -l` will show all the files in the current directory along with permission details for the user, owing group and others. The `semester` file created by us only has read/write permissions. We don't have execute permissions.

 1. Run the command by explicitly starting the `sh` interpreter, and giving it
    the file `semester` as the first argument, i.e. `sh semester`. Why does
    this work, while `./semester` didn't?
    {: .fw-500 }

    The explanation from a [similar question on Stackoverflow](https://stackoverflow.com/questions/2468132/whats-the-difference-between-running-a-shell-script-as-script-sh-and-sh-script) is as follows:
    
    *Running it as ./script.sh will make the kernel read the first line (the shebang), and then invoke bash to interpret the script. Running it as sh script.sh uses whatever shell your system defaults sh to (on Ubuntu this is bash, which is sh-compatible, but doesn't support some of the extra features of Bash).*

    Check out the link for more details.

1. Look up the `chmod` program (e.g. use `man chmod`).
    {: .fw-500 }

     ```shell
    man chmod
    ```

 1. Use `chmod` to make it possible to run the command `./semester` rather than
    having to type `sh semester`. How does your shell know that the file is
    supposed to be interpreted using `sh`? See this page on the
    [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) line for more
    information.
    {: .fw-500 }

      ```shell
    chmod  +x semester
    ```
    This gives execute permissions to the user, group and others. If you want to restrict execute permissions to say only to the user/owner of the file use `chmod u+x`. Alternatively, you can replace `u` with `g` (group) or `o` (other) depending on your use-case.

    For the second part of the question the wikipedia link mentioned above says the following:

    *When a text file with a shebang is used as if it is an executable in a Unix-like operating system, the program loader mechanism parses the rest of the file's initial line as an interpreter directive.*

1. Use `|` and `>` to write the "last modified" date output by
    `semester` into a file called `last-modified.txt` in your home
    directory.
    {: .fw-500 }

    ```shell
    ./semester | grep "last-modified" > ~/last-modified.txt
    ```
    The STDOUT we get with `./semester` is piped through grep which tries to match the `"last modified"` substring. Once it gets the match the shell takes that line and writes it to the `last-modified.txt` file located in the home directory.

 1. Write a command that reads out your laptop battery's power level or your
    desktop machine's CPU temperature from `/sys`. Note: if you're a macOS
    user, your OS doesn't have sysfs, so you can skip this exercise.
    {: .fw-500 }

    Functionality not available with WSL.
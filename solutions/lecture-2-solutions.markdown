---
layout: page
title: "Lecture 2 - Shell Tools and Scripting"
nav_order: 3
permalink: /lecture-2-shell-tools-and-scripting/
---
# Lecture 2 - Shell Tools and Scripting
{: .fs-7 }
\
[View lecture](https://www.youtube.com/watch?v=kgII-YWo3Zw&feature=emb_imp_woyt){: .btn .mr-2 }
[View lecture notes](https://missing.csail.mit.edu/2020/shell-tools/){: .btn }

## Exercises
{: .fs-6}
---

1. Read [`man ls`](https://www.man7.org/linux/man-pages/man1/ls.1.html) and write an `ls` command that lists files in the following manner
    {: .fw-500 }

    - Includes all files, including hidden files
    - Sizes are listed in human readable format (e.g. 454M instead of 454279954)
    - Files are ordered by recency
    - Output is colorized
    {: .fw-500 }
    

    A sample output would look like this
    {: .fw-500 }

    ```shell
    -rw-r--r--   1 user group 1.1M Jan 14 09:53 baz
    drwxr-xr-x   5 user group  160 Jan 14 09:53 .
    -rw-r--r--   1 user group  514 Jan 14 06:42 bar
    -rw-r--r--   1 user group 106M Jan 13 12:12 foo
    drwx------+ 47 user group 1.5K Jan 12 18:08 ..
    ```

    ```shell
    ls -l -a -h -t --color
    ```
    `ls` lists all directories and files in the current folder. `-l` flag lists everything in a 'long' format. `-a` flag ensures that entries starting with `.` which are hidden are also shown. `-h` prints sizes in human readable format eg. 10K, 100M, 1.5G etc. `-t` enables the result to be sorted by modification time with newest first and finally `--color` colorizes the output.

1.  Write bash functions  `marco` and `polo` that do the following.
    Whenever you execute `marco` the current working directory should be saved in some manner, then when you execute `polo`, no matter what directory you are in, `polo` should `cd` you back to the directory where you executed `marco`.
    For ease of debugging you can write the code in a file `marco.sh` and (re)load the definitions to your shell by executing `source marco.sh`.
    {: .fw-500 }

    ```shell
    # marco.sh
    marco() {
        export CURR_DIR=$(pwd)
    }

    polo() {
        cd "$CURR_DIR"
    }
    ```
    `marco` saves the current directory in a variable called `CURR_DIR`. Then using the `export` command the `CURR_DIR` variable is set as an environment variable. Therefore, it can be accessed later on when required.

    Now when`polo` is executed it uses this environment variable to `cd` into the saved directory.

1. Say you have a command that fails rarely. In order to debug it you need to capture its
    output but it can be time consuming to get a failure run. Write a bash script that runs the following script until it fails and captures its standard output and error streams to files and prints everything at the end. Bonus points if you can also report how many runs it took for the script to fail.
    {: .fw-500 }

    ```bash
    # script.sh
    #!/usr/bin/env bash

    n=$(( RANDOM % 100 ))

    if [[ n -eq 42 ]]; then
       echo "Something went wrong"
       >&2 echo "The error was using magic numbers"
       exit 1
    fi

    echo "Everything went according to plan"
    ```

    Remember to make `script.sh` executable first by using `chmod +x ./script.sh`. Otherwise `solution.sh` won't work.

    ```shell
    # solution.sh
    #!/usr/bin/env bash

    RUN=0

    until [[ "$?" -ne 0 ]]; do
        RUN=$((RUN+1))
        ./script.sh &> outputstream.txt
    done

    echo "The script failed after $RUN runs"
    cat outputstream.txt
    ```

1. As we covered in the lecture `find`'s `-exec` can be very powerful for performing    operations over the files we are searching for.
    However, what if we want to do something with **all** the files, like creating a zip file?
    As you have seen so far commands will take input from both arguments and STDIN.
    When piping commands, we are connecting STDOUT to STDIN, but some commands like `tar` take inputs from arguments.
    To bridge this disconnect there's the [`xargs`](https://www.man7.org/linux/man-pages/man1/xargs.1.html) command which will execute a command using STDIN as arguments.
    For example `ls | xargs rm` will delete the files in the current directory.
    {: .fw-500 }

    Your task is to write a command that recursively finds all HTML files in the folder and makes a zip with them. Note that your command should work even if the files have spaces (hint: check `-d` flag for `xargs`).
    {: .fw-500 }

    ```shell
    find . -type f -name "*.html" | xargs -d '\n' tar cf compressed.tar.gz
    ```
    `find` will recursively find all the `.html` files in the current directory. We pipe the STDOUT of this command into the `xargs` program. The `-d` flag discards all the `\n`'s we get as part of `find`'s output. This cleaned output is then supplied as STDINPUT to `tar` which compresses all the required files into a zip called `compressed.tar.gz`.

1. (Advanced) Write a command or script to recursively find the most recently modified file in a directory. More generally, can you list all files by recency?
    {: .fw-500 }

    Open to suggestions. I think we can use `find . -type d` to get a list of all sub-directories. Then we can use `ls -l` for each of those sub-directories and append all outputs together in a file and `sort` the time column to get a final list of files sorted by modification time. Can't seem to put to put it together though. Happy if one of you could chip in! &#128516;
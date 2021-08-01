---
layout: page
title: "Lecture 6 - Version Control (Git)"
nav_order: 4
permalink: /lecture-6-version-control-git/
---
# Lecture 6 - Version Control (Git)
{: .fs-7 }
\
[View lecture](https://youtu.be/2sjqTHE0zok){: .btn .mr-2 }
[View lecture notes](https://missing.csail.mit.edu/2020/version-control/){: .btn }

## Exercises
{: .fs-6}
---
1. If you don't have any past experience with Git, either try reading the first
   couple chapters of [Pro Git](https://git-scm.com/book/en/v2) or go through a
   tutorial like [Learn Git Branching](https://learngitbranching.js.org/). As
   you're working through it, relate Git commands to the data model.
   {: .fw-500 }

   Self explanatory. 
   
   Unrelated to the question but this [Git cheatsheet from Atlassian](https://www.atlassian.com/dam/jcr:e7e22f25-bba2-4ef1-a197-53f46b6df4a5/SWTM-2088_Atlassian-Git-Cheatsheet.pdf) might be quite handy for the rest of the questions and in general for life.

1.  Clone the [repository for the class website](https://github.com/missing-semester
    missing-semester).
    {: .fw-500 }
    
    a. Explore the version history by visualizing it as a graph.
    {: .fw-500 }
      
      ```bash
      git log --graph
      ```
      
      `git log` will give a linear history of all the commits. Adding the `--graph` flag prints out a graph to go along with the commits.
      
    b. Who was the last person to modify `README.md`? (Hint: use `git log` with an argument).
    {: .fw-500 }

      ```bash
      git log README.md
      ```

      `git log <filepath>` lists only the commits in which the aforementioned file has been modified.

    c. What was the commit message associated with the last modification to the `collections:` line of `_config.yml`? (Hint: use `git blame` and `git show`).
    {: .fw-500 }

      ```bash
      git blame _config.yml

      git show a88b4eac
      ````
      `git blame` shows what revision and author last modified each line of a file. Here the `collections:` line of the `_config.yml` file contains the sha1hash `a88b4eac`. Hence, on running the subsequent command, that is, `git show a88b4eac` will show the log message associated with that commit. The commit message reads as follows `Redo lectures as a collection`.


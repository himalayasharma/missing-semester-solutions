---
layout: page
title: "Lecture 4 - Data Wrangling"
nav_order: 5
permalink: /lecture-4-data-wrangling/
---
# Lecture 4 - Data Wrangling
{: .fs-7 }
\
[View lecture](https://www.youtube.com/watch?v=sz_dsktIjt4){: .btn .mr-2 }
[View lecture notes](https://missing.csail.mit.edu/2020/data-wrangling/){: .btn }

## Exercises
{: .fs-6}
---
1. Take this [short interactive regex tutorial](https://regexone.com/).
   {: .fw-500}
   
   Self explanatory.

1. Find:
   {: .fw-500 }

	 - The number of words (in `/usr/share/dict/words`) that contain at
	   least three `a`s and don't have a `'s` ending. `sed`'s `y` command, or
	   the `tr` program, may help you with case insensitivity. 
	   {: .fw-500 }

	   ```shell
	   cat /usr/share/dict/words | tr "[:upper:]" "[:lower:]" | grep ".*a.*a.*a.*" | grep "[^('s)]$" | wc -l
	   ```
	   The output of the command above turns out to be `639`. `tr` converts all uppercase letters into lower case. `grep` with `.*a.*a.*a.*` regex will 
	   match 3 or more `a's`. You can have a look at the [regex debugger](https://regex101.com/r/ZTcnFt/1/) to try out other test cases. Similarly, we 
	   `grep` again with the `[^('s)]$` regex.  This will avoid all words by using the `('s)` capture group. `$` marks the end the line which in this 
	   case is also the end of the word. Finally, `wc` will count all lines with these filtered words. 

	 - What are the three most common last two letters of those words? 
	   {: .fw-500 }
	 
	   ```shell
	   cat /usr/share/dict/words | tr "[:upper:]" "[:lower:]" | grep ".*a.*a.*a.*" \
	   | grep "[^('s)]$" | sed -E "s/^.*(..)$/\1/" | sort | uniq -c | sort -nk1,1 | \
	   tail -n3 | awk '{ print $1 }'
	   ```
	   We append extra sub-commands to the previous command. With `sed` we pluck out the last two letters from each word. Then we `sort` the results. Then 
	   we pipe the STDOUT to `uniq -c` which gives back only unique instances of all the lines fed to it along with the count of repititions. Then `sort -n
	   k1,1` sorts the incoming list by the 1st column. To get the three most common last two letters of those words we use the `tail -n3` command. `awk 
	   '{ print $1 }'` strips off the 2nd second column which shows the frequency and prints only the first column. The output of command above is as 
	   follows.
	   ```shell
	    al
	    ia
	    an 
	   ``` 

	 - How many of those two-letter combinations are there? 
	   {: .fw-500 }

	   ```shell
	   cat /usr/share/dict/words | tr "[:upper:]" "[:lower:]" | grep ".*a.*a.*a.*" \
	   | grep "[^('s)]$" | sed -E "s/^.*(..)$/\1/" | sort | uniq -c | sort -nk1,1 | \
	   tail -n3
	   ```
	   Command is same as above. Only the `awk` part is removed in order to print both columns. The output of the command above is as follows:

	   ```shell
	    49 al
	    51 ia
	    101 an 
	   ``` 

1. To do in-place substitution it is quite tempting to do something like
   `sed s/REGEX/SUBSTITUTION/ input.txt > input.txt`. However this is a
   bad idea, why? Is this particular to `sed`? Use `man sed` to find out
   how to accomplish this. 
   {: .fw-500 }
   
   The shell makes the file on the right of the redirection symbol `>` empty before writing the output of the the expression on the left. Hence,
   `sed` scans through an empty file if the above mentioned command is used.

   To achieve the required functionality we can use the `-i` option which allows the replacement to be done inplace in the text file. Hence the
   following command can be used:
   ```shell
   sed -i "s/REGEX/SUBSTITUTION/" input.txt
   ```
4. Find your average, median, and max system boot time over the last ten
   boots. Use `journalctl` on Linux and `log show` on macOS, and look
   for log timestamps near the beginning and end of each boot. On Linux,
   they may look something like:
   {: .fw-500}

   ```
   Logs begin at ...
   ```
   and
   {: .fw-500}
   ```
   systemd[577]: Startup finished in ...
   ```
   On macOS, [look
   for](https://eclecticlight.co/2018/03/21/macos-unified-log-3-finding-your-way/):
   {: .fw-500}
   ```
   === system boot:
   ```
   and
   {: .fw-500}
   ```
   Previous shutdown cause: 5
   ``` 
   Functionality not available on WSL. Will update as soon as I move to a full-fledged Linux system.

1. Look for boot messages that are _not_ shared between your past three
   reboots (see `journalctl`'s `-b` flag). Break this task down into
   multiple steps. First, find a way to get just the logs from the past
   three boots. There may be an applicable flag on the tool you use to
   extract the boot logs, or you can use `sed '0,/STRING/d'` to remove
   all lines previous to one that matches `STRING`. Next, remove any
   parts of the line that _always_ varies (like the timestamp). Then,
   de-duplicate the input lines and keep a count of each one (`uniq` is
   your friend). And finally, eliminate any line whose count is 3 (since
   it _was_ shared among all the boots).
   {: .fw-500}

   Functionality not available on WSL. Will update as soon as I move to a full-fledged Linux system.

6. Find an online data set like [this
   one](https://stats.wikimedia.org/EN/TablesWikipediaZZ.htm), [this
   one](https://ucr.fbi.gov/crime-in-the-u.s/2016/crime-in-the-u.s.-2016/topic-pages/tables/table-1),
   or maybe one [from
   here](https://www.springboard.com/blog/free-public-data-sets-data-science-project/).
   Fetch it using `curl` and extract out just two columns of numerical
   data. If you're fetching HTML data,
   [`pup`](https://github.com/EricChiang/pup) might be helpful. For JSON
   data, try [`jq`](https://stedolan.github.io/jq/). Find the min and
   max of one column in a single command, and the difference of the sum
   of each column in another. 
   {: .fw-500}

   ```shell
   curl -o data.html \
   https://ucr.fbi.gov/crime-in-the-u.s/2016/crime-in-the-u.s.-2016/topic-pages/tables/table-1
   ```

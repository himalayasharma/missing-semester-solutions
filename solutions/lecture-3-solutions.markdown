---
layout: page
title: "Lecture 3 - Editors (Vim)"
nav_order: 4
permalink: /lecture-3-editors-vim/
---
# Lecture 3 - Editors (Vim)
{: .fs-7 }
\
[View lecture](https://www.youtube.com/watch?v=a6Q8Na575qc&list=PLyzOVJj3bHQuloKGG59rS43e29ro7I57J&index=4){: .btn .mr-2 }
[View lecture notes](https://missing.csail.mit.edu/2020/editors/){: .btn }

## Exercises
{: .fs-6}
---
1. Complete `vimtutor`. Note: it looks best in a [80x24](https://en.wikipedia.org/wiki/VT100) (80 columns by 24 lines) terminal window
    {: .fw-500 }

    Type `vimtutor` in the terminal. It will take around 25-30 minutes to get through all the 7 chapters.

    The terminal can be resized by changing your terminal settings accordingly. I have outlined the process for Windows Terminal (which I use) below.

    - Click on the 'Settings' option in dropdown.
    
    ![Click on the 'Settings' option in dropdown](/images/Windows-terminal-1.jpg "Click on the 'Settings' option in dropdown.")

    - Scroll down to the bottom of the 'Startup' tab.

    ![Scroll down to the bottom of the 'Startup' tab](/images/Windows-terminal-2.jpg "Scroll down to the bottom of the 'Startup' tab.")

    - Adjust the number of columns and the number of rows and click on 'Save'.

    ![Adjust the number of columns and the number of rows and click on 'Save'](/images/Windows-terminal-3.jpg "Adjust the number of columns and the number of rows and click on 'Save'.")

    - Close 'Windows Terminal' and restart the application.

1. Download our [basic vimrc](https://missing.csail.mit.edu/2020/files/vimrc) and save it to `~/.vimrc`. Read
   through the well-commented file (using Vim!), and observe how Vim looks and
   behaves slightly differently with the new config.
   {: .fw-500 }

   `wget` is a command line tool that can be used to download files from the web. It supports HTTP, HTTPS and FTP.
   ```shell
   wget https://missing.csail.mit.edu/2020/files/vimrc; mv vimrc ~/.vimrc
   ```
   Then you can go on to read the contents of the `.vimrc` file.
   ```shell
   vim ~/.vimrc
   ```

1. Install and configure a plugin: [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim).
    {: .fw-500 }
   
   1. Create the plugins directory with `mkdir -p ~/.vim/pack/vendor/start`
   1. Download the plugin: `cd ~/.vim/pack/vendor/start; git clone
      https://github.com/ctrlpvim/ctrlp.vim`
   1. Read the
      [documentation](https://github.com/ctrlpvim/ctrlp.vim/blob/master/readme.md)
      for the plugin. Try using CtrlP to locate a file by navigating to a
      project directory, opening Vim, and using the Vim command-line to start
      `:CtrlP`.
    1. Customize CtrlP by adding
       [configuration](https://github.com/ctrlpvim/ctrlp.vim/blob/master/readme.md#basic-options) to your `~/.vimrc` to open CtrlP by pressing Ctrl-P.
    {: .fw-500 }

    Self-explanatory.

1. To practice using Vim, re-do the [Demo](https://missing.csail.mit.edu/2020/editors/#demo) from lecture on your own machine.
    {: .fw-500 }

    Self-explanatory.

1. Use Vim for _all_ your text editing for the next month. Whenever something
   seems inefficient, or when you think "there must be a better way", try
   Googling it, there probably is. If you get stuck, come to office hours or
   send us an email.
   {: .fw-500 }

   Self-explanatory.

1. Configure your other tools to use Vim bindings (see instructions above).
   {: .fw-500 }

    - Shell -
    \
        For `zsh` add the following lines to `~/.zshrc`

        ```shell
        bindkey -v
        export KEYTIMEOUT=1
        ```

        This [video](https://www.youtube.com/watch?v=hIJh-KlQ7io&list=PLG1IUAHj1WhVwqlIgX2EU7ZwflNVJrCJx&index=7&t=82s) talks about how to enable and use Vi mode in both bash/zsh.

    - Browser -
    \
        I am a [Brave](https://brave.com/) user which is based on [Chromium](https://www.chromium.org/Home). For browsers based on [Chromium](https://www.chromium.org/Home) you can simply install the [Vimium](https://chrome.google.com/webstore/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb?hl=en) plugin and adjust settings according to your needs.

1. Further customize your `~/.vimrc` and install more plugins.
   {: .fw-500 }

   Self-explanatory.

1. (Advanced) Convert XML to JSON ([example file](https://missing.csail.mit.edu/2020/files/example-data.xml))
   using Vim macros. Try to do this on your own, but you can look at the
   [macros](https://missing.csail.mit.edu/2020/editors/#macros) section above if you get stuck.
   {: .fw-500 }

   Will be updated soon.





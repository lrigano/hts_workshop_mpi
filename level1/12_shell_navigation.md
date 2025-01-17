# Introducing the shell

* Teaching: 40 minutes
* Exercises: 20 minutes

#### Objectives

* Understand how to navigate your file system using the command line.
* Perform basic file operations using the command line.
* Demonstrate the use of tab completion, and understand its advantages.

#### Key points

* The shell gives you the ability to work more efficiently by using keyboard commands rather than a GUI.
* Useful commands for navigating your file system include: `ls`, `pwd`, and `cd`.
* Tab completion can reduce errors from mistyping and make work more efficient in the shell.

---

## Contents

1. [Navigating your file system](#navigating-your-file-system)
1. [Accessing documentation on the command line](#accessing-documentation-on-the-command-line)
1. [Full versus relative paths](#full-versus-relative-paths)
1. [Navigational shortcuts](#navigational-shortcuts)
1. [Speeding up commands with tab completion](#speeding-up-commands-with-tab-completion)

---

## Navigating your file system

The part of the operating system responsible for managing files and directories is called the **file system**. It organizes our data into files,
which hold information, and directories (also called "folders"), which hold files or other directories. This is **exactly* the same as what you will be used to using the `File Explorer` on your home and work computers, except that we do not have visual prompts to tell us where we are in the file system.

To the left hand side of your terminal cursor is a dollar sign character (`$`). The dollar sign is a **prompt**, which shows us that the shell is waiting for input; your shell may use a different character as a prompt and may add information before the prompt. When typing commands, either from these lessons or from other sources, do not type the prompt, only the commands that follow it.

Let's find out where we are by running a command called `pwd` (which stands for "print working directory"). At any moment, our **current working directory** is our default directory, i.e. the directory that the computer assumes we want to run commands in, unless we explicitly specify something else.

```bash
$ pwd
```

You will see a return line of text, which looks something like the following:

```bash
/home/username
```

This is your home directory. It is private to you, and has limited file storage space. When working on NeSI we typically want to leave our home directory and navigate to a project directory. We will use the `cd` ("change directory") command to swtich our current working directory to a new location in the NeSI file system.

```bash
$ cd /nesi/project/nesi03181/phel/
```

We are now inside a particular folder on the NeSI system, similar to how you navigate folders in the Windows Explorer program on your desktop. Let's now look at how our file system is organised. We can see what files and subdirectories are in this directory by running `ls`,
which stands for "listing":

```bash
$ ls
```

`ls` prints the names of the files and directories in the current directory in alphabetical order, arranged neatly into columns. Identify the folder that corresponds to your user name, then navigate into that folder using the `cd` command. Once inside, use the `ls` command again to view the contents.

```bash
$ cd USERNAME/
$ ls
shell_data
```

We will be working within the `shell_data` subdirectory, and creating new subdirectories, throughout this workshop.  

If we want to now navigate into the `shell_data` folder we must once again call the `cd` command:

```bash
$ cd shell_data/
```

> **NOTE:** It's easy to get lost in a text-based file system. If you ever get stuck and do not know how to get out of your current location, calling either of:
> ```bash
> $ cd ~
> ```
> or
> ```bash
> $ cd
> ```
> Will return you do your **home directory** (`/home/username/`).

Let's look at what is in the `shell_data` directory:

```bash
$ ls
sra_metadata  untrimmed_fastq
```

We can make the `ls` output more comprehensible by using the **flag** `-F`, which tells `ls` to add a trailing `/` to the names of directories:

```bash
$ ls -F
sra_metadata/  untrimmed_fastq/
```

Anything with a `/` after it is a directory. Things with a `*` after them are programs. If there are no decorations, it's a file.

---

## Accessing documentation on the command line

`ls` has lots of other options. To find out what they are, we can type:

```bash
$ man ls
```

`man` (short for manual) displays detailed documentation (also referred as man page or man file) for `bash` commands. It is a powerful resource to explore `bash` commands, understand their usage and flags.

Some manual files are very long. You can scroll through the file using your keyboard's down arrow or use the <kbd>Space</kbd> key to go forward one page and the <kbd>b</kbd> key to go backwards one page. When you are done reading, hit <kbd>q</kbd> to quit.

Alternatively, many tools produce a brief help menu if run in one of the following ways:

```bash
$ ls --help
$ ls -h
```

This help is usually shorter and more concise than what you would get through the `man` command, but often if you're just trying to jog your memory it is sufficient.

---

## Full versus relative paths

As we have previously seen, the `cd` command takes an directory name which you provide, and moves you to that location on the computer file system. Up until this point, we have been specifying our directory changes one folder at a time, but this is not necessary.

Directories can be specified using either a *relative* path or a full *absolute* path. The directories on the computer are arranged into a hierarchy. The full path tells you where a directory is in that hierarchy. Dependending on where you currently are in the file system when you enter the `pwd` command you will see something like:

```bash
$ pwd
/nesi/project/nesi03181/phel/USERNAME/
```

This is the full name of your current directory. Assuming you saw the first output, this tells you that you are in a directory called `username/`, which sits inside a directory called `phel/`, which in turn sits inside a directory `nesi03181/`. At the very top of the hierarchy is a directory called `/` which is usually referred to as the **root directory**.

Return to your home directory, then navigate back to your current location using the following command:

```bash
$ cd ~
$ cd /nesi/project/nesi03181/phel/USERNAME/
```

Now return to your home directory again, and navigate back using the following commands:

```bash
$ cd ~
$ cd /
$ cd nesi/
$ cd project/
$ cd nesi03181/
$ cd phel/
$ cd USERNAME/
```

These two commands have the same effect and take us to the same location. However, the first uses the absolute path, giving the full address from the top of the file system. The second uses a series of relative paths, with the directory specified in each command contingent on the current working directory.

A relative path is like getting directions from someone on the street. They tell you to "go right at the stop sign, and then turn left onto Queen Street". That works great if you're standing there together, but not so well if you're trying to tell someone how to get there from another country. A full path is like GPS coordinates. It tells you exactly where something is no matter where you are right now.

You can use either a full path or a relative path depending on what is most convenient. If we are in the home directory nd want to move into the training folder it is more convenient to enter the full path. If we are already in the this location but want to move to another nearby folder, it may be more convenient to enter the relative path since it involves less typing.

Over time, it will become easier for you to keep a mental note of the structure of the directories that you are using and how to quickly navigate amongst them.

A full path always starts with a `/` (the root directory). A relative path does not. This is a helpful difference to remember so that you always know which type of path you are working with.

When working with relative paths, there is one other thing which is critical to know - how to move up out of a directory. This can be achieved using a special path `../` which means "move one level higher than the current directory. To see this in action, run the follow commands and note output each time to run `pwd` and `ls`.

```bash
$ cd /nesi/project/nesi03181/phel/USERNAME/
$ pwd
$ ls

$ cd ../
$ pwd
$ ls

$ cd USERNAME/
$ pwd
$ ls
```

> **Exercise**
>
> Using the filesystem diagram below, if `pwd` displays `/Users/thing`, what will `ls ../backup` display?
> 1.  `../backup: No such file or directory`
> 2.  `2012-12-01 2013-01-08 2013-01-27`
> 3.  `2012-12-01/ 2013-01-08/ 2013-01-27/`
> 4.  `original pnas_final pnas_sub`
> 
> ![](../img/level1_12_filesystem_challenge.svg)
> 
> <details>
> <summary>Solution</summary>
> 
> 1. No: there *is* a directory `backup/` in `/Users`.
> 2. No: this is the content of `Users/thing/backup`, but with `..` we asked for one level further up.
> 3. No: see previous explanation. Also, we did not specify `-F` to display `/` at the end of the directory names.
> 4. Yes: `../backup` refers to `/Users/backup`.
> 
> </details>

---

## Navigational shortcuts

The root directory is the highest level directory in your file system and contains files that are important for your computer to perform its daily work. While you will be using the root (`/`) at the beginning of your absolute paths, it is important that you avoid working with data in these higher-level directories, as your commands can permanently alter files that the operating system needs to function.

In many cases, including when working on NeSI, trying to run commands in root directories will require special permissions which are not available to you as a regualar user.

Dealing with the home directory is very common. The tilde character, `~`, is a shortcut for your home directory. On a Linux operating system the root directory is **two** levels above our home directory, so `cd` or `cd ~` will take you to `/home/username/` and `cd /` will take you to `/`.

---

## Speeding up commands with tab completion

Typing out file or directory names can waste a lot of time and it's easy to make typing mistakes. Instead we can use **tab complete** as a shortcut. When you start typing out the name of a directory or file, then hit the <kbd>Tab</kbd> key, the shell will try to fill in the rest of the directory or file name.

Return to your working directory:

```bash
$ cd /nesi/project/nesi03181/phel/USERNAME/
```

Then enter:

```bash
$ cd she<tab>
```

The shell will fill in the rest of the directory name for `shell_data`. Move into this directory.

Using tab complete can be very helpful. However, it will only autocomplete a file or directory name if you've typed enough characters to provide a unique identifier for the file or directory you are trying to access.

For example, if we now try to list the files which names start with `SR` by using tab complete:  

```bash
$ ls SR<tab>
```

The shell auto-completes your command to `SRR09`, because all file names in the directory begin with this prefix. Hitting <kbd>Tab</kbd> twice in quick succession will prompt the the shell to list all possible choices.

```bash
$ ls SRR09<tab><tab>
SRR097977.fastq  SRR098026.fastq
```

Tab completion can also fill in the names of programs, which can be useful if you remember only part  of a program name.

```bash
$ pw<tab><tab>
pwck              pwd               pwhistory_helper  pwscore
pwconv            pwdx              pwmake            pwunconv
```

Displays the name of every program that starts with `pw`.

---

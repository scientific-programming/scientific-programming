---
title: "Version Control"
date: 2018-10-25T17:49:03+01:00
draft: false
weight: 20
---

### What is Version Control?

Simply put, it's a way of keeping old versions of your software or documents. If you've ever worked in a business environment, you might be familiar with Microsoft SharePoint, and the concepts of checking in and out documents. This is an example of version control. Here, however, we're going to teach you how to use Git, which is a more general purpose version control software. There are alternatives (Mercurial and SVN), but Git seems to have become particularly popular with the launch of the site GitHub.

### Why is it useful?

![PhD Comic on Versioning of Documents](vc-comic.gif)

1) Open your terminal, or Git Bash.

2) Set your name and username with Git. This labels things you do and
associates them with you!

```bash
git config --global user.name "Ryan Pepper"
git config --global user.email "ryan.pepper@soton.ac.uk"
```

3) Set your favourite text editor by running the appropriate command
below:

```bash
# Atom
git config --global core.editor "atom --wait"
# nano
git config --global core.editor "nano -w"

# Sublime Text (Mac)
git config --global core.editor
"/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl -n
-w"

# Sublime Text
(Win, 64-bit install) git config --global core.editor
"'c:/program files/sublime text 3/sublime_text.exe' -w"

# Notepad++ (Win, 64-bit install)
git config --global core.editor
"'c:/program files/Notepad++/notepad++.exe' -multiInst -notabbar
-nosession -noPlugin"

# Emacs
git config --global core.editor "emacs"

# Vim
git config --global core.editor "vim"
```

4) We're going to create a folder with the command "mkdir", and change into that directory with "cd".

```bash
cd ~
mkdir project
cd project
```
5) Now, we make the folder into a git repository. This means that git will start to keep track
of files created in the folder.

```bash
git init
```

6) The command "ls" shows the directories contents. If we use the command "ls -a" - the "-a" flag means
that we see hidden files, shows us that a new folder called ".git" has been created.

7) We can run

```bash
git status
```

to show that everything has worked correctly. You should see something like:

```bash
 # On branch master
 #
 # Initial commit
 # nothing to commit
 (create/copy files and use "git add" to track)
```

8) Let's create a file; open the text editor you chose earlier, and
save a file called "workshop.txt" in the directory you're in.

Write something in the file:

```text
I'm learning how to use Version Control with Git!
```

and save it.

9) Now, let's try running 'git status' again. What you should see is
that now, changes you've made show up.

```bash
 On branch master

 No commits yet

 Untracked files: (use "git add <file>..." to include in what will be
 committed)

 workshop.txt

 nothing added to commit but untracked files present (use "git add" to
 track)
```

An untracked file is just a file that we haven't told Git to watch in
any way.  To track the file we created, we use the command:

```bash
git add workshop.txt
```

Doing "git status" again:

```bash
On branch master

No commits yet

Changes to be committed: (use "git rm --cached <file>..." to unstage)

  new file: workshop.txt
```

10) Now, we're going to 'commit' our changes - basically, take a
snapshot of them at this particular time.

You have two options

i) Run the command

```bash
git commit
```

This will bring up the text editor you chose earlier. Type a message
about the changes you have made so that the file looks something like
this:

```bash
Added text to workshop.txt
```

Now save the file.

ii) Alternatively, skip opening the text editor with:

git commit -m "Added text to workshop.txt"

11) Now make some more changes - add another line of text to the file
workshop.txt, and commit them again.

12) Now we're going to look at the record we've made so far. Try
runningt the command:

```bash git log ```

What you should see is something like the following:

```bash commit 3ef8ea1e42fc071b8f8121ba80419b9df6f5d983 (HEAD ->
master) Author: Ryan Pepper <ryan.pepper@soton.ac.uk> Date: Wed Oct 24
15:04:12 2018 +0100

    Added more text to workshop.txt

commit dc6b701bcdbff38fa8a9800f8173f88d514090ac Author: Ryan Pepper
<ryan.pepper@soton.ac.uk> Date: Wed Oct 24 14:17:36 2018 +0100

    Add text to workshop.txt ```

Breaking this down - there are two sections, for the two commits
you've made so far, ordered from newest to oldest.

The big long strings are a label for a particular set of changes.
Author and date are self-explanatory, and the text below that is the
message

13) Now, let's say that you need to go back in time and look at how the
file looked some time ago. We could just delete the text, but in more
complicated cases, that's not sufficient. There is an easy way to go
back.

Copy about 10 or so of the first letters and numbers of the commit
that you want to see. Then run the command:

```bash git checkout dc6b701bcdbff ```

You will see some output:

``` Note: checking out 'dc6b701bcdbff38f'.

You are in 'detached HEAD' state. You can look around, make
experimental changes and commit them, and you can discard any commits
you make in this state without impacting any branches by performing
another checkout.

14) If you want to create a new branch to retain commits you create, you
may do so (now or later) by using -b with the checkout command
again. Example:

  git checkout -b <new-branch-name>

HEAD is now at dc6b701 Add text to workshop.txt
```

You're now in a working environment with the old set of changes - if
you open the file again, you can see the latest committed changes have
disappeared. Don't worry! They're safe. You're in something called a
'detached HEAD' state. This is often a source of a lot of confusion
for people new to Git, because if you make commits in this state, they
will get lost.

Now is a good time to introduce the concept of a branch. Branches are
basically a parallel stream of commits that you can work on
seperately, and switch to at any time. The "main" branch - the master
copy of the history is known as the "master" branch. You can have as
many branches as you like in a repository. The main use case is for
fixing bugs or From the detached head state, or any other place, you
can create a branch by running:

```bash
git checkout -b mynewbranch
```

Git checkout is for switching between branches; the "-b" flag creates new ones.

15) From here, we can make changes. Add some more text in the file
workshop.txt and commit the changes.

You can switch back to the original history by running the command:

```bash
git checkout master
```

16) Now you can try and merge the branch into the 'master' branch. To do
this, run the command:

```bash
git merge mybranch
```

However, you may see an error message:

```
Auto-merging workshop.txt
CONFLICT (content): Merge conflict in workshop.txt
Automatic merge failed; fix conflicts and then commit the result.
```

What this means is that Git cannot automatically reconcile the
differences between the version of the file in your new branch, and
the version of the file in your master branch. This is called a 'merge
conflict' That means you manually need to edit the file. Edit the file
and you will see three odd lines with special markers:

```
Hello, we've got a file in here!

<<<<<<< HEAD
Added a line of text on the branch!
=======
Added another line to the file.
>>>>>>> mybranch
```

The "<<<<< HEAD" means that what follows is text on the head of the
current branch - i.e. mynewbranch.

The "=======" acts as a seperator

The ">>>>> master" signals the end of the conflicting changes on the
master branch.

To reconcile, simply delete these three lines, and save the file. Do a
'git add' and then 'git commit'


# Storing your repository somewhere safe

You have a history of your changes locally, but that's not much good
if your hard drive fails.  We'll now show you how keep a history
remotely.

Git is known as a 'distributed version control' system. Generally, you
host a repository somewhere online. There are lots of different
providers for this.

* GitHub - free! Lots of integrations with other services. Limited
number or private repositories, but you can send off proof of academic
status to get an unlimited number.

* GitLab - also free. Unlimited number of private repositories.  Also
allows local hosting - for e.g. in the University of Southampton,
there is a private GitLab instance hosted internally, which can be
used for sensitive projects.

* BitBucket - Has a lot of commercial products that are used in
industry - good issue trackers.

For this exercise, we'll use GitHub, but in practice there is not much
between them.

1) Create an account on github.com

2) Once done, click the "+" arrow in the top right hand corner, and click "New repository"

3) Type in a name and description for your repository:

<img src="drawing.jpg" alt="Image showing repository creation" style="width:300px;"/>

You'll now get a list of commands to type; the ones you want are:

```bash
git remote add origin https://github.com/rpep/mytestrepo.git
git push -u origin master
```

You'll get asked for your username and password for GitHub - enter these.

Now refresh the page, and you'll see the file you had has appeared online!

4) Now - in pairs - one of you go to the Git repository of your neighbour. This will be

https://github.com/their-username/their-repository-name

Click 'Fork'. This will make a copy of their repository on your GitHub.

5) Now, copy their repository to your computer with the command:

```bash
git clone https://github.com/yourusername/their-repository-name.git
```

6) Move into the folder:

```bash
cd their-repository-name
```

And make your own change to the file.

7) Commit it as before:

```bash
git commit -m "Making a change to my partner's repository"
```

8) Now push the change online:

```bash
git push
```

9) Go back to GitHub.

Click "New Pull Request, and then "Create New Pull Request" on the next page.

Add in some information about the changes you made, and then "Create pull request"

10) Now, your partner needs to go back to their version of the repository, and look at
    the tab labelled "Pull Requests"

Scroll to the bottom, and then press "Merge pull request"

---
title: "Discarding Temporary Changes"
date: 2018-10-25T17:49:03+01:00
draft: false
weight: 33
---

### Discarding channges

1) If you make some changes to the file workshop.txt, but then decide that they weren't correct or were unnecessary, you can easily get back to the head of the branch with the following command:

```Bash
git reset HEAD workshop.txt
```
This permanently discards these changes!

{{% panel theme="warning" header="Resetting the whole repository" %}}
If you have multiple files that have been changed, and you want to reset all of them, you can use:

```Bash
git reset --hard HEAD
```
Use with caution!
{{% /panel %}}


2) Alternatively, if you want to hide the changes now, but might come back to them, you can use:

```bash
git stash
```

This creates a list of changes which are stored, but not committed, and which you can recover later. You can stash multiple times. Change your file and then stash it, and then repeat that again a few times.

3) To look at a list of the stashes you've made, just type:

```bash
git stash list
```

4) To recover the most recent set of changes, you can just type

```bash
git stash apply
```

If you want a different set, you can type:

```bash
git stash apply stash@{2}
```

If there is a clash between your current commit and the stashed code,
you will get a merge conflict which you'll need to resolve.

5) If you recover something from a stash, but then decide you don't want it anymore,
you can achieve this by 'unapplying' the stash, using the following command:

```bash
git stash show -p stash@{2}| git apply -R
```

If you don't specify which stash from the list you recovered from, git will
just assume you chose the most recent one.

---
title: "Version Control"
date: 2018-10-25T17:49:03+01:00
draft: false
weight: 30
---

### What is Version Control?

Simply put, it's a way of keeping old versions of your software or documents. If you've ever worked in a business environment, you might be familiar with Microsoft SharePoint, and the concepts of checking in and out documents. This is an example of version control. Here, however, we're going to teach you how to use Git, which is a more general purpose version control software. There are alternatives (Mercurial and SVN), but Git seems to have become particularly popular with the launch of the site GitHub.

### Why is it useful?

![PhD Comic on Versioning of Documents](vc-comic.gif)

The concept of version control is something which people do without thinking about. It's common to keep older versions of documents in general, and the same applies to code. However, using software to do this for code is not very common in academia, and most people end up with situations something like that in the above comic.

Think about how you might behave when you find a bug in your code somewhere. You might know that it didn't previously exist and so an older version of a function was fine. With your code tracked in version control, you can look back at old versions of your code, with notes about what changes were made between versions.

### How is it useful for scientists in particular?

There are a number of really strong arguments for using version control as a scientist. When you run a simulation for example, it is good practice to be able to record the exact version of the code used to generate your results. If you don't do so, and you find at a later date that you can't reproduce your simulation results, you can then go back to the old version and find out why this might be the case.

Version control is useful especially for writing papers when you have multiple collaborators. When this is the case, you can have a master copy of a document written in LaTeX, which every person can work on together. Certain commands let you see which author wrote or edited each line, and so you know exactly who is responsible for particular changes, making it easy to ask for clarification or make suggestions to the right person as necessary.

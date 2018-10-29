---
title: "GitHub and Collaborating"
date: 2018-10-25T17:49:03+01:00
draft: false
weight: 32
---
# Storing your repository somewhere safe

You have a history of your changes locally, but that's not much good
if your hard drive fails.  We'll now show you how keep a history
remotely.

Git is known as a 'distributed version control' system. Generally, you
host a repository somewhere online. There are lots of different
providers for this.

{{% panel theme="info" header="Version Control Websites" %}}
<img src="../github-logo.jpg" alt="GitHub" style="width:200px;"/> [GitHub](https://github.com) - free! Now owned by Microsoft. Lots of integrations with other services. Limited number of private repositories, but you gain [education status](https://education.github.com/) to get an unlimited number.
Probably the widest used, and has best social features because of this.

<img src="../gitlab-logo.jpg" alt="GitLab" style="width:200px;"/>
[GitLab](https://about.gitlab.com/) - also free. Unlimited number of private repositories.  Also
allows local hosting - for e.g. in the University of Southampton,
there is a private GitLab instance hosted internally, which can be
used for sensitive projects.

<img src="../bitbucket-logo.png" alt="BitBucket" style="width:200px;"/>
[BitBucket](https://bitbucket.org/) - Owners Atlassian have a lot of commercial products that are used in
industry such as [JIRA](https://www.atlassian.com/software/jira) which integrate well with this service.
{{% /panel %}}


For this exercise, we'll use GitHub, but in practice there is not much
between them.

1) Create an account on https://www.github.com

2) Once done, click the "+" arrow in the top right hand corner, and click "New repository"

3) Type in a name and description for your repository:

<img src="../Github-new-repo.png" alt="Image showing repository creation" style="width:600px;"/>

Don't touch the other settings yet!

4) You'll now get a page with a list of commands to type; the ones you want are:

```bash
git remote add origin https://github.com/rpep/my-new-repository.git
git push -u origin master
```

the other options are used when you have not yet created a repository on your local machine.

When you run 'git push', you will be asked for your username and password for GitHub - enter these.



Now refresh the page, and you'll see the repository you were working on has appeared online!

### Collaborating - Partner Up

1) Now - in pairs - each go to the Git repository of your neighbour. This will be

https://github.com/their-username/their-repository-name

<img src="../fork.png" width="600px">

Click 'Fork'. This will make a copy of their repository on your GitHub.

5) Now, copy their repository to your computer with the command:

```bash
cd ..
git clone https://github.com/yourusername/their-repository-name.git
```

{{% panel theme="warning" header="Cloning to an alternate folder" %}}
You can only clone a repository like this from GitHub if a folder by the same name doesn't exist in the directory where you are working.
You can get around this via:
```bash
git clone https://github.com/yourusername/their-repository-name.git my-alternate-folder-name
```
{{% /panel %}}

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

10) Now, each of you go back to your own version of the repository, and look at
    the tab labelled "Pull Requests"

Scroll to the bottom, and then press "Merge pull request"

12) Pull these changes to your repository using 'git pull', and your partners changes
will now be on your computer as well.



If you choose to make your code public, there are a number of files that are an absolute must have. These are normally written in [Markdown](https://guides.github.com/features/mastering-markdown/) format (.md).

* A License - A license just describes the terms under which others can use your code.
There are many types of Open Source licence, but common ones for academic projects, the GNU [GPL](https://www.gnu.org/licenses/gpl-3.0.en.html) and [LGPL](https://www.gnu.org/licenses/lgpl-3.0.en.html), [MIT](https://en.wikipedia.org/wiki/MIT_License), [Apache](https://apache.org/licenses/LICENSE-2.0) and [3-clause BSD](https://opensource.org/licenses/BSD-3-Clause) licenses are some common ones.

* A README.

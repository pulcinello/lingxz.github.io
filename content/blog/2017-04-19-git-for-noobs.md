---
title: 'Git for noobs: an attempt at a git tutorial'
tags: [git]
toc: true
draft: true
---

So this is my attempt at making a git tutorial out of the countless git tutorials already out there. Why am I doing this? I remember the time I struggled with git when I started, and I want to challenge myself to write a tutorial that answers all the questions I had and all the questions I didn't think to ask. <!--more-->

I feel that's the frustrating thing about the initial stages of learning something completely new and unrelated to anything you've done before--it is often not that you cannot find answers to your questions, it is that you're struggling to *find the questions to ask*. Sometimes the novelty of something just overwhelms and you're left grasping at straws just trying find its place in your life, and when someone asks you, "What don't you not understand?" and you're just lost for words because it all seems right and it all seems wrong at the same time, but you don't know how to express any of it. It's as if someone put a strange object in your hand and walked away--you can see every part of it, feel every part of it, but you just don't understand--what is it doing here? 

I don't know about you, but that's sometimes how I feel when I learn something completely new (mostly in physics, most recently when I started my final year project, not so recently when I was just learning frontend development). I feel that once you are able to ask clear, pointed questions about something, it already demonstrates a certain level of familiarity with the subject. And I believe a good introductory tutorial, since it cannot and is not meant to cover everything, should point you to the right questions to ask. 

It's not that some of the tutorials are not clear in what they teach. A lot of tutorials meticulously teach you how to work with git, but personally I need a super rough, high-level conceptual understanding of the thing before I can start looking at its details. 

So this is a git tutorial tailored for the past me. I don't pretend I represent the what the general population thinks, but hopefully it helps a few other people. It will aim to give a high-level overview of sorts in as layman terms as possible before going through each set of common commands, introducing its aims, purpose, and the problems it solves. 

Before anything, here is a relevant xkcd:

<figure class="xkcd-embed">
  <a href="https://xkcd.com/1597">
    <img src="https://imgs.xkcd.com/comics/git.png" title="If that doesn't fix it, git.txt contains the phone number of a friend of mine who understands git. Just wait through a few minutes of 'It's really pretty simple, just think of branches as...' and eventually you'll learn the commands that will fix everything." alt="https://xkcd.com/1597">
  </a>
  <figcaption>
    "Git" - created by <a href="http://xkcd.com">xkcd</a>
  </figcaption>
</figure>

## Introduction

First, **GitHub is not git**. It is an important conceptual distinction, and the difference will be explained later. To understand how to use GitHub, one has to first understand git. 

### What is git? 

Git is a version control system. Remember those times when you had `report-FINAL.docx` and `report-FINAL2.docx` and `report-REALLYFINAL.docx`? A version control system is a solution for that. It keeps tracks of your history in a folder so you don't have to create multiple files or folders just so that you can retain history. It takes a series of snapshots of your folder, so that you can revert to any one of those snapshots anytime. 

There are various version control systems out there, such as [cvs](http://www.nongnu.org/cvs/) and [svn](https://subversion.apache.org/), and git is one of them, the most popular of them all. 

In fact, apart from retaining the history of a document, you've probably also had troubles when multiple people edit the same file, and oops, your colleague's changes overrode yours and your edits are all gone. Collaboration--that's also a problem solved by git. 

So now you can see why it might be useful. Git is mostly used for code, because code is just plain text files, as compared to Microsoft Word whose data is stored in binary, though apparently, a quick google tells me that you can make it work with certain binary files after [jumping through some hoops](http://blog.martinfenner.org/2014/08/25/using-microsoft-word-with-git/).

In short, git is a version control system that solves these problems: 

- keeping track of your history
- multiple people working on the same set of files

A note about terms that might be used: folder is used interchangealy with directory, and in this context a repository refers to a version-controlled folder. 

### Basic git commands: stage and commit

With a version control system, the very basic thing you would want to do is to make changes and tell git to track those changes. 

To start off, you need to tell git to start tracking changes in your folder. If you haven't downloaded git yet, now is the time. There are plenty of guides for installing git and plenty of options for git clients, some of which include a user interface, which is useful for visualizing what's going on in git. Just choose any one. For now we'll just be working with the command line. 

Let's say we want to version control a folder called `flowers`. Navigate into `flowers` on the command line, and do 

```shell
git init
```

This tells git to start tracking changes in the current folder. 

Then make some changes. Create a text file or something. Now you want to tell git that you've made some changes and ask them to record your changes, in essence, make a checkpoint. 

This is called committing your changes. But before you commit, you have to stage your changes. 

Let's say you added a new file called `tulips.md`. You can stage it by doing

```shell
git add tulips.md
```

or

```shell
git add .
```

The single dot `.` tells git to stage all changes in the folder. At this point, your file `tulips.md` is staged, ready to be committed. Then you can commit your staged files by doing

```shell
git commit -m "here is a commit message!"
```

At this point, it might seem strange why there are two steps: staging then committing. Staging seems like a duplicate step, because in this case we're doing essentially the same thing in these two steps. 

However, the usefulness of staging comes in when you have made changes to many files and only want to commit a few. Perhaps you fixed a bug while implementing a feature, and you don't want them to be in the same commit. Staging allows you to do that. 

Currently, everything is saved locally--all your commits and version history. There are certainly other things that can be done, such as reverting changes, soft / hard reset, and there are plenty of tutorials out there that go in depth about git commands. 

But to see where git truly shines, we would have to look at collaboration. 

## Collaboration with git

### What is GitHub and what has it got to do with git

To collaborate with others, we have to find a way to share whatever folder we are working on. You might have done this by email, by Dropbox, by Google Drive, or something else. The idea is that there must be a central place that holds the folder, so that everyone is looking at the same thing. 

That is what GitHub is: a web-based hosting service for git repositories. Git is the tool, and GitHub is the service for projects that use git. There are, of course, other git repository hosting services other than GitHub, such as [Gitlab](https://about.gitlab.com/) and [BitBucket](https://bitbucket.org/), or you can [host your own git server](https://www.techrepublic.com/article/how-to-set-up-a-gitlab-server-and-host-your-own-git-repositories/).  

The following section talk about how to work with remote repositories hosted on a server. This server is GitHub most of the time, but it doesn't have to be. These are features of git, which means that they are not specific to GitHub. 

### More git commands: push and pull

Now that there is a remote repository, there are many more things you can do, most notably: push and pull. 

Before you can do that, you have to set up authentication with the remote server. First, you would need a GitHub account. Then, you can follow the instructions at [Set up Git at GitHub](https://help.github.com/articles/set-up-git/#next-steps-authenticating-with-github-from-git) to set up authentication. After setting up authentication properly, you wouldn't have to type your GitHub password every time you need to access GitHub locally. 

After committing your changes locally, you have to inform your remote repository (e.g your GitHub repository) of the changes. This is known as pushing your changes. 

Before you can push, you have to tell your local folder about the remote: 

```shell
git remote add <remote name> <remote url>
```

On GitHub, the remote url can be found at the clone and download button, and should look something like `https://github.com/user/repo.git` (https) or `git@github.com:user/repo.git` (ssh). 

The remote name can be anything you like. In many tutorials, you'll see it named as `origin`. But it can absolutely be anything you like to call it. 

After setting up the remote, the command to push is: 

```shell
git push <remote name> <branch name>
```

At this point, we only have one branch: the default `master` branch. Branches will be explained in the next section. 

It is only at this point that, if you're collaborating, your teammates are informed of your changes. Anything before you push is local and only visible to you. 

The equivalent reverse action is pulling other people's changes. If other people have made changes and pushed to the remote repository, you can pull their changes by doing

```shell
git pull
```

### Branching

Branching is a powerful feature. So far, we've been working on the default master branch. While branching is not a feature only used in collaboration, it is something whose usefulness manifests itself hugely in collaborative projects. Without branching, powerful workflows would not be possible. 

Think of it, literally, as a branch in a tree. The master is the trunk, which you can branch off, so that you can make changes to the project without affecting master. Main operations would be to: 

- create branches
- switch between branches
- merge branches

Why branching? You might want to make a feature that will necessitate multiple commits, and you don't want to pollute the master branch. Often you have different members on your team working on different things. For example, you might be fixing a bug, while your team member might be working on a feature, and another teammate is trying out with another version of the website. Branches isolate all these things in their own contexts. Many projects have some version of the production or development branch, and other feature and bugfix branches. 

By convention, the default branch is the master branch. 

To create a branch named hotfix from the current branch and switch to it: 

```shell
git checkout -b hotfix
```

To switch between branches that already exist, simply do

```shell
git checkout <branch name>
```

To merge `hotfix` back into `master`, do

```shell
git checkout master
git merge hotfix
```

This can all be done on the command line, but a graphical user interface (GUI) can can make this part of the process much easier, especially when you have multiple branches to keep track of. Especially so when you have merge conflicts to deal with. This is optional, and here is an [extensive list of git GUIs](https://git-scm.com/downloads/guis).

### Contributing to open source: fork and pull requests

If you're looking to contribute to an open source project on GitHub, there are a few more steps to follow. When you are not a collaborator of the project, that is, you don't have push access, you have to first fork the project. That is easily done by pressing the fork button on GitHub. Take note that unlike previous operations, **forking is a GitHub concept and not a git concept**. 

After forking, the repo now lives remotely on your own GitHub account. To get a local copy of the remote repo, you would have to clone it. For example, if you want to contribute to [astropy](http://www.astropy.org/), you would first fork the repo from the astropy GitHub page, then do: 

```shell
git clone git@github.com:<your-username>/astropy.git 
```

Now, create a new branch, checkout that branch, and make some edits, commit them, push to GitHub, and now the edits live on your fork of the project. However, as you don't have push access to the project, you would have to create a pull request (PR) from your branch to the original project. 

<p class="notice">
<b>Aside: Why is it called a pull request and not a push request if you are essentially suggesting edits?</b> This was confusing for me when I first heard about PRs. But the reason it is called a pull request is that you are not requesting the project owners to allow you to <em>push</em> to the repository; instead, you're requesting for them to <em>pull</em> your branch, and hence it is called a pull request, not a push request. 
</p>

Each repository has its own contributing guidelines. Be sure to read them before contributing. 

The [Astropy developer documentation](http://docs.astropy.org/en/latest/development/workflow/development_workflow.html), for example, provides a good guide for setting things up and provides guidelines for contributing to a large open source project. In my opinion it is incredibly well written and most things are not specific to Astropy, but overall applicable to anyone who wants to contributes to open source. 

And all that's left is to wait for the open source collaborators to review your pull request. 

## Conclusion

There are a great many things git can do that this tutorial doesn't cover, the most prominent (I think) being `git stash` and `git fetch`. As was mentioned in the beginning, the aim is to provide a sort of high-level understanding and point you to the right questions to ask. Once you know your questions, there are tons of more detailed git documentations / tutorials out there. 

## Some resources and useful things
- [Git Tower - Understanding branches in Git](https://www.git-tower.com/blog/understanding-branches-in-git/)
- [Try git: An interactive git tutorial](https://try.github.io/)
- [Astropy's developer documentation](http://docs.astropy.org/en/latest/development/workflow/development_workflow.html#pull-request)
- [Gitmagic](http://www-cs-students.stanford.edu/~blynn/gitmagic/)
- [Deeper inside git](https://matthew-brett.GitHub.io/curious-git/curious_details.html)
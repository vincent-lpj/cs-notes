###### Reference

[The Git & GitHub Bootcamp](https://www.udemy.com/course/git-and-github-bootcamp/)

## Section 1: Course Orientation

#### 1. Welcome to the Course

Step 1: Learning Git

Step 2: Living Git

#### 3. What the Course Cover

###### Git Core

1. Intro to Git
2. Installation
3. Git Basics
4. Committing in Detail
5. Branching
6. Merging

###### Next Level Git

1. Diffing
2. Stashing
3. Undoing Changes

###### GitHub/Collab Core

1. GitHub Intro
2. Fetching & Pulling
3. GitHub Odds & Ends
4. Collaborative Workflows

###### Git: The Other Parts

1. Rebasing
2. Interactive Rebasing
3. GitTags
4. Git Behind the Scenes
5. Reflogs
6. Custom Aliases

## Section 2 Introducing Git

###### What is Git?

[Official Website of Git](https://git-scm.com/)

Git is the world's most popular version control system (VCS).

Version Control System is a software that tracks and manages changes to files over time.

VCS usually generally allow users to revisit earlie versions of the files, compare changes between versions, undo changes, and a whole lot more.

###### What Git can Do for You?

- track changes accross multiple files
- compare versions of a project
- "time travels" back to old versions
- revert to a previous version
- collaborate and share changes
- combine changes

###### History of Git

Linus Torvalds

[Git Source Code Mirror](https://github.com/git/git?tab=readme-ov-file)

###### Who Use Git

- Engineers & Coders
- Tech-Adjacent Roles
- Government
- Writers

###### Git and GitHub

Git is the version control software that runs locally on your machine.

Github is a service that hosts Git repositories in the cloud and makes it easier to collaborate with other people.

## Section 3 Installation & Setup

###### Installing Git: Terminal Vs. GUI

Git is (primarily) a **terminal** tool. Git is created as command-line-tool.

Popular [git GUIs](https://git-scm.com/tools/guis) include: Github Desktop, GitKraken

This course will use the command line first, because it is the most commonly used Git Interface.

GitKraken will also be used in this course to illustrate.

###### Mac Git Installation & Configuration

```bash
git --version

# We need to provide the following infos before using git
# name
# email
git config --global user.name "Your Name"
git config --global user.email "Your Email"

# Check your name and email address
git config user.name
git config user.email
```

## Section 4: The Very Basic of Git: Adding & Commiting

#### 24. Important Topics

In this section, we will get to know what are git repos, the commiting workflow, and commands like `git init`, `git status`, `git add`, `git commit`, `git log`. And finally, we will explore the `.git` folder.

######

#### 25. What Is a Git Repo?

###### Repository

A Git `Repo` or `Repository` is a workspace which tracks and manages files within a folder.

#### 26. Our First Commands: Git Init and Git Status

`git status` gives information on the current status of a git repository and its contents.

Use `git init` to create a **new** git repository.

```bash
git status
# fatal: not a git repository (or any of the parent directories): .git

git init
# Initialized empty Git repository in /Users/**/**/**/.git/

git status
# On branch main

# No commits yet

# nothing to commit (create/copy files and use "git add" to track)
```

#### 27. The Masterious .Git Folder

In the reference of `git init`, we can find what is `.git`

> This command creates an empty Git repository - basically a `.git` directory with subdirectories for `objects`, `refs/heads`, `refs/tags`, and template files.

In fact, `.git` is a **directory**.

```bash
ls .git/
# HEAD         description  info/        refs/
# config       hooks/       objects/
```

#### 28. A Common Early Git Mistake

Do not init a repo **inside** a repo!

So, using `git status` to check if there has been a git repo existing.

#### 29. The Commiting Workflow Overview

One **commit** is basically a checkpoint, a snapshot of the repository.

Changes in a repository can be **grouped** selectively to a single commit.

We use `git add` to highlight or select changes included in the next commit.

###### The Basic Git Workflow

- Working on stuff (`Working Directory`)
  - Make new files, edit files, delete files, etc.
- Add changes (`git add`, `Staging Area`)
  - Group specific changes together, in preparation of commiting
- Commit (`git commit`, `Repository`)
  - Commit everything that was previously added

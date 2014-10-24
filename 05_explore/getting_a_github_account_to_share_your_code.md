# Getting a Github account to share your code

## What is git and why use it?

Lots of people, but programmers especially, need to share lots of files. Sometimes you want to even keep different versions around to compare which looks (or works) the best.

The conventional method of renaming files with different numbers or phrases, such as "`my_presentation.pptx`", "`my_presentation_2.pptx`" and so on, works well enough when dealing with a few files.

But this doesn't work so well for developers, whose projects often have hundreds of files. Our small chirps application already has a few dozen! Renaming every single file with "`version_2`" on the end, over and over, would get tedious.

So as far back as the 1970's, software developers have used **Version Control** systems to manage different versions, and allow many people to work on the same project simultaneously. With a Verson Control system, you never need to email files with names like "`presentation version 3 (final).txt`".

**Git** is a modern and powerful tool for Version Control.

**GitHub** is a website that lets you back-up your code, share it for free, and see other people's code, all by using git!

Both git and GitHub have become important tools by helping people share open-source code more easily. In fact, all of the code for [Ruby on Rails can be found on a GitHub page](https://github.com/rails/rails). As you can see, over 2,400 people have worked together to make Rails as awesome as it is today!

## Getting git

To check if you have git, first enter the comman:

```bash
$ git --version
```

If you run Windows, you should already have git built in to the "Git Bash" terminal you have been using.

For Mac OS X, if you are using 10.6, 10.7, or 10.8, you should be fine as well. If you are using Mavericks (10.9), and do not have git installed, please talk to your coach.

Linux users install git from your package mananger.

Next we need git to know who you are. Because the tool was built to share code between people, it won't let you add new files without knowing who did it:

```bash
$ git config --global user.name "your-name"
$ Type git config --global user.email "your-email"
```

Using git follows the pattern of writing `git` command in command line, followed by other words describing what you want git to do. So for instance, the usual workflow to save your changes in git is to first "add" them, and then "commit" them with a message describing what you did.

But first off, we need to tell git that we want to start having it watch for changes in our app. In your project's root directory, enter the command:

```bash
$ git init
```

This **initializes** the folder as a place that git should keep an eye on. The files which are being watched by git is commonly called the project's **repository**. If you ever hear a developer say the word "repo" or "git repo", they are using **repo** as shorthand for the word repository.

For the moment, we'll run a few more commands that your coach can explain in detail. The basic idea is we are helping git catch up to where we are so far in our project. Still in the project root, after running `git init` :

```bash
echo "public/uploads" >> .gitignore
echo "tmp" >> .gitignore
echo "logs" >> .gitignore
git add .
git commit -m "Initial commit."
```

> **COACH:** Explain .gitignore to the students and why we don’t want these files included in our project's version history.

## Using git

Earlier we saw that the words "add" and "commit" are somehow used to save our changes in git, so let's dig deeper into that. Let's say we added a logo to our Chirps app, we would first check what files have changed since the last time we used git. We can check these changes by asking git for the repository's *status*:

```bash
$ git status

On branch master

Untracked files:
  (use "git add <file>..." to include in what will be committed)

  app/assets/images/logo.png

nothing added to commit but untracked files present (use "git add" to track)
```

And we see that there is an **untracked file** which is our `logo.png`, and git has suggested we use "git add" to track it. So let's do that with the command:

```bash
$ git add .
```

Note the space between `add` and the period. And if we again ask git for the project's status:

```bash
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

  new file:   logo.png

```

Now git can "see" our `logo.png` as a new file that has been created. But we're not done yet! Git gives you a chance to add changes to files slowly, and then collect one big list of changes and give it an explanation. This is called a **commit**, and the explanation is called a **commit message**.

We tell git to make this commit (a.k.a. list of changes) by using the command:

```bash
$ git commit -m "Added a logo."
```

The `-m` and the section in quotes immediately afterward is a message to ourselves (or coworkers!) about what we changed and why. For example, after added a big, difficult new feature to a project it would be appropriate to write:

```bash
$ git commit -m "Added users with passwords and profiles."
```

It would be confusing and inappropriate to write:

```bash
$ git commit -m "Gosh that was a lot of work!"
```

This is because later on, if you need to know what you changed via a quick glance, *"a lot of work"* doesn't really tell you what was done to the code itself.

## Putting our code online with GitHub

First, go to https://github.com/ and sign up, confirm your account via email, and sign in.

In the top-right corner there is a plus symbol. Click it and select "Add New Repository" in the menu that appears. Fill in a name for the repository. Simply calling it "chirps" is fine, and we will use that name in our examples.

Now back in the command line, we need to tell the git on our computer to talk to our GitHub account online. This is done by adding a **remote**, that is, a git repo somewhere outside our computer:

```bash
$ git remote add origin https://github.com/YOUR_USERNAME/chirps.git
```

Here we have given the nickname "origin" to the remote repository. Now we can **push** our code out to GitHub by using that nickname:

```bash
$ git push origin
Counting objects: 10, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 1.65 KiB | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
To git@github.com:YOUR_USERNAME/chirps.git
   938701a..a7ce718  master -> master
```
Congratulations, if you check out your Github page now, you will see the Chirps Project has all of your code from today in it!

With any changes to your project in the future, to keep a copy of them on Github and share with the world, the same process repeats itself:

Add Files via `$ git add .`, make a commit with a summary of what you did `$ git commit -m "Message Here!"` and then "push" the changes online via `$ git push origin`.

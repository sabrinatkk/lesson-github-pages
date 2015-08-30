# Setting Up Your Online Presence Using GitHub Pages

- **Author**: Bruno Grande
- **Research field**: Cancer genomics, computational biology
- **Lesson Topic**: GitHub and Git

## Motivation

As the title suggests, this lesson is about setting up your
online presence using GitHub Pages. First, I'd like to explore 
a bit why you should concern yourself with creating a personal
space online. Let's be honest with ourselves: when we hear about
someone that we don't know much about, our reflex is to google
them, right? Well, believe it or not, people will (or already are)
doing that for you. Whether it's colleagues, collaborators or 
future employers, you probably want to leave a good first impression. 

What's the current status of your online presence? Take a look
yourself: open a new browser window in Incognito or Private 
mode and google your name. What comes up? Are any of 
the results on the first page related to you? For some of you, 
your LinkedIn profiles will show up and this is a good start. 
But the reality is that everyone can easily create one. You
can differentiate yourself and gain an edge over others by 
creating a website. You might not know HTML, CSS or JavaScript. 
You also might never have had experience with web hosting. 
This is where GitHub Pages comes in. 

GitHub Pages is a feature offered by GitHub that enables Git
repositories to act as websites. Don't worry though: you don't
need to fully understand Git to use GitHub Pages. In this lesson,
I will introduce some basic concepts to get started. Over time,
you will continue to learn about Git until you become proficient.
This will be worth your while: Git is a powerful version control
system that I recommend you all use. Many things can be tracked by
Git: code, papers, results, etc. Today, we'll focus on your personal
website. Let's get started then!

**Fun fact:** [SciProg.ca](http://sciprog.ca) is actually hosted on 
GitHub Pages. This just comes to show how powerful it can be.

## Lesson Notes

### Forking and Cloning a Template

You can write your own website from scratch, but that takes time
and knowledge about HTML, CSS, JavaScript and Jekyll, the underlying
platform used by GitHub Pages. Instead, we'll kickstart our website
by using a template. For this lesson, I'll be using the [Pixyll template]
(https://github.com/johnotander/pixyll), but there are [many options]
(http://jekyllthemes.org/) out there. I mostly learned HTML and CSS by
starting off with a template and tweaking it bit by bit. You can do the
same!

The Pixyll template repository is owned by [John Otander]
(https://github.com/johnotander), meaning that we can't edit it as is. 
We need to create a copy of the repository under our account first. This
is called forking the repository. You may visit the [repository page]
(https://github.com/johnotander/pixyll) and click the Fork button at the
top-right. If GitHub prompts your to select an account to store the fork
under, choose your personal GitHub account. 

![Fork](images/1-fork.png)

Next, we need to tidy up our newly created repository fork. First, 
we need to rename it to `<username>.github.io`, where you replace 
`<username>` with your actual GitHub username. This will be your website
address. To rename your repository, visit the Settings page. 

![Rename](images/2-rename.png)

Let's change the repository's description to something more adequate.
For example, the description can be "My Personal Website" and the
website will be the same URL as above, `<username>.github.io`. You
can edit the description by clicking the "Edit" link beneath the 
repository name at the top. 

![Description](images/3-description.png)

Now that we've done some tidying, we can download the repository. 
In the world of Git, this is done by cloning the repository. As the
name implies, you're creating an exact copy locally. To accomplish this,
copy the link located at the bottom right of the repository page. 
If you haven't set up SSH keys (or haven't heard of SSH keys), make
sure you click the small HTTPS link and then copy the repository link.

![Link](images/4-link.png)

Now, open a Bash shell. Navigate to where you want to store your local 
copy of the website. For instance, I have a `Repos` directory. Then, 
run the git clone command using the link your copied. Git might ask
for your GitHub login information. You may avoid this by [setting up
SSH keys](https://help.github.com/articles/generating-ssh-keys/). 

```bash
# Create a Repos directory in your home folder
mkdir -p ~/Repos
# Change directory
cd ~/Repos
# Clone the website repository (replace <username>)
git clone https://github.com/<username>/<username>.github.io.git
```

You now have a local copy of your website repository! Also, if you
visit the URL (`username.github.io`), your website should be live. 
Of course, it isn't personalized yet, but this is what we're gonna
do next. 

### Personalizing your Website

Now that you've cloned your website repository, we need to make a few
changes. First of all, we need to delete the file called `CNAME`, 
whichis meant to be used for custom domains. Otherwise, we'll keep 
receiving email notifications that the CNAME is already taken. 

```bash
# Enter your repository directory
cd <username>.github.io
# Delete the CNAME file
rm CNAME
```

This is a small change, but let's save it by committing it to the
Git repository. If you run `git status` in your repository, you'll
be given a list of changes. Here, we should only have one change: 
the CNAME file we deleted (see below for example output). 

```
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    CNAME

no changes added to commit (use "git add" and/or "git commit -a")
```

When we commit a change like this one, it allows us to track each
edit we make and this grants us the power of reverting a specific 
change if we mess up. There are two steps to committing a change:

1. Adding the change to the stage. 
	- This allows us to pick and choose which changes we want to 
	commit first, in case there are multiple changes in the repository.
	- In our case, we only have one change, so this step seems a bit
	superfluous. It becomes more useful when your changes are more complex.
2. Commit the change. 
	- This step requires you to provide a message describing the change.
	This is useful when you are looking back at individual changes. 

Using the command-line, we achieve these steps as follows. 

```bash
# Include all changes made in the repository for the next commit
# Here, the . refers to the current directory, namely the entire repository
git add .
# Commit the changes by giving a message describing the change
git commit -m 'deleted CNAME file'
```

This change is now registered as a commit locally, but GitHub isn't
aware of the change yet. For that, we need to push the commits we've 
created since running `git clone` to GitHub. In this case, we only have
one. For this, you simply run `git push`. 

```bash
# Push your changes to GitHub.com
git push
```

Now, if you visit the GitHub page for your website, you should see your
commit. 

![Commit](images/5-commit.png)

----

#### Challenge Problem 1

Edit the _config.yml file according to your preferences. When you're done, 
commit and push those changes to GitHub.

**Hint:** If you've installed Jekyll, you can preview your website locally
by opening a new Bash shell, changing to your repository directory and 
running `jekyll serve`. There will be a URL (_e.g._ http://127.0.0.1:4000/) 
you can visit. 

*Answers to challenge problems are located at the bottom of this lesson.*

----

After pushing these changes to GitHub, you can visit your website's URL
(`<username>.github.io`) to see the changes take effect. It might take a 
few minutes for them to appear online. 

#### Creating our First Blog Post

Next up is creating our first blog post! The Pixyll template makes it 
painless for us to accomplish this. Blog posts are stored in the _posts 
subdirectory. We're gonna delete all but one, which we are gonna edit into 
our own post. Conveniently, there's only one 2015 post, so we're gonna 
remove all 2014 posts.

```bash
# Delete all but one blog posts
rm _posts/2014-*
```

Let's rename this blog post into our blog inauguration accouncement.

```bash
# Rename remaining post into something else
mv _posts/2015-07-11-announcing-pixyll-version-2.md _posts/2015-09-01-first-blog-post.md
```

Now, open this Markdown file in a text editor and change it to whatever 
you want while sticking to the template, of course. Leave the layout as  
`post` and categoriescan be anything you want; they're like tags. For 
something like this, you can use `general`, but whenever you write more 
scientific posts, you can use a `science` category.

Here's my example: 

```
---
layout:     post
title:      First Blog Post!
date:       2015-09-01
summary:    This is my first blog post
categories: general
---

May this be the beginning of something great!

```

Let's commit and push these changes to GitHub. Since we only changed 
the contents of the _posts directory, we only need to add it to the 
staging area.

```bash
# In this case, we can only add _posts to the staging area
git add _posts
# Then, we commit
git commit -m 'my first blog post!'
# Let's go live!
git push
```

Once again, you can visit your website's URL (`<username>.github.io`) to
see your blog post go live. You might have to wait a few minutes first. 

----

#### Challenge Problem 2

Edit the about.md file so that it describes you and what you do. 
When you're done, commit and push those changes to GitHub.

*Answers to challenge problems are located at the bottom of this lesson.*

----

## Answers to Challenge Problems

#### Challenge Problem 1

I changed my _config.yml as follows. I only included the sections I edited. 

```yaml
# Site settings
title:       Bruno's Blog
email:       bgrande@sfu.ca
author:      Bruno Grande
description: "Where I write about my thoughts and experiences"
baseurl:     ""
url:         "http://brunogrande.github.io"
date_format: "%b %-d, %Y"

[...]

# Optional features
animated:           true
```

Once I'm done with my changes, I can commit and push them to 
GitHub as follows.

```bash
git add .
git commit -m 'modified config to my liking'
git push
```

#### Challenge Problem 2

Your approach should be the same as in Challenge Problem 1. Here's 
my `about.md` file. 

```
---
layout: page
title: About Me
permalink: /about/
---

My name is Bruno Grande and I'm a graduate student at SFU. 
I work in Ryan Morin's lab in the Department of Molecular Biology
and Biochemistry. Despite that, I exclusively do computational biology.
In essence, I use computation to answer biological questions. In our lab, 
our questions focus on cancer genomics, a growing field enabled by next-
generation sequencing. 

Check out my [GitHub page](https://github.com/brunogrande) for some of my 
open-source projects, and [Twitter](https://twitter.com/grandebruno) for my 
quick thoughts. 
```

Once you're done editing your About page, commit and push as usual. 

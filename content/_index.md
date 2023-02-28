+++
title = "Version Control"
outputs = ["Reveal"]
+++
<!-- some miminal styling here
     no CSS file because minimal
     - embedding CSS like this in a  markdown file
       is NOT recommended - don't try this at home!
-->
<style>
<!-- end of  minimal styling -->    
/*
body {
  background-color: lightgray;
}
.reveal .slides section,
.reveal .slides section > section {
  font-size: x-large;
  text-align: justify;
}
// Slide-specific vertical centering override
.reveal .slides section[data-vertical-align-top]{
	top: 0 !important;
}


p,div {
  font-family: Georgia, serif;
  font-size: 0.5em;
}
  

*/

.reveal h2,h3 {
    color: gray;
    text-align: center;
  }

.reveal h1 {
  color: yellow;
  text-align: center;
  font-size: 1.2em;
  margin: 0px 0 50px;
}

</style>

# A Gentle Introduction to Version Control
## Martin Collier
### 1st March, 2023

---

# What is Version Control?

- a backup mechanism for software and documentation projects
  - with an "undo button"
  - and a "redo button"
- you can skip back to the version of your project it would revert to only after multiple "undos" in one leap
  - hence called version control

---

# Benefits of Version Control

{{% section %}}

- labelling the versions means it's easy to roll back to (e.g) the working version of the code from last night and to undo all the code "improvements" you made today.
  - new features can be added with confidence
- tasks can be distributed to multiple authors or developers
  - version control can be used to _merge_ their contributions 
  - not our focus today

---

- you can separate the code/text/whatever implementing various flavours of the project
  - e.g., a book might have chapters that only appear in the US or UK editions

{{% /section %}}

---

# Disadvantages of Version Control

- works from the command line
  - there are IDE integrations for VSCode, Jetbrains IDEA, etc.
  - GitHub provides a GUI-based client
- not so effective with non-text sources
  - Microsoft Office files, bitmap images, etc.
- learning curve

---

# Git and GitHub

- git is a relatively new version control tool (first version 2005)
  - probably the most widely used
  - alternatives include Subversion and Mercurial
- GitHub is the most popular hosting service for Git
  - Alternatives include GitLab, Bitbucket
- Let's look at git and GitHub    

---

# Tools we'll use

{{% section %}}

- A terminal application
  - If running Windows 10+, I recommend installing [Windows Terminal](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701)
  - Otherwise, open up PowerShell
  - On Linux, use whatever terminal tool is installed with your distribution
  - On Mac, buy me an M1 and I'll figure out for you what to do

--- 

- A version of git
  - you can [install git](https://gitforwindows.org/) on Windows
    - I've found this a bit temperamental on my laptop
  - In Linux, install it using your package manager
    - e.g., on Ubuntu `$ sudo apt install git`

--- 

- I recommend installing Ubuntu on W10+ from the Windows Apps Store
    - use this [link](https://apps.microsoft.com/store/detail/ubuntu/9PDXGNCFSCZV)
        - this installs a command-line version of Linux only
        - no GUI

---
- Windows App Store (cont.)          
    - install git (`$ sudo apt install git`) and then (e.g.)
        - `$ cd /mnt/c/Users/YourName/Development`
    - can now use your favourite windows GUI editor (VSCode?) but have the Linux version of git
    - can open up File Explorer from the Terminal with `$ cd ~ &&explorer.exe .`

---

- Our demo application today requires us to install [Hugo](https://gohugo.io/installation/)
  - this is _not_ needed for either git or GitHub workflows 
    - just a tool our toy project needs
    - we'll also use a Hugo [theme](https://themes.gohugo.io/) called [reveal-hugo](https://themes.gohugo.io/themes/reveal-hugo/)      

{{% /section %}}

---

# Aside: installing Hugo

{{% section %}}

- [Hugo](https://gohugo.io/) is a static website generator
- Installation instructions for Windows are [here](https://gohugo.io/installation/windows/)
  - I installed it from source on the command line in Ubuntu (Windows 10 Store version). You can do this using the commands below (there are [easier ways](https://gohugo.io/installation/linux/)!)

---

```bash{1|2-5|6-8|9-11}
$ sudo apt install build-essential git-all
$ wget https://go.dev/dl/go1.20.1.linux-amd64.tar.gz
$ sudo rm -rf /usr/local/go
$ sudo tar -C /usr/local -xzf go1.20.1.linux-amd64.tar.gz
$ echo export PATH=$PATH:/usr/local/go/bin >> ~/.profile
$ source ~/.profile 
$ go version
$ rm go1.20.1.linux-amd64.tar.gz
$ go install -tags extended github.com/gohugoio/hugo@latest
hugo version
$ hugo version
```
{{% /section %}}

---

# Interlude

{{% section %}}

- Slide show halted whilst I log into [GitHub](https://github.com) and create a new _repository_
  - I'll make it _private_ rather than _public_, just to make life a bit harder for myself.
  - I'll go through some of the other steps involved live.

- I also need to create a _Personal Access Token_ so that I can access the repository from the command line.

---

- You can create tokens for your GitHub a/c as follows
  - Click on your user icon at the very right of the "ribbon" at the top of GitHub landing page
  - Select Settings/Developer Settings/Personal Access tokens
  - create a "classic" token using the "Generate new Token" button
  - Make sure to copy the token to a local file 
- We'll enter the token whenever we are prompted for a password by git when accessing GitHub   

{{% /section %}}

---

# <del>Three</del> Two ways to get your project onto GitHub

{{% section %}}

1. download the (virtually) empty "repo" we just created from GitHub into a directory on our local machine and add our code/text/etc. to the folder
2. Pair an existing local project folder that is already under version control with the (virtually) empty repo we just created on GitHub
3. <del>Execute some magic git command that tells GutHub to create a new repo based on the contents of an  existing local project folder</del>


---

- So whether or not we want to upload an existing project to GitHub, or to create a brand new project, our first step in pairing it with GitHub has to be to create a new repo on GitHub
  - rather disappointing for those of us who prefer the command line to using a mouse

{{% /section %}}


  ---

# Interlude

- Slide show halted whilst I show how the command line steps to pair our local directory and the remote repo on GitHub.
I'll use these commands

``` bash
git init # creates a new .git subfolder and populates it with git stuff - you can now do version control on the folder contents using git
git clone https://github.com/leachim6/hello-world.git # downloads a copy of a repo from GitHub including its .git subfolder
git status # tells you what files have not yet been brought into version control
git log # lists events that have occurred to the repo
git add . # tentatively adds all new or updated files to the repo
git commit -m "add wonderful code" # "commits" those tentative files, and labels the commit with a text descrption
git push # updates a remote repo with the changes in our local copy 
```

{{% note %}}
```bash
hugo new site version-control # create a new directory laid out as per hugo requirements
cd version-control/ # go into it
git init # set up version control
hugo mod init github.com/jamstackdev/version-control # set it up as a hugo module
git submodule add https://github.com/dzello/reveal-hugo.git themes/reveal-hugo # download (via git) the project theme
nano config.toml # edit/enter some project settings
nano content/_index.md # add slideshow content here
hugo serve # see how it looks at http://127.0.0.1:1313
hugo # create the website in public folder
git status # what files have changed?
nano .gitignore # add public dir to list of files to ignore
git status # the public folder contents no longer listed
git add .
git status
git commit -m "first slide"
git status
git log
git push # this won't work - git doesn't know where to push to (i.e., github)
git remote add origin https://github.com/jamstackdev/version-control.git
```
{{% /note %}}

---

# Telling git about GitHub

- the command `git push` is used to copy the local repo to a remote repository
- we get this error
```
fatal: No configured push destination.
Either specify the URL from the command-line or configure a remote repository using

    git remote add <name> <url>

and then push using the remote name

    git push <name>

```
---

```bash
$ git remote add origin https://github.com/jamstackdev/version-contl.git
$ git remote -v
origin  https://github.com/jamstackdev/version-control.git (fetch)
origin  https://github.com/jamstackdev/version-control.git (push)
```

---

```bash
$ git push
fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin master

```
- see [this](https://stackoverflow.com/questions/37770467/why-do-i-have-to-git-push-set-upstream-origin-branch) explanation of what this means

---

- so now we try

```
$ git push -u origin master
remote: Repository not found.
fatal: repository 'https://github.com/jamstackdev/version-control.git/' not found

```
- What's gone wrong?
    - the push won't create a new remote repo
    - if the remote repo does not exist it just stops


---
# After creating the new repo

GitHub advises either
```bash
# create a new repository on the command line
echo "# version-control" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/jamstackdev/version-control.git
git push -u origin main
```
- or
```bash
# push an existing repository from the command line
git remote add origin https://github.com/jamstackdev/version-control.git
git branch -M main # GitHub prefers to call the principal branch "main" rather than "master"
git push -u origin main
```

---

We go with the second approach, since our git-managed project already exists
```
l$ git push -u origin main
remote: Permission to jamstackdev/version-control.git denied to ********.
fatal: unable to access 'https://github.com/jamstackdev/version-control.git/': The requested URL returned error: 403
```

You will most likely get a different error - it will compalin that you have no user email or user name associated with the repo. Check this using

```
$ git config --list
user.email=anonymous@nowhere.none
user.name=Joe-Jane Bloggs-Doe
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
submodule.reveal-hugo.url=https://github.com/dzello/reveal-hugo.git
submodule.reveal-hugo.active=true
remote.origin.url=https://github.com/jamstackdev/version-control.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
```

If those first two fields are blank, you need to set them, using either

```bash
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@wherever.com
```

or

```bash
$ git config user.name "Jane Doe"
$ git config user.email janedoe@wherever.com

```

The latter approach sets a custom identity for this repo, `--global` applies it to every repo attached to your account on the local machine


---

# Avoiding spam

- GitHub provides a "no reply" address you can use for commits so that you can keep your regular email address private when committing to a public repo. See [here](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address)
- this used to be simply `USERNAME@users.noreply.github.com` but new accounts have a more complex prefix - go into email settings on your GitHub account to find out what it is.

---

# the end

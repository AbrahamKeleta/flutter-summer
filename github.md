# Github 101

### Objective

Our goal is to get familiar with github and use it to collaborate on projects. 

Here is our visual that we will use to describe how we use git:

![alt text](https://github.com/Hgp-GeniusLabs/Curriculum/blob/cf5cc84bf0e486e9bc0319091b22ec204bf939ad/Immersion/Assets/git_visual.png)

## Part 1 - Introduction

### What is Git?

Git is a distributed version control system that is widely used for tracking changes in source code during software development. Created by Linus Torvalds in 2005, Git provides a way for multiple developers to collaborate on projects while keeping track of changes made to the codebase.

Here are some key features and concepts of Git:

Version Control: Git allows developers to track changes to their code over time. It maintains a history of all changes made to files within a repository.

Distributed: Unlike centralized version control systems, such as Subversion, Git is distributed. Each developer has a local copy of the entire repository, including its history. This makes operations like branching, merging, and committing faster and more flexible.

Branching and Merging: Git enables developers to create branches to work on features or fixes independently of the main codebase. Branches can be merged back into the main branch (often called "master" or "main") when the changes are ready.

Committing: Developers make changes to files within their local repository and then commit those changes to the repository's history. Each commit is accompanied by a message that describes the changes made.

Remote Repositories: Git supports remote repositories hosted on platforms like GitHub, GitLab, and Bitbucket. Developers can push changes from their local repository to a remote repository and pull changes made by others.

Collaboration: Git facilitates collaboration among developers by allowing them to share changes through branches and remote repositories. It also provides tools for resolving conflicts that arise when merging branches with conflicting changes.

Overall, Git has become an essential tool in modern software development workflows due to its flexibility, speed, and powerful branching and merging capabilities.

Your goal, as the image above implies, is to use the platform to create versions of a document or documents, and allow others to collaborate with you. 

## Part 2 - Create git repository


#### Locally, using git

```code

$ mkdir github_exmaple_folder
$ cd github_exmaple_folder

# initalize git inside the folder you want to track for versions

$ git init

# add files inside the folder to track with git

$ touch index.html
$ touch styles.css

# check the status of your repository

$ git status

```

Your terminal should show you files in **red**, letting you know that you haven't explicitly let git know to track the files you created inside your respository. Let's do that next

```code

# add all your files 

$ git add .

# check the status of your repo

$ git status

```

Your terminal should now be **green** and let's you know your files is being tracked. Next, let's add a message of what you have done in a commit so folks know what you did. 

```code

# commit message should be relevant

$ git commit -m "added index.html and styles.css to project"

```

## Part 3 - Pushing to Github.com


Now that we have our project being tracked with git, we need to push it to the cloud so everyone on the team can have access and collaborate. 

Go to github.com and create  respository: 

![alt text](https://github.com/Hgp-GeniusLabs/Curriculum/blob/f6d69c29941c7107f556701e9833194f8447c9c6/Immersion/Assets/github_new_repo.png)

Put the repo name, and create at the bottom. 

Next you should see two options: 

![alt text](https://github.com/Hgp-GeniusLabs/Curriculum/blob/a2f1d7b1023bbcdf1685f2eb447c461452542049/Immersion/Assets/github_options.png)

Go with option 2: 

Copy and paste those commands into your terminal

```code

$ git remote ...
$ git push -u origin main

```

At this point, you are finally pushing your local respoitory into the cloud at github.com

## Part 4 - Collaboration

Go to the repository's settings and go to collaborators, invite your team and they collaborate by cloning the project link: 

```code
$ git clone repository_link
```

More to come...

































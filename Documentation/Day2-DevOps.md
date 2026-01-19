# Connect a GitHub Repo with AWS

**Author:** Dhruva Kashyap  
**Email:** dhruvakashyap73@gmail.com

---

## Connect a GitHub Repo with AWS

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-github_dd9d254e)

---

## Introducing Today's Project!

We are here to connect our web application project to a GitHub repository using Git so the code is stored safely in the cloud and every change is tracked. This is important because a shared repository becomes the starting point of a CI/CD pipeline and allows collaboration, version control, and easy rollbacks. By pushing our code to GitHub and updating files like README, we ensure the project is ready for automated build and deployment in upcoming phases.

### Key tools and concepts

In this project, I learned how Git is used for version control to track changes, stage files, and create commits. I also learned how GitHub is used as a remote repository to store code in the cloud. The project helped me understand pushing local changes to GitHub, managing branches, and handling authentication using tokens.

### Project reflection

This project took me approximately 2 hours to complete. The most challenging part was understanding Git authentication and handling push/pull conflicts. It was most rewarding to successfully push my code to GitHub and see the version history working correctly.

I did this project today to strengthen my understanding of Git and GitHub. It helped me practice version control and learn how to manage code changes properly. This project also improved my confidence in using Git for real-world development workflows.

This project is part two of a series of DevOps projects where I’m building a CI/CD pipeline. I’ll be working on the next project tomorrow as part of the ongoing challenge.

---

## Git and GitHub

Git is a version control tool. It works like a time machine and filing system for your code. It tracks changes made to the code by taking snapshots at different points in time. These snapshots are called versions. Git helps you recover older versions of the code if something goes wrong with the current version.
Git was installed on the EC2 shell using the following command:
sudo dnf install git -y

GitHub is a cloud-based platform that hosts Git repositories and helps manage different versions of code. It is used to store code safely, track changes visually, and access it from anywhere. It also enables easy collaboration by allowing code sharing, reviews, and teamwork.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-github_efaadbf7)

---

## My local repository

A Git repository is a storage location where a project’s code and its complete change history are saved. It contains all files, folders, and versions (snapshots) tracked by Git. This allows you to manage changes, revert to older versions, and collaborate efficiently.

git init creates a new local Git repository inside the Project folder in the EC2 instance. It allows Git to start tracking changes made to files in that directory. This is the first step to enable version control for the project.

A branch in Git is a separate line of development within a repository. It allows you to work on new features or fixes without affecting the main code. Once ready, changes from a branch can be merged back into the main branch.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-github_7bf21bae)

---

## To push local changes to GitHub, I ran three commands

### git add

The first command run was 'git add . ' This command adds changes to the staging area, telling Git to collect all modified files for a final review before committing them.

### git commit

The second command was 'git commit -m "Updated index.jsp with new content" '. It saves the staged changes as a snapshot in the project’s version history. The -m flag adds a message describing the changes made in that commit

### git push

The third command was 'git push -u origin master'. It uploads the committed changes to the GitHub repository (origin) on the master branch. The -u flag sets the upstream, so future pushes can be done using just git push.


---

## Authentication

Git asked for a username and password to verify that the user has permission to push changes to the GitHub repository. This process is called authentication and is required when interacting with a remote repository. Since GitHub no longer allows password-based access, a secure personal access token is required instead.

### Local Git identity

Git needs a name and email to identify who created each commit. This information is stored in the commit history as the author details. It helps track changes, accountability, and collaboration in projects.

Running git log showed the list of commits made in the repository. It displayed details like the commit ID, author name, email, date, and commit message. This helped review the project’s change history.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-github_9a27ee3b)

---

## GitHub tokens

Authentication failed because GitHub no longer allows password-based authentication for Git operations over HTTPS. Passwords are less secure and can be intercepted, so GitHub disabled them. Instead, GitHub requires a Personal Access Token (PAT) for secure authentication.

A GitHub token is a secure, unique string used to authenticate access to GitHub repositories. It is used because GitHub no longer allows password-based authentication over HTTPS. The token safely verifies identity and permission when pushing or pulling code.

A GitHub Personal Access Token was set up by logging into GitHub and navigating to Settings → Developer settings → Personal access tokens. A new token was generated by selecting the required permissions (such as repository access). This token was then used in place of a password when authenticating Git commands.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-github_fa11169d)

---

## Making changes again

The file updated in the nextwork-web-project was index.jsp. A new paragraph line was added to verify that changes were pushed to GitHub. This update was committed and pushed to the remote repository.

To see the changes in the GitHub repo, the updates were first staged using 'git add .' They were then committed to the local repository with a commit message. Finally, the changes were pushed to GitHub using git push.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-github_6becb2bc)

---

## Setting up a READMe file

A README file is a document that explains what a project is about. It describes the project’s purpose, setup steps, and how to use it. It helps others understand the project quickly and professionally.

A README file is a document that introduces and explains a project. It describes what the project does, how to set it up, and how to use it. It helps others quickly understand the project when viewing it on GitHub.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-github_c94976902)

---

---

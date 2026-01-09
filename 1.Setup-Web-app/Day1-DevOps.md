<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up a Web App in the Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-vscode)

**Author:** Dhruva Kashyap  
**Email:** dhruvakashyap73@gmail.com

---

## Set Up a Web App Using AWS and VS Code

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-vscode_7a1de541)

---

## Introducing Today's Project!

This Project is day 1 of 7 days of the DevOps Challenge. 
In this challenge, we are going to set up the Foundation of CI/CD Pipeline by creating a webapp from scratch. We'll need to launch the EC2 Instance and connect the instance using VSCode to generate a web app inside.

This project is part one of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project tomorrow as part of the 7-day challenge. Continuing daily helps me stay consistent and build momentum. It also allows me to gradually improve my AWS and DevOps skills step by step.

I did this project today to gain hands-on experience with AWS and understand how real-world cloud servers are set up. I wanted to learn how to deploy and manage a web application on an EC2 instance. This project also helped me practice using SSH and VS Code for remote development. I aimed to improve my confidence in working with Linux servers and DevOps tools. Overall, it was done to strengthen my practical skills and prepare for real projects.

### Key tools and concepts

In this project, I learned how to launch and manage an EC2 instance on AWS and connect to it securely using SSH. I understood the importance of key pairs, file permissions, and security groups for secure access. I learned how to install and configure Java (Amazon Corretto) and Apache Maven to build Java web applications. I explored how Maven helps generate project structure and manage dependencies. I connected VS Code to an EC2 instance using Remote-SSH to edit files with IDE features. I also learned how to navigate and edit files using Linux terminal commands like pwd, ls, cd, and nano. I understood the difference between editing code in a terminal versus an IDE. I learned how changes made via SSH reflect instantly across different connections. Finally, I gained practical experience troubleshooting SSH and resource issues on cloud instances.

### Project reflection

It took me a few hours to complete this project from start to finish. Setting up the EC2 instance and installing the required tools was quick, but troubleshooting the SSH and VS Code connection issues took extra time. As a beginner, understanding the errors and fixing them step by step required patience. Connecting VS Code successfully and editing files felt like a big milestone. Overall, the time spent helped me learn a lot about real-world cloud and DevOps challenges.

One thing I didn’t expect in this project was how sensitive small EC2 instances are to resource limits. I was surprised that connecting VS Code using Remote-SSH could cause the instance to disconnect due to low memory. I also didn’t expect SSH connections to fail because of small issues like IP changes or key file location on my system. Troubleshooting these problems taught me how important instance sizing and security group settings are. Overall, it helped me understand that cloud setup issues are common and part of real DevOps work.

---

## Launching an EC2 instance

### What I did in this step

In this step, we are launching the EC2 instances in our AWS account. Also going to set up the network settings, which helps us to find EC2 instances and the key pair (Which helps us to make sure we have the permission to use and access the EC2 instance)

We started this project by launching EC2 instances, because EC2 instances are like Virtual Computers/Servers that live in the cloud. We want our web app to live in the cloud, so we are launching an EC2 instance to even develop a webapp code

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-vscode_7852fbf3)

### I also enabled SSH

SSH is Secure shell Protocol used to make sure only authorized users can access a remote server. It's also a type of traffic that lets us transfer the data back and forth with the EC2 instances once we connect to it.
I enabled SSH so that we can securely connect to our EC2 instance later, and we make sure that it only allows SSH traffic from my IP address for security.

### Key pairs

Key pair is a mechanisum for us to get connect and access to the EC2 instances that launched in the AWS. So we created a keypair for EC2 instances. It's made of two halves: a public key that AWS keeps, and a private key that you download. When we use the private key, it verifies that we're the one allowed to access that specific virtual machine, keeping everything secure and just for us.

### Downloaded key pair file

Once I set up my key pair, AWS automatically downloaded a private key file called network-devops-keypair.pem for safe keeping, we moves private key file into a folder DevOps in out dekstop. 

---

## Set up VS Code

### What I did in this step

In this step, I will be going to install VS Code, which is a tool that lets us write and edit code, and it's free of cost. We are also going to set up the terminal and update the permission settings of our key.

### What is VS Code?

VS Code is an Integrated Development Environment (IDE) that helps developers write, edit, run, and debug code efficiently. It supports multiple programming languages, offers smart features like syntax highlighting, auto-completion, and debugging, and can be extended using extensions for frameworks, Git, databases, and cloud tools. 

I installed VS Code to write and edit code in languages like Python, Java, C, JavaScript, and SQL. Run and debug programs to find and fix errors. Build web applications using HTML, CSS, and JavaScript. Manage projects with Git and GitHub integration. It also has handy extensions to connect to the EC2 instances.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-vscode_53d05e68)

---

## My first terminal commands

A terminal is a place for us to send commands, i.e., tell computer what we want to do. 
The first command I ran for this project is cd ~/Desktop/DevOps 
We navigate the terminal to the DevOps folder

### Updating file permissions

I also updated my private key's permissions by...

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-vscode_9328ada1)

---

## SSH connection to EC2 instance

### What I did in this step

In this step, we are connecting VS Code to the EC2 instance.
This allows us to access and work directly inside the EC2 server.
Once connected, we can set up and run our web application on the instance.

### Connecting to EC2

To connect to my EC2 instance, I ran the SSH command (ssh -i path-to-.pam-file ec2-user@public-ipv4-dns-path) in the VS Code terminal. I used the -i option to provide my .pem private key for authentication. Then I connected as ec2-user using the instance’s Public IPv4 DNS.

### This command required an IPv4 address

A server’s Public IPv4 DNS is its unique public address on the Internet. It allows other computers to find and connect to the server.
This DNS points to the EC2 instance so users and applications can access it remotely.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-vscode_e3069dca)

---

## Maven & Java

### What I did in this step

In this step, I will install Apache Maven and Amazon Corretto 8 on my EC2 instance because they are required to build and run Java web applications. I will set up Maven to manage project dependencies and automate the build process because it simplifies development. I will verify both installations because confirming the setup ensures the environment is ready for web app development.

### Why I'm using Maven

Apache Maven is a tool that helps to build and project management tool for Java applications. It automatically downloads and manages the libraries and dependencies a project needs. Maven also provides project templates (archetypes) to quickly set up Java web applications.

Maven is required in this project because it helps quickly set up a Java web application structure. It automatically manages and downloads all required dependencies. It also simplifies building and running the project efficiently.

### Why I'm using Java

Java is a programming language used to build many types of applications, including web applications. It is required for tools like Maven to work properly. Without Java installed, we cannot build or run our Java web app.

We are using Java in this project because our web application is built using Java. Maven needs Java to generate and build the web app. Without Java, we cannot run Maven or our application.

---

## Create the Application

### What I did in this step

In this step, I will create the Web Application inside our EC2 instance using Maven and Java.

### Creating the Java web app

I created a Java web app using the mvn archetype:generate command. This command uses a Maven web app template to generate the project structure automatically. Maven set up all required folders and files without manual input.

### Installing Remote - SSH

I installed Remote - SSH to connect VS Code directly to my EC2 instance. This allows me to browse, edit, and manage files on the EC2 server using VS Code’s IDE features. It makes editing my Java web app easier than using only the terminal.

### SSH configuration details

The configuration file contained the Host name (EC2 Public IPv4 DNS). It included the IdentityFile path pointing to my .pem private key. It also specified the User (ec2-user) to connect to the EC2 instance.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-vscode_2939cf01)

---

## Create the Application

### Exploring the project structure

With VS Code’s file explorer, I could see the full project structure of the Java web app. This included the src folder with webapp and resources subfolders, and the pom.xml file. All these files together define how the web application is built and runs.

src (source) folder contains all the source code of the web application. webapp folder (inside src) holds the web files like JSP, HTML, CSS, and JavaScript. These files define how the web app looks and behaves in the browser.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-vscode_45f91fd7)

---

## Using Remote - SSH

### What I did in this step

In this step, I will connect VS Code directly to my EC2 instance because SSH in the terminal alone does not provide IDE features. I will install a VS Code extension to browse and edit files on the EC2 server. This allows me to view and modify my Java web app files easily.

### Updating the web app

index.jsp is a file used in Java web applications to display web pages. It is similar to HTML but can also contain Java code. This allows the page content to be dynamic instead of static like normal HTML.

I opened the index.jsp file using VS Code’s file explorer. Edited the code directly in the VS Code editor. Saved the changes using Command + S.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-vscode_7a1de541)

---

## Using nano

### Additional improvements

In this secret mission, I will edit the index.jsp using the terminal instead of an IDE (i.e, VS Code)

### Terminal vs IDE

I navigated to the project folder in the terminal using cd and ls. I moved to the webapp directory where index.jsp is located. Then I opened the file in the terminal using nano index.jsp.

Editing code in the terminal is basic and uses only the keyboard, which is useful for quick changes on a server. An IDE like VS Code makes editing easier with features like file explorer, syntax highlighting, and auto-save. Overall, an IDE is more comfortable and productive, while the terminal is simple and direct.

### Verifying my work

I opened the index.jsp file in the terminal using nano. Edited and saved the file directly from the terminal. Then I checked the same file in VS Code Remote-SSH and saw the updated content.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-vscode_a3324ad41)

---

---

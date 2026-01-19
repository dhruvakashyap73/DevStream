<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Secure Packages with CodeArtifact

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codeartifact-updated)

**Author:** Dhruva Kashyap  
**Email:** dhruvakashyap73@gmail.com

---

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-codeartifact-updated_1d79e699)

---

## Introducing Today's Project!

We are setting up AWS CodeArtifact to securely store and manage the project’s dependencies. IAM roles and permissions are configured so the web app can access these packages safely. The connection is verified, and packages are uploaded to integrate CodeArtifact into the CI/CD pipeline.

### Key tools and concepts

In this project, I learned how AWS CodeArtifact is used to securely store, manage, and distribute application dependencies and custom packages. I also gained hands-on experience with AWS Identity and Access Management (IAM) roles and policies to grant secure, temporary access to AWS services from an EC2 instance. Additionally, I understood how Maven integrates with CodeArtifact using configuration files and authorization tokens to enable controlled, reliable builds within a CI/CD pipeline.

### Project reflection

This project took approximately 2 to 2.5 hours to complete. During this time, I set up dependency management using CodeArtifact, configured IAM roles and permissions, and verified the full package lifecycle. The hands-on steps helped reinforce both security and CI/CD concepts in a practical environment.

I will work on the next project the following day as part of continuing the CI/CD learning series. This steady progression helps reinforce concepts by building on previous work. It also allows time to review and apply lessons learned before moving forward.

---

## CodeArtifact Repository

AWS CodeArtifact is a managed artifact repository used to store and manage software packages and dependencies. It provides a secure and centralized place for teams to retrieve packages. This improves security, reliability, and control over dependency versions.

A domain in AWS CodeArtifact acts as a central container for multiple repositories. It allows permissions and security policies to be managed in one place. This ensures consistent access control across all repositories within the domain.

The upstream repository used is Maven Central Repository, configured as maven-central-store. It acts as a trusted public source for Java dependencies not found in the local repository. These packages are fetched once and cached securely in AWS CodeArtifact for future builds.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-codeartifact-updated_n4o5p6q7)

---

## CodeArtifact Security

### Issue

An authorization token is required to securely authenticate access to AWS CodeArtifact. It proves that the EC2 instance and tools like Maven have permission to access the repository. This prevents unauthorized users or services from downloading or uploading packages.

### Resolution

The permissions error was resolved by attaching the correct IAM role to the Amazon EC2 instance, which granted it access to AWS CodeArtifact. After allowing time for the role to propagate, the authorization token command was re-run successfully. This confirmed that the instance could now securely authenticate and access CodeArtifact using temporary credentials.

Using IAM roles is considered a security best practice because they provide temporary, automatically rotated credentials instead of long-term access keys. This allows services like Amazon EC2 to securely access other AWS services without storing sensitive credentials in code or configuration files. IAM roles also support the principle of least privilege, ensuring that resources have only the permissions they actually need.

---

## The JSON policy attached to my role

This IAM policy, which is written in JSON, grants permission to authenticate with and read packages from AWS CodeArtifact. It allows fetching authorization tokens and repository endpoints so Maven can access dependencies. The STS permission enables temporary, secure access specifically for CodeArtifact operations, following least-privilege principles.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-codeartifact-updated_23rp7q8r9)

---

## Maven and CodeArtifact

### To test the connection between Maven and CodeArtifact, I compiled my web app using settings.xml

The settings.xml file configures Maven with the repository URLs, authentication tokens, and rules required to connect to AWS CodeArtifact. It tells Maven where to fetch dependencies from and how to securely authenticate using the authorization token. This setup ensures that all dependency downloads are routed through CodeArtifact in a consistent and secure manner.

Compiling is the process of converting the project’s source code into a format that the system can execute. It validates that the code and dependencies are correctly configured and work together as expected. This step ensures the application is ready to be built and run without errors.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-codeartifact-updated_c17eace8)

---

## Verify Connection

After compiling the web app, the AWS CodeArtifact repository named nextwork-devops-cicd was checked in the console. The repository displayed a list of Maven packages that were automatically added during the build process. These packages confirmed that Maven successfully fetched dependencies via CodeArtifact and cached them from the upstream repository.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-codeartifact-updated_1d79e699)

---

## Uploading My Own Packages

This task focuses on creating and publishing a custom package to AWS CodeArtifact. It demonstrates how organizations manage and distribute internal libraries that are not meant for public repositories. By publishing and consuming a custom package, the complete lifecycle of enterprise package management is understood.

I generated my own package by first creating a simple text file containing a custom message using a shell command. That file was then bundled and compressed into a single archive using a tar.gz format to simulate a distributable package. Finally, a Security hash (SHA256) was generated for the archive to ensure its integrity before publishing it to the repository.

The AWS CodeArtifact console displays the published package name, version number, and namespace within the selected repository. It also shows metadata such as the publish time, package origin, and the repository where it is stored. Additionally, the package details include asset information like file name and SHA256 hash, confirming the integrity of the uploaded package.

I validated the package by downloading it from AWS CodeArtifact using the AWS CLI and confirming a successful retrieval response. The downloaded archive was extracted to verify that the contents matched the originally published file. Finally, reading the file contents confirmed that the package was intact and correctly managed through the publish-and-consume lifecycle.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-codeartifact-updated_sm12-upload)

---

---

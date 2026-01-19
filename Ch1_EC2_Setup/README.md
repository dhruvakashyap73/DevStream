# 📌 Chapter 1: Set Up a Cloud Development Environment (EC2)

![Status](https://img.shields.io/badge/Status-Complete-brightgreen) ![Difficulty](https://img.shields.io/badge/Difficulty-Beginner-blue) ![AWS](https://img.shields.io/badge/AWS-EC2-orange) ![Tools](https://img.shields.io/badge/Tools-Maven%20%7C%20Java-red)

---

## 🎯 Aim / Goal

The goal of this chapter is to set up a complete cloud-based development environment using an Amazon EC2 instance. This environment will be used to build and manage a Java web application completely on the cloud, and it will act as the foundation for the upcoming CI/CD phases.

---

## 🏗️ Architecture (Chapter-Specific Diagram)


Local system connects securely to EC2 using SSH, installs required build tools (Maven + Java), and generates the web project on the server.

---

## ✅ Pre-requisites

Since this is Chapter 1, there are no previous chapters required. However, ensure the following setup is completed in this phase:

- ✅ AWS account access available
- ✅ IAM user created and used instead of root user (recommended best practice)
- ✅ EC2 Instance created and running
- ✅ Key Pair (.pem) created and stored safely
- ✅ Security Group allows SSH access (Port 22) only from your IP
- ✅ VS Code installed on local machine
- ✅ Remote-SSH extension installed and connected
- ✅ Maven + Java installed on EC2
- ✅ Web app generated successfully (BUILD SUCCESS)

---

## 🧰 Tech Stack Used

| Tool | Version/Details |
|------|-----------------|
| **AWS IAM** | IAM Admin User |
| **Amazon EC2** | Amazon Linux 2023 AMI |
| **SSH** | Secure remote login (Port 22) |
| **VS Code** | IDE (Local) |
| **Remote - SSH Extension** | VS Code plugin |
| **Apache Maven** | Build tool |
| **Amazon Corretto 8** | Java 8 Runtime |
| **Nano Editor** | Terminal editor |

---

## 🛠️ Step-by-Step Implementation

### ✅ Step 1: Log in using IAM User (not root)

**Action Items:**
1. Create IAM user:
   - Username: `IAM-Admin`
   - Permissions: `AdministratorAccess`
   - Download `.csv` file with login details
2. Login using IAM Admin user from Console Sign-In URL

**📸 Screenshots to include:**
- [ ] IAM user created successfully
- [ ] Logged in using IAM user

---

### ✅ Step 2: Launch an EC2 Instance

**Action Items:**
1. Go to EC2 → Instances → Launch Instances
2. Configure:
   - **Name:** `nextwork-devops-`
   - **AMI:** Amazon Linux 2023
   - **Instance Type:** `t2.micro`
3. Create Key Pair:
   - **Name:** `nextwork-keypair`
   - **Type:** RSA
   - **Format:** .pem
4. Network Settings:
   - Allow SSH from: **My IP**

**📸 Screenshots to include:**
- [ ] EC2 instance running
- [ ] Key pair created
- [ ] Security group rules (SSH from My IP)

---

### ✅ Step 3: Store .pem File and Update Permissions

**Action Items:**
1. Create a folder on desktop: `DevOps`
2. Move `nextwork-keypair.pem` into: `~/Desktop/DevOps/`
3. Run inside VS Code terminal:

```bash
cd ~/Desktop/DevOps
ls
chmod 400 nextwork-keypair.pem
```

**📸 Screenshots to include:**
- [ ] .pem present inside DevOps folder
- [ ] `chmod` command output

**🔧 Troubleshooting:**
> **Error:** Permission denied (publickey)
> 
> **Fix Checklist:**
> - Confirm .pem file name matches
> - Ensure permissions are correct: `chmod 400 nextwork-keypair.pem`
> - Verify Security Group allows SSH (port 22) from your IP
> - If your IP changed, update inbound rule

---

### ✅ Step 4: Connect to EC2 via SSH

**Action Items:**
1. Copy EC2 Public IPv4 DNS
2. Run this command:

```bash
ssh -i ~/Desktop/DevOps/nextwork-keypair.pem ec2-user@<YOUR_PUBLIC_IPV4_DNS>
```

3. Type `yes` when prompted.

**📸 Screenshots to include:**
- [ ] Successful SSH connection showing `ec2-user@...`

**🔧 Troubleshooting:**
> **Error:** Operation timed out
> 
> **Fix Checklist:**
> - Check instance is running
> - Confirm security group SSH rule
> - Confirm correct IP address is allowed

---

### ✅ Step 5: Install Apache Maven on EC2

**Action Items:**
Run the following commands:

```bash
wget https://archive.apache.org/dist/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz
sudo tar -xzf apache-maven-3.5.2-bin.tar.gz -C /opt
echo "export PATH=/opt/apache-maven-3.5.2/bin:$PATH" >> ~/.bashrc
source ~/.bashrc
```

**If wget is missing:**
```bash
sudo yum install wget -y
```

**📸 Screenshots to include:**
- [ ] Maven installation commands executed

---

### ✅ Step 6: Install Java 8 (Amazon Corretto 8)

**Action Items:**
Run the following commands:

```bash
sudo dnf install -y java-1.8.0-amazon-corretto-devel
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64
export PATH=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64/jre/bin/:$PATH
```

**📸 Screenshots to include:**
- [ ] Java installation output

---

### ✅ Step 7: Verify Installations

**Action Items:**
Run:

```bash
mvn -v
java -version
```

**🔧 Troubleshooting (Java version mismatch):**
```bash
sudo alternatives --config java
```

**📸 Screenshots to include:**
- [ ] Maven version output
- [ ] Java version output showing `1.8`

---

### ✅ Step 8: Generate Java Web App Using Maven

**Action Items:**
Run:

```bash
mvn archetype:generate \
   -DgroupId=com.nextwork.app \
   -DartifactId=nextwork-web-project \
   -DarchetypeArtifactId=maven-archetype-webapp \
   -DinteractiveMode=false
```

**Expected Output:** `BUILD SUCCESS`

**📸 Screenshots to include:**
- [ ] BUILD SUCCESS message

---

### ✅ Step 9: Connect VS Code to EC2 (Remote SSH)

**Action Items:**
1. Install extension: **Remote - SSH**
2. Add SSH host:
```
ssh -i ~/Desktop/DevOps/nextwork-keypair.pem ec2-user@<YOUR_PUBLIC_IPV4_DNS>
```
3. Open folder in remote session: `/home/ec2-user/nextwork-web-project`

**📸 Screenshots to include:**
- [ ] Remote SSH connected (bottom left shows SSH)
- [ ] Project opened in VS Code explorer

---

### ✅ Step 10: Edit index.jsp from VS Code

**Action Items:**
1. Open `index.jsp` in VS Code
2. Replace content with:

```html
<html>
<body>
<h2>Hello !</h2>
<p>This is my NextWork web application working!</p>
</body>
</html>
```

3. Save using: `Ctrl + S` / `Cmd + S`

**📸 Screenshots to include:**
- [ ] Updated `index.jsp` file

---

### ✅ Step 11 (Secret Mission): Edit index.jsp using Terminal (Nano)

**Action Items:**
1. Navigate to:
```bash
cd ~/nextwork-web-project/src/main/webapp
nano index.jsp
```

2. Add this line to the file:
```html
<p>I am writing this line using nano instead of an IDE.</p>
```

3. Save + Exit:
   - `Ctrl + S`
   - `Ctrl + X`

**📸 Screenshots to include:**
- [ ] Nano editor screen
- [ ] Final file showing the new line

---

## ✅ Outputs

By the end of this chapter, the following outputs are achieved:

- ✅ IAM Admin user created and used successfully
- ✅ EC2 instance launched and running
- ✅ Secure SSH connection established from local system to EC2
- ✅ VS Code installed and connected to EC2 via Remote SSH
- ✅ Apache Maven installed and verified (`mvn -v`)
- ✅ Java 8 (Amazon Corretto 8) installed and verified (`java -version`)
- ✅ Java web app generated successfully using Maven (BUILD SUCCESS)
- ✅ `index.jsp` edited using both VS Code IDE + nano (terminal editor)

---

## 📚 Key Takeaways

1. **Cloud Development Environment Setup:** Established a complete development environment on AWS EC2
2. **Infrastructure as Code Mindset:** Used cloud services for scalable development
3. **SSH Security:** Practiced secure remote connection using key pairs
4. **Build Tools Mastery:** Installed and configured Maven and Java
5. **Web Application Generation:** Created a Maven-based Java web project from archetypes

---

## 🔗 Navigation

| Previous | Current | Next |
|----------|---------|------|
| — | **Chapter 1: EC2 Setup** | [Chapter 2: Build & Deploy](../Ch2_BuildAndDeploy/README.md) |

---

## 📝 Notes

- Always use IAM users instead of root account for security best practices
- Store your `.pem` file securely and never commit it to version control
- Monitor AWS costs by stopping EC2 instances when not in use
- Update security groups based on your current IP address for SSH access

---

**Last Updated:** January 19, 2026  
**Status:** Complete ✅  
**Difficulty Level:** Beginner 🟢

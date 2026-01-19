# Infrastructure as Code with CloudFormation

**Author:** Dhruva Kashyap  
**Email:** dhruvakashyap73@gmail.com

---

---

## Introducing Today's Project!

The goal is to use AWS CloudFormation to define the CI/CD infrastructure as code instead of setting it up manually in the console. This includes rebuilding the required resources in a consistent and repeatable way using templates. By converting the pipeline setup into code, the infrastructure becomes easier to automate, reuse, and manage with fewer configuration errors.

### Key tools and concepts

### Project reflection

---

## Generating a CloudFormation Template

IaC Generator scans your AWS account and discovers the existing resources like EC2, S3, and IAM that you’ve already created. It then automatically generates a CloudFormation template (code) for the resources you select, so you don’t need to write the template from scratch. This makes Infrastructure as Code faster, easier, and more reliable for deploying and managing the same setup again.

A CloudFormation template is a code file (YAML/JSON) that describes all the AWS resources we want to create and manage, like S3 buckets, IAM roles, and CodeDeploy applications. It is used so we can deploy the same infrastructure quickly and consistently by creating a CloudFormation stack instead of doing everything manually. This supports Infrastructure as Code (IaC) by making our setup repeatable, reusable, and easy to update or delete.

Some resources could not be added using the IaC Generator, such as the CodeBuild project and the CodeDeploy deployment group. This is because they need specific configuration details like build environment settings and deployment configurations that the generator cannot auto-capture. So, these resources must be added manually into the CloudFormation template later.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-cloudformation-updated_0495b046)

---

## Template Testing

Before deploying new resources, we deleted all the existing CI/CD resources like CodeDeploy, CodeBuild, CodeArtifact domain/repositories, IAM roles and policies, the EC2 instance, and the S3 bucket. This was done because CloudFormation deployment will fail if resources with the same names already exist in the AWS account. Clearing them ensured the template could recreate everything cleanly and avoid name conflicts during deployment.

The first template test failed because CloudFormation could not find the IAM role codebuild-nextwork-web-build-service-role while trying to attach policies to it. This happened because CloudFormation attempted to create the role and attach the policies at the same time, so the role wasn’t fully created yet when the policies referenced it. As a result, the stack rolled back and deleted the newly created resources to keep the account clean.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-cloudformation-updated_f56730fd)

---

## DependsOn

Adding the DependsOn attribute forced CloudFormation to create the IAM role first before creating and attaching the IAM policies. This fixed the error where policies failed because the role did not exist yet during stack creation. As a result, the template deployment became properly ordered and could proceed successfully without that dependency failure.

We added the DependsOn line inside each of the four IAM ManagedPolicy resources in the CloudFormation template that start with IAMManagedPolicy00policyservicerole.... This ensures these policies wait until the CodeBuild service IAM role is created before being attached. We also added a similar DependsOn to the CodeArtifact consumer policy so it waits for the EC2 CodeArtifact access role to exist first.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-cloudformation-updated_f0df8018)

---

## Circular Dependencies

The new error was a circular dependency issue in the CloudFormation template. This happened because the IAM policies were set to depend on the IAM role being created first, while the IAM role also indirectly depended on those policies, creating a loop. As a result, CloudFormation could not decide the correct creation order and the stack deployment failed.

We fixed the CloudFormation template by removing the circular dependency inside the CodeBuild IAM role configuration. Specifically, we deleted the ManagedPolicyArns references that were pointing to the IAM policies, because the policies were already depending on the role using DependsOn. After removing those lines and saving the template, CloudFormation could create the role first and attach the policies without getting stuck in a dependency loop.

![Image](http://learn.nextwork.org/easygoing_azure_noble_spider/uploads/aws-devops-cloudformation-updated_e6fd85ed)

---

## Manual Additions

---

## Success!

---

---

What if I told you that a text file could help you tackle the normally tedious and time-consuming task of setting up and managing your AWS infrastructure? Good news. It’s actually easy to do with an **AWS CloudFormation template**.

A typical AWS infrastructure can consist of numerous resources that might need to be managed across different accounts and regions. Setup is often a manual process that can be overwhelming to maintain. This is especially true if your **AWS infrastructure** continues to grow and you have to start from scratch each time you need to add new resources or services. The one-off, ad hoc nature of provisioning resources via the CLI or management console also leaves too much room for error.

Luckily, AWS CloudFormation was built to solve these issues. It simplifies the management of your AWS infrastructure, by allowing you to create text-file templates that provision and update resources in an organized and predictable way. CloudFormation is well-established, with more than 10 years since launch, and has the support of a large community.

In this article, we’ll cover the benefits and potential drawbacks of CloudFormation and how to **setup** and **modify** your **architecture with templates**. We’ll also share CloudFormation template examples that can make things even easier. By adopting AWS CloudFormation, you and your team will spend far less time building and managing your infrastructure, so you can stay focused on development.

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qs17w3187jhp1g5mpnhf.png)
 

My Background: Cloud Engineer | AWS Community Builder | AWS Educate Cloud Ambassador | 4x AWS Certified | 3x OCI Certified | 3x Azure Certified.


**The Introduction to AWS Services** is a mini Series containing different articles that provide a basic introduction to different aws services. Each article covers the detailed guide on how to Use the AWS Service. This series aims at providing "A Getting Started Guide on Different AWS Services."

# AWS CloudFormation

**AWS CloudFormation** performs the crazy party trick of enabling you to manage your complete AWS infrastructure and resources from a text file. The formatted YAML or JSON code you write in the AWS CloudFormation template describes your AWS infrastructure and the resources you need. CloudFormation does the rest, provisioning, configuring and deploying everything for you. It also handles dependencies between resources, removing another piece of complexity from the puzzle.

Without a template, you would have to set everything up manually using the AWS management console or CLI. You would also have to make note of all the resources involved, especially if you wanted to replicate your work for another environment. On the other hand, templates can be used on an ongoing basis, moving you away from the tedium of manually executing multiple steps every time you need to make a change. For example, extending your environment by adding a few more functions is easy with a template.

# Understanding CloudFormation Stacks

The collection of AWS resources created when CloudFormation runs a template is called a stack. The resources that make up a stack are provisioned to work together to build your application or solution. You can create, modify, delete or replicate resources at the stack level, making management easier and more organized.

Here are a few of the many advantages that come with defining your resources with AWS CloudFormation templates and managing them as stacks:

## Use existing CloudFormation templates so you don’t have to start from scratch

Chances are you’ll need similar sets of resources for several different environments. With AWS CloudFormation templates, the days of having to start from scratch each time are over. Instead, lean on an existing template to replicate the infrastructure you need. You can then customize your setup using CloudFormation template parameters and conditions (more on that later). In this way, you can quickly set up resources in multiple environments and in different regions around the world. The portable nature of templates also allows you to share them, say with other teams in your organization, when it makes sense.

## Stacks are easier to QA

With your infrastructure declared by the code in your templates, you can now add reviews to your process to ensure no mistakes are made during deployment. You can also use a change management process to verify any changes to your infrastructure, instead of risking mistakes by making changes directly in the console or via CLI.

## CloudFormation is the largest resource provider

CloudFormation has many more features you can explore, including built-in identity and access management (IAM), automated rollback and error-checking. And after lagging in resource coverage in the past, CloudFormation now covers more AWS resources than any other Infrastructure-as-Code framework, including Terraform, and almost all new AWS releases now have CloudFormation coverage at launch.

Of course, nothing is perfect and AWS CloudFormation does have some drawbacks. Here are a couple to keep in mind:

**Steep learning curve:** While working with templates creates more predictable results than working directly with the console, CloudFormation has many concepts to learn, and, until you get a firm handle on them, things can easily go wrong. For example, if you change the logical ID of a resource, CloudFormation will delete it and create a new one. And, when it deletes that resource, it also trashes its data. Similarly, a resource and all its content are often automatically deleted when the stack is deleted, unless you specify otherwise using the DeletionPolicy attribute in your template. 

**Beware of drift:** CloudFormation keeps a snapshot of the current state of your AWS infrastructure. If you then make a change directly through your AWS console or your AWS CLI, your resources will be out of sync with the snapshot. This discrepancy is called drift and it can cause your deployments to fail. 
So, once you start using CloudFormation, you should stop making manual updates to your account, through the console or CLI, to avoid this issue.

## What Are the Basic CloudFormation Template Sections?

As mentioned earlier, an AWS CloudFormation template is simply a formatted YAML or JSON text file. Next, we’ll cover the 9 main sections used in a template to define and modify the resources you need.

## Format version

This is where you specify the template format version. The capabilities of the template can vary depending on which one you choose. If you don’t pick one, CloudFormation defaults to the latest version. As an aside, CloudFormation has yet to make a backwards-incompatible change, so don’t worry too much about versions.

## Description

Use the description area to add comments about your template, such as its purpose.

## Metadata

Use JSON or YAML objects in this section to provide further details about the resources in your template.

## Parameters

In this section, you declare parameters that are passed to the template when a stack is created or updated. In this way, you can specify unique values for use in the properties of your stack’s resources and effectively customize a template each time it’s used. It also allows you to use a single template across multiple accounts and regions, or to specify information unique to the application or configuration being deployed. A best practice is to store parameters in AWS Systems Manager Parameter Store for each environment and then reference the parameters instead of passing in literal values to CloudFormation directly.

## Mappings

There may be cases where you’ll want to add logic to your template. With Mappings, you can use an input value as a condition that determines another value.

## Conditions

Conditions are statements that determine whether or not a resource is created or a property is assigned to a value when a stack is created or updated. For example, a condition could check to see if one value is greater or less than another value and, based on the result, conditionally create a resource. This gives the same template the flexibility to be used across different environments.

## Transform

You can specify one or more macros that enable the reuse of template components. They are often used to condense or simplify your code. This is where you enable AWS SAM, which is used to simplify the development of serverless stacks.

## Resources

This is where you list the resources that will be created by the template. It’s also where you specify the necessary properties to create each resource.

## Output

In this section, you can specify the values you want to have returned to you and available after the stack is created. For example, there could be output values you might need to have handy to import into other stacks or you might want easy access to a particular output, like a URL created in the template.

> To see examples of these template sections in actual code, take a look at the CloudFormation Sample Templates part of the article.

# Best Practices when Creating CloudFormation Templates

**Leave credentials out of your templates:** It’s not a smart move to store credentials or other sensitive information in your AWS CloudFormation templates. Instead, use dynamic references to specify and retrieve information managed in other services, like AWS Secrets Manager, without CloudFormation ever storing the actual reference value.

**Reference non-confidential parameters:** It’s a good idea to store non-confidential parameters (like the memory size of a Lambda Function) in AWS Systems Manager Parameter Store and reference them, instead of passing literal values to CloudFormation directly.

**Make your code more readable:** If you’re writing your AWS CloudFormation template in YAML, use CFN-specific tags (e.g. !GetAtt instead of the full Fn::GetAtt syntax) to make your code more readable. You’ll thank yourself later when you revisit your code.

**Add comments and background information:** With a top-level Metadata section and the ability to add Metadata sections to every resource, you have plenty of opportunities to provide details that could be helpful later. And don’t worry, these comments won't be lost when you use tools to edit your templates.

**Check your code:** Validate your template with AWS CloudFormation, before creating or updating a stack, to ensure it consists of valid JSON or YAML without syntax or semantic errors. Also make sure to use tools like AWS CloudFormation Guard (cfn-guard) and cfn-nag to check your template for policy compliance issues or security vulnerabilities, respectively.

# CloudFormation Sample Templates

Take a look at these AWS CloudFormation template examples to get a feel for what they’re like.

Services templates:

[Auto Scaling template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/sample-templates-services-us-west-2.html#w2ab1c35c58c13b7)
[Amazon EC2 template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/sample-templates-services-us-west-2.html#w2ab1c35c58c13c17)
[Elastic Load Balancing template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/sample-templates-services-us-west-2.html#w2ab1c35c58c13c23)
[Explore more AWS services templates.](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/sample-templates-services-us-west-2.html)

### Application framework templates:

[Basic LAMP stack template](https://s3.us-west-2.amazonaws.com/cloudformation-templates-us-west-2/LAMP_Single_Instance.template)
[Basic Ruby on Rails template](https://s3.us-west-2.amazonaws.com/cloudformation-templates-us-west-2/Rails_Single_Instance.template)
[Check out more application framework templates.](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/sample-templates-appframeworks-us-west-2.html)

### Template snippets:

[These template snippets can help you learn.](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/CHAP_TemplateQuickRef.html)

### More AWS templates and resources:

[Take a look at the AWS CloudFormation templates page for more samples and resources.](https://aws.amazon.com/cloudformation/resources/templates/)

# Conclusion

AWS CloudFormation gives you an easy way to model a collection of related AWS and third-party resources, provision them quickly and consistently, and manage them throughout their lifecycles, by treating infrastructure as code. 

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rrkgdjdxha4xvqa5aucx.png)

---

Hope this guide helps you understand on How to Get Started With AWS Cloudformation, feel free to connect with me on [LinkedIn] (https://www.linkedin.com/in/adit-modi-2a4362191/)|[Twitter](https://twitter.com/adi_12_modi).
If you are interested in learning more about AWS Services then follow me on [github.](https://github.com/AditModi)
If you liked this content then do clap and share it . Thank You .
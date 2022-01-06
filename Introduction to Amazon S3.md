Amazon Simple Storage Service, also known as Amazon S3 is an online storage facility. It is cheap, fast and easy to setup. And since it’s a service provided by e-commerce giant Amazon, you can be rest-assured whatever you stored at S3 is secured.

**Amazon S3** is one of the core services and among the pillars of the AWS cloud infrastructure. The S3 stands for **“Simple Storage Service”** and is among the three foundational services that Amazon started with back in 2006. Almost all services in the AWS cloud infrastructure use this service in one way or the other. In simple terms, Amazon S3 is an object store just like a regular file system that you have on your computer but is **“infinitely scaling”** or as AWS advertises it. There’s no limit to the amount of data you can store on s3.

The key features of s3 service are it's **infinite, highly scalable, high availability, high durability, manageable, and secure.** Even with the option of infinite storage, in terms of cost, it is one of the most costly friendly services and you only pay for what you use. It can be used to store all kinds of image, text, and multi-media data.

The article will cover the following sections:
Amazon S3 overview.
* S3 Buckets and Objects overview.
* S3 Advance features.
* S3 popular use cases.

If you’re new to AWS and cloud check out my article summarizing what is cloud and AWS.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/d1kxbvxh0sdaej18ie5k.png)

My Background: I am Cloud , DevOps & Big Data Evangelist | 4x AWS Certified | 3x OCI Certified | 3x Azure Certified | AWS Community Builder | AWS Educate Cloud Ambassador . 

**The Introduction to AWS Services** is a mini Series containing different articles that provide a basic introduction to different aws services. Each article covers the detailed guide on how to Use the AWS Service. This series aims at providing "A Getting Started Guide on Different AWS Services."

## Amazon S3 overview

Amazon S3 is designed to allow users to build highly scalable applications with infinite but inexpensive storage. S3 being a fast, inexpensive, and reliable option allows it to be used as a backbone for a large number of cloud-based applications and is also an integral service in the AWS cloud infrastructure with integration options available for most of the services. Users can store or retrieve any amount of data as per their needs at any time of day from around the globe.

In S3, everything is stored like an object which is mainly used for storing text-based data like server logs or multi-media data like images, videos, or mp3 files. The data is stored with **99.99% availability** which sums to just 53 mins of downtime in a year and 99.999999999% durability which means that a single object is lost every 10,000 years. The service can be easily accessed via the management console providing the users with a well built and easy to use interface to easily manage all the different features and options. In addition to the console, the AWS CLI and SDKs for S3 are also available for more programmatic access.

Some more advanced features that S3 offers are **object encryption for data security, versioning and replication for backup and durability**, storage classes for cost optimization based on object access patterns, auditing, monitoring, and compliance features, permissions, and access management at the user, bucket, and even object level for restricted access, query in-place support for other AWS services to allow direct query on the objects.
We’ll cover most of the details of these features in the coming sections.

## S3 Buckets and Objects overview

With a general overview of the S3 service, we can dig into how the objects are structured in the S3 service. S3 follows the convention of buckets and objects.

## Buckets:

A bucket in S3 is just like a directory that contains an unlimited number of objects(files). Each account can have 100 buckets(soft limit and can be increased by request to AWS) by default but there's no cap on the number of objects in one bucket but each object can only be 5TB in size.

S3 is a regional service and buckets are saved at the regional level. Each bucket has a globally unique name (bucket names follow a convention)meaning that only one bucket can have a given name at a time in the entire AWS infrastructure unless deleted by the bucket owner. Buckets are created in a specific region that we choose so choosing geographically closer regions can help minimize latency.

## Objects:

An object in S3 is just a file you store. Ojects consists of data and metadata. Each object has a unique key that consists of a prefix and the object name.
E.g. s3://s3bucket/some_folder/s3_object.txt

The bucket name, key, version ID, and the object name itself all together uniquely identify the object. Although I mentioned earlier that buckets are like directories and even the UI on the management console will show a directory structure, there’s no concept of directories within buckets nor do any directories exists like in a Linux file system. 

The directories in buckets are only there for data organization purposes. S3 works entirely with keys. S3 objects can be 5TB in size but unlimited in number. Objects also have additional attributes like metadata, version, and tags.

## Objects Consistency Model

The S3 service due to its high availability and durability provides atomic updates to objects meaning the objects are never partially updated. The consistency model for S3 is based on two approaches:

**Read after write consistency for new objects** — means that if we request new objects right after creation, S3 might return 404 but eventually the objects become available.

**Eventual Consistency for objects overwrites** — If an object is retrieved right after the update, S3 might return the old copy or the new one but never a partially updated object.

**Buckets, objects, and keys** together make up the entire working structure of the S3 service. The advanced features for buckets and objects are discussed in the next section.

## S3 Advance features.

S3 although being a very foundational service offers many advanced features that are listed as follows:

#### S3 Storage Classes and Life Cycle Management

Not all objects in a bucket have the same access patterns some are accessed more frequently than the others. Considering this, the S3 service allows objects to be transitioned into different storage classes depending upon their access patterns to help reduce the cost of storage. This can be either done manually via the management console or the SDKs or we can set life cycle configuration on buckets to transition objects in a different storage class.

## Storage Classes

S3 offers a range of different storage classes that can be used depending upon the S3 popular use cases. object's access patterns.

**S3 Standard** — This is the default storage class for all objects. This storage class is suitable for frequently accessed objects (such as images)and for performance-sensitive use cases.

**S3 Reduced Redundancy Storage(RRS)**— This storage class is also for the frequently accessed objects but more suitable for non-critical data that are easily reproducible if lost. AWS recommends not using RRS.

**S3 Intelligent-Tiering** — This storage class is suitable for use cases when want to automatically optimize the storage costs. Depending upon the changes in object access patterns, the S3 Intelligent-Tiering moves data automatically to a frequent access tier or low-cost infrequent access tier. A small monthly automation and monitoring fee is associated with each object for this storage class. 
No additional tiering fee or object retrieval fees are associated with this storage class. Ideal for use cases having long-lived data with unknown and unpredictable access patterns.

**S3 Standard-IA and S3 One Zone-IA** — These storage classes are suitable for long-lived infrequently accessed objects such as backup files. The objects are available at millisecond access times but an object retrival fee is associated with these storage classes. 

The difference between S3 Standard-IA and S3 One Zone-IA is that the former stores data across multiple availability zones redundantly while the latter stores data in only one AZ. 

Hence One Zone-IA is less expensive but less resilient and available and prone to the physical loss of data compared to Standard-IA.

**S3 Glacier and S3 Glacier Deep Archive** — These storage classes are suitable for archiving data and have the least cost from all of the above storage classes. Data in Glacier and Deep Glacier Archive is not readily available and data retrival can take from 1 minute to 12 hours in the case of Glacier and about 12 hours in the case of Deep Glacier Archive. These storage classes are suitable for data that needs to rarely need to be accessed.
A detailed analysis of S3 storage classes by AWS is given below:

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9vttt9wh9i1u5i3nwuuo.png)
 

## S3 Storage Classes Comparison

For more details on S3 storage classes visit the S3 documentation.

Life Cycle Management

S3 provides transitioning of objects into different storage classes as per the need to reduce costs. We set the life cycle configuration(a set of rules) that is applied to the objects. S3 performs the actions as in the configurations. Two types of actions are performed:

**Transition actions** — These actions transition objects from one storage class to the other after a specified time interval e.g. after 7 days or 15 days etc. Additional costs are associated with life cycle transition requests.

**Expiration actions** — These actions delete the objects after the specified interval.

For the configuration of life cycle management, we can either set it on a bucket via the management console or we can provide an excel document having predefined actions(stored as an S3 sub-resource) to be performed on objects via API operations.

For more details on S3 life cycle management visit the [S3 documentation.](https://www.google.com/aclk?sa=L&ai=DChcSEwjtnuS73unvAhVHDCsKHSmEAEYYABAAGgJzZg&ae=2&sig=AOD64_2s39eC24U7dzTsQdskRQR6LMgmUQ&q&adurl&ved=2ahUKEwj-vNy73unvAhWQ7HMBHZ3IAA4Q0Qx6BAgDEAE)

## S3 Object Versioning

Another cool feature the S3 service provides is **object versioning**. Versions is enabled at bucket level and buckets with versioning enabled(disabled by default) have a version ID( auto-generated and noneditable) attached with each S3 object in that bucket. Objects present before versioning is enabled are assigned a null version ID while new objects each have a unique version ID. **S3 versioning** allows us to store multiple versions of an object and prevents the accidental deletions and overwrites of an object. Can also be used for archival purposes. The following images show the behavior of versioning for overwrites and delete:

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/srbafmxl0hj0zb9en5rz.png)
 

The original version always remains in the bucket while a new copy of the same object is placed with a new and unique version ID that becomes the current version. 

For deletes, a delete marker is placed on the object deleted but in actual it is never deleted and S3 returns a 404 error if the deleted object is retrieved. 

For permanently deleting the object, version ID has to be passed along the request which deletes the current version and sets the current version to the next most recent version.

## S3 Replication

S3 replication allows objects of one bucket to be copied to another bucket with the same or a different AWS account and within the same or a different region. We configure object replication by providing a replication configuration to the source bucket consists of at least the destination bucket and IAM role for S3 to copy the objects.

For **objects replication**, we have **cross-region object replication (CRR)** and same **region object replication (SRR)**. Other than data redundancy purposes we can use S3 replication for various use cases such as:

Replication of objects with different storage classes.
Object replication with different ownership.

S3 Replication Time Control (S3 RTC) to copy 99.99% objects within the same or a different region in 15mins or less.

Some vital considerations we must consider are: object versioning must be enabled for source and destination buckets for replication. 
All objects present before the replication configuration is set for the bucket are not copied and we have to contact AWS support for their replication.

## S3 Security and Encryption

#### Security

S3 durability and reliability are one of its most attractive features providing 99.999999999% (eleven 9s)durability and 99.99% availability. Along with a highly secure and fault-tolerant infrastructure provided by AWS data in S3 is replicated across multiple availability zones to sustain the concurrent loss of data in two AZs.

S3 also provides user-based and resource-based security options to restrict access to specific users, buckets, and even objects.
user-based restriction: We can set IAM policies to define specific actions a user can perform on S3.

**resource-based restriction**: Resource-based actions can either be on buckets or objects within buckets for even finer control. These are done via **bucket policies** and **access control lists (ACLs)** respectively. By default, S3 buckets are private and we specifically allow pubic access on the bucket and objects via the bucket policies and ACLs respectively.

## Encryption

Data in S3 can be made more secure using the encryption options available in S3. Encryption can be either:
**Server-Side** — Unencrypted data is uploaded on S3 and encrypted first before physically stored by S3 and decrypted on access. The keys used for encryption are managed by the S3 service. S3 also provides options for the client to use its own encryption keys in this case as well.

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6kkwla2bd38pddhv9s95.png)
 

**Client-Side** — Data is encrypted at clients' end and uploaded to S3 in encrypted form. The client is responsible for key management in this case.

## S3 popular use cases

Some really popular use case which AWS S3 can be used for can be:
**Data backups**, **data storage**, and **hybrid cloud storage**.
Media such as images, music and videos, application hosting, and Static Website Hosting.
**Data archiving**.
**Data Lakes building and data analytics on data lakes.
Disaster recovery.**

## Summary

The article summarizes the working model of S3 and the various features offered by the service. S3 being a very foundational service can be used for a number of different applications. The features provided in S3 are very lucrative and the cost at which an infinite amount of data can be stored with high durability and accessibility makes it one of the most go-to services for any architecture.

I would love to hear your thoughts about amazon s3. I hope this guide was helpful in understanding more about amazon s3. feel free to contact me on [LinkedIn.](https://www.linkedin.com/in/adit-modi-2a4362191/)
You can view my badges [here.](https://www.youracclaim.com/users/adit-modi/badges)
If you are interested in learning more about AWS then follow me on [github.](https://github.com/AditModi)
If you liked this content then do clap and share it . Thank You .
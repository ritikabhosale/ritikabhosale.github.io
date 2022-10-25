---
title: "S3 Bucket"
date: 2022-10-21T19:03:40+05:30
draft: false
---

**What is S3?**  
S3 is a storage service provided by Amazon AWS. It stands for `Simple Storage Service`. It's an object storage service offering leading scalability, data availability, security and performance. You basically store your virtually on various data centeres provided by Amazon AWS. It optimizes your data boosting the performance and manages it various storage classes which makes it cost effective.

**Benefits**

- performance, scalability, availability
- cost effective - storage classes are available
- security, compliance and auditing capabilities
- manage data and access permissions
- query in place and on demand processing
- widely used cloud storage

S3 bucket contains objects of different shapes and sizes. Firstly, you create a bucket and upload your files into that bucket. A bucket could hold multiple objects of different types (pdf, jpeg, csv, etc). Objects are fundamental entities in bucket. It's like an wrapper over your file. A object consists of data as well as metadata like creation data, size, etc. S3 can also access the metadata associated with the objects, not the actual data. When you store a object in a bucket, the default storage class is `S3 Standard`.

**What are storage classes?**  
Amazon S3 provides a range of storage classes to provide the lowest cost storage for different access patterns. You choose which storage class will be suitable for storing your object based on the frequency of access request. The frequency of access is directly proportional to the cost.

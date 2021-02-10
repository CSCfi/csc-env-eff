---
theme: Allas storage service
lang: en
---


# How to get access to Allas

Use [https://my.csc.fi](https://my.csc.fi) to 
1. Register to CSC (haka)
2. Set up a project at CSC (Principal Investigator)
3. Apply for Puhti and Allas service, quota and billing units for your project
4. Add other registered users to your project
5. Members have to register and accept the services in [https://my.csc.fi](https://my.csc.fi)

All project members have equal access to the data in Puhti and Allas.

# Allas – object storage: what it is for?

*  Allas is new storage service for all computing and cloud services
*  CEPH based object storage
*  Meant for data during project lifetime
*  Default quota 10 TB / Project.
*  Possible to upload data from personal laptops or organizational storage systems into Allas
*  Clients available in Puhti and Mahti
*  Data can also be shared via Internet

# Allas – object storage: what it is for?

*  Data can be moved to and from Allas directly without using Puhti or Mahti.
*  For the computation the data has to be typically copied to a file system in some computer
*  Data can be shared publicly to Internet, which is otherwise not easily possible at CSC.

# Allas – object storage: what it is NOT

*  **Allas is not a file system** (even though many tools try to fool you to think so). It is just a place for a pile of static data objects.
*  **Allas is not a data management environment**. Tools for etc. search, metadata,version control and access management are minimal.
*  **Allas is not a back up service**. Project mebers can delete all the data with just one command.

# Allas - storage 

An object is stored in multiple servers so a disk or server break does not cause data loss.
There is no backup i.e. if a file is deleted, it cannot be recovered
 Data cannot be modified while it is in the object storage –  data is immutable.
Rich set of data management features to be built on top of it, initially S3 and Swift APIs supported



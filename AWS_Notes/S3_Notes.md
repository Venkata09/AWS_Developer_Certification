## Simple Storage Service S3

An AWS account can have upto 100 S3 buckets

No limits on the number of objects stored within a bucket

any kind of data in any format can be stored in s3

S3 is a simple key based object store

S3 in US Standard provided eventual consistency. In all other regions, s3 provided read-after-write consistency for PUTS of new objects and eventual consistency for overwtite PUTS and DELETES

within a region objects are redundantly stored on multiple devices across multiple facilities

Content MD5 and CRC are used to detct data corruption

Cross region replication (CRR) is allowed. Enable it to replicate data across different regions. ofcouse more cost

Event notifications can be setup in s3, messages can be sent out using SNS, SQS or lambda

Reduced redundancy storage is provide RRS. durability is 99.99% vs 99.999999999% of standard s3

if data lost in RRS, then 405 error. Can also setup SNS

S3 can host static website. Bucket name must match domain name for website hosting.

S3 supports own website name or website redirects

Access control in s3 : 4 ways can be used to secure access

IAM policies
bucket policies
ACLs
Query string authentication: can create URL to s3 object which is only valid for certain time
Bucket name restrictions

upper, lowercase letters, numbers periods and dashes
must start and end with letter or number, not period or dash
minimum 3, max 63 characters
cannot be an IP address style name (10.2.2.1)
periods and dashes cannot follow each other
S3 object size

minimum of 1 byte
maximum of 5TB
Object greater than 5G are required to be multipart upload api
largest object using PUT operation is 5G
for greater than 100Mb, you should consider multipart
can upload a file as it is being created,
can start or stop uploads
Must call CompleteMultiPartUpload to reassemble the file

S3 sorts and stores files in lexicographical order - alphabetical order.

So if you are reading or writing many files, then add a random hash in the begining of filename so s3 stores in different partitions. Hence throughput performance increases

S3 allows hosting static HTML

Route 53 can direct your domain to your bucket. But the bucket name needs to match domain name

No subdomains using s3 buckets

URL name .s3-website-.amazonaws.com

Error codes 400-client side error, 500 server side error

404 not found : requesting bucket which does not exist

403 forbidden : accessing bucket for which you do not have permission

400 bad request : invalid bucket state

409 conflict: If you try to delete a bucket that is not empty

500 server : s3 issue

CORS Cross Origin Resource Sharing

in order to load resource from another bucket, you have to enable CORS
In the resource bucket add CORSconfiguration and add CORSRule and specify the AllowedOrigin and AllowedMethod
S3 Permissions: bucket permissions

S3 polices can be created only by the owner of the bucket
can allow/deny bucket level permissions
bucket ownership cannot be transferred
can allow/deny object level permission if the bucket owner is owner of object
Cross account management through ACLs
Bucket policies can only be 20kb size
IAM policies vs bucket policies vs ACLs

IAM polices are account level
Bucket policies are object / resource based - only by bucket owner
ACLs are cross account object/bucket level permissions. ACLs can be used for grantint other AWS accounts to s3 resources
AWS gives full permissions to owners of the bucket

However, IAM policy can deny owner of a bucket from upload/modify or list

explicit deny always overrides an allow

Permissions are applied to S3 ARNs

access can be applied at object level, as each object will have ARN

S3 Server side encryption

provides encryption on bucket level and object level
x-amz-server-side-encryption request header is added in metadata with the upload, then aws will automatically add server side encryption
AES 256 encryption
Enable SSE through console or api. Python currently does not support SSE
AW deals with encryption and decryption automatically
You can also use your own encryption keys, but then you have to manage encription and decryption

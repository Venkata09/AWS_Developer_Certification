## Simple Storage Service S3


1. An AWS account can have upto 100 S3 buckets
1. No limits on the number of objects stored within a bucket
1. any kind of data in any format can be stored in s3
1. S3 is a simple key based object store
1. S3 in US Standard provided eventual consistency. In all other regions, s3 provided read-after-write consistency for PUTS of new objects and eventual consistency for overwtite PUTS and DELETES
1. within a region objects are redundantly stored on multiple devices across multiple facilities
1. Content MD5 and CRC are used to detct data corruption
1. Cross region replication (CRR) is allowed. Enable it to replicate data across different regions. ofcouse more cost
1. Event notifications can be setup in s3, messages can be sent out using SNS, SQS or lambda
1. Reduced redundancy storage is provide RRS. durability is 99.99% vs 99.999999999% of standard s3
1. if data lost in RRS, then 405 error. Can also setup SNS
1. S3 can host static website. Bucket name must match domain name for website hosting.
1. S3 supports own website name or website redirects
1. Access control in s3 : 4 ways can be used to secure access
1. IAM policies
1. bucket policies
1. ACLs
1. Query string authentication: can create URL to s3 object which is only valid for certain time
1. Bucket name restrictions
1. upper, lowercase letters, numbers periods and dashes
1. must start and end with letter or number, not period or dash
1. minimum 3, max 63 characters
1. cannot be an IP address style name (10.2.2.1)
1. periods and dashes cannot follow each other
1. S3 object size
1. minimum of 1 byte
1. maximum of 5TB
1. Object greater than 5G are required to be multipart upload api
1. largest object using PUT operation is 5G
1. for greater than 100Mb, you should consider multipart
1. can upload a file as it is being created,
1. can start or stop uploads
1. Must call CompleteMultiPartUpload to reassemble the file
1. S3 sorts and stores files in lexicographical order - alphabetical order.
1. So if you are reading or writing many files, then add a random hash in the begining of filename so s3 stores in different partitions. Hence throughput performance increases
1. S3 allows hosting static HTML
1. Route 53 can direct your domain to your bucket. But the bucket name needs to match domain name
1. No subdomains using s3 buckets
1. URL name .s3-website-.amazonaws.com
1. Error codes 400-client side error, 500 server side error
1. 404 not found : requesting bucket which does not exist
1. 403 forbidden : accessing bucket for which you do not have permission
1. 400 bad request : invalid bucket state
1. 409 conflict: If you try to delete a bucket that is not empty
1. 500 server : s3 issue
1. CORS Cross Origin Resource Sharing
1. in order to load resource from another bucket, you have to enable CORS
1. In the resource bucket add CORSconfiguration and add CORSRule and specify the AllowedOrigin and AllowedMethod
1. S3 Permissions: bucket permissions
1. S3 polices can be created only by the owner of the bucket
1. can allow/deny bucket level permissions
1. bucket ownership cannot be transferred
1. can allow/deny object level permission if the bucket owner is owner of object
1. Cross account management through ACLs
1. Bucket policies can only be 20kb size
1. IAM policies vs bucket policies vs ACLs
1. IAM polices are account level
1. Bucket policies are object / resource based - only by bucket owner
1. ACLs are cross account object/bucket level permissions. ACLs can be used for grantint other AWS accounts to s3 resources
1. AWS gives full permissions to owners of the bucket
1. However, IAM policy can deny owner of a bucket from upload/modify or list
1. explicit deny always overrides an allow
1. Permissions are applied to S3 ARNs
1. access can be applied at object level, as each object will have ARN
1. S3 Server side encryption
1. provides encryption on bucket level and object level
1. x-amz-server-side-encryption request header is added in metadata with the upload, then aws will automatically add server side encryption
1. AES 256 encryption
1. Enable SSE through console or api. Python currently does not support SSE
1. AW deals with encryption and decryption automatically
1. You can also use your own encryption keys, but then you have to manage encription and decryption

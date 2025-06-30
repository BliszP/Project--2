# Project--2
Title - Refactoring with Aws or Re-architecture
The refactoring approach is used to boast project agility or improve business continuity in-order to scale effectively.
Objective - flexible infrastructure PAAS and SAAS services pay as you go no upfront cost 


Refactoring help to reduce operational overhead in deploying stack.
So in using cloud services you use Paas and Saas services which are very easy to manage, flexible and scalable. So instead of using regularly Ec2 instance we use the beanstalk manage by aws service which will host our application, it has the load balancer, autoscaling and S3 buckets to store artifacts.

Frontend services provided by beanstalk
ELB
Beanstalk -TOMCAT EC2/VM
Autoscaling
Storage - EFS/S3/EBS

For the backend of the project we use the RDS service which provides the database management service
Elastic cache of for Memecache
Active MQ for RabbitMQ
Route53 for  DNS
CloudFront for Content delivery network. endpoint from cloudfront to cache

The architecture is simply put as
User access an endpoint from amazon cloudfront and the request sent to the application load balancer in the beanstalk and forwarded to the request to instances in the autoscaling group, and the beanstalk is monitored by the cloudwatch alarm. The artifacts will be stored in S3 bucket, For the backend, it will access amazon MQ, elastic cache and amazon RDS

flow of execution
login aws account
create key pair for beanstalk instance login
create security group for elastic cache , RDS and ActiveMQ
create
- RDS
- Amazon elastic cache
- Amazon active MQ
create elastic beanstalk environment
update SG of backend to allow traffic from Beanstalk SG
update SG of backend to allow internal traffic
launch Ec2 instance for DB initializing
login to instance and initialize RDS DB
change health check on beanstalk to login
Add 443 https listener to ELB
build artifact with backend information
deploy the artifact to beanstalk environment
create  CloudFront delivery network with ssl cert
update entry in Godaddy DNS zones
test url


# How to use this Repo

This is a learning Repository to show how you would create resources using cloudformation via localstack

Make sure that you have the following resouces installed on your machine before trying to use this project

* SamLocal
* AWSLocal
* Docker, running an instance of Localstack

```
docker images pull localstack/localstack:latest
```
Then to run the image that you have just downloaded 
```
docker run --rm -it -d -p 4566:4566 -p 4510-4559:4510-4559 localstack/localstack
```

To Execute any of the following scripts in each folder you will need to follow the list of instructions below

```
samlocal build
awslocal deploy --guided
```

## Buckets

This folder houses scripts to make an S3 Bucket.  After you execute the deploy you can check that the bucket has been created, by executing the following

```
awslocal s3api list-buckets

or

aws --endpoint=http://localhost:4566 s3 ls
```

you may need to add a profile, assuming that you have set on up, you would add --profile=profile_name before s3

This will display, 2 buckets first being the bucket that the template is housed in and the second should contain the name of the bucket you specified and -xxxxxxxx (where x is either a number of character)

## DynamoDB Tables

This folder houses scripts to make dynamoDB tables.  After you have executed the script you can checkout that the table has been created by executing the following

```
awslocal dynamodb list-tables

or 

aws --endpoint-url=http://localhost:4566 dynamodb list-tables
```

## SQS Simple Queue Services

There are 2 scripts in this section **template** and **dlq-template**.

The first template will setup 2 queues, one a standard queue and the second a FIFO Queue.  The other template is for setting up a Dead letter queue.  To run the second specified template you will need to adjust the build command from 

```
samlocal build
```

to 

```
samlocal build --template dlq-tempalte.yaml
```

to views the queues in a terminal window, you can do the following

```
awslocal sqs list-queues

or 

aws --endpoint-url=http://localhost:4566 sqs list-queues
```
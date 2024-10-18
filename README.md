# Use-lambda-to-count-total-object-size
> In this assignment, you will build a cloud application that plots S3 bucket size (the sum of the size of all the objects in the bucket)  change, following the microservice architecture. Specifically, you'll write three lambdas. Let's call them driverLambda, sizeTrackingLambda and plottingLambda. 

## Part 1

Write a python program (not a lambda, just a python program that runs on your laptop) that creates TestBucket and S3-object-size-history.

- Confiugre aws on terminal using
`aws configure`
- Run `createS3andTable.ipynb`

## Part 2

The `sizeTrackingLambda.py` does the following:

1. it is triggered by s3 events including object creation, update and deletion, happened in the TestBucket.

2. whenever it is triggered, it computes the total size of all the objects in the TestBucket bucket

3. Then writes the computed total size into the S3-object-size-history table. Along with the size info, it also stores the timestamp when the size is computed, the total number of objects in the bucket at that time, and the bucket name into the table.

### steps
- upload `sizeTrackingLambda.py` to lambda
- add trigger to S3 bucket
- comfigue permissions to allow read from S3 and write to DynamoDB by creating an IAM role

## Part 3
The plotting lambda, when triggered, it plots the change of bucket size of TestBucket in the last 10 seconds, plus a line that indicates the maximum size TestBucket has ever gotten in history. The Y axis is the size, X is the timestamp.

The real important thing is how to get the values needed for the plot. The plotting lambda will query (scan not allowed) items from the S3-object-size-history table and use them for the plot.
> to solve this, i used index

Lastly, expose a REST API from the plotting lambda so that it can be called synchronously.
### steps
- upload `plottingLambda.py` to lambda
- Add Layers by:
    -

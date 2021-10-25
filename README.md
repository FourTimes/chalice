# chalice
Chalice is a framework for writing serverless apps in python. It allows you to quickly create and deploy applications that use AWS Lambda. 

It provides:
  
  1. A command line tool for creating, deploying, and managing your app
  2. A decorator based API for integrating with Amazon API Gateway, Amazon S3, Amazon SNS, Amazon SQS, and other AWS services.
  3. Automatic IAM policy generation

Requirements

  python3 -m pip install botocore boto3
  python3 -m pip install chalice
  
initialize the chalice framwork

```bash

    $ mkdir chalice
    $ cd chalice
    $ chalice --help
    Usage: chalice [OPTIONS] COMMAND [ARGS]...
    ...

```
#### Credentials

Before you can deploy an application, be sure you have credentials configured. If you have previously configured your machine to run boto3 (the AWS SDK for Python) or the AWS CLI then you can skip this section.

If this is your first time configuring credentials for AWS you can follow these steps to quickly get started:

```bash
    $ aws configure
    $ aws s3 ls
```

#### Creating Your Project

The next thing we'll do is use the chalice command to create a new project

```bash
    $ chalice new-project vanguard-dev
```

This will create a vanguard-dev directory. Cd into this directory. You'll see several files have been created for you:

```bash
    $ cd vanguard-dev
    $ ls -la
    drwxr-xr-x   .chalice
    -rw-r--r--   app.py
    -rw-r--r--   requirements.txt
```

You can ignore the .chalice directory for now, the two main files we'll focus on is app.py and requirements.txt.

Let's take a look at the app.py file:

```python3

from chalice import Chalice

app = Chalice(app_name='vanguard')

@app.route('/')
def index():
    return {'hello': 'vanguard team'}

```
#### Deploying

Let's deploy this app. Make sure you're in the helloworld directory and run chalice deploy:

```bash
$ chalice deploy
Creating deployment package.
Creating IAM role: vanguard-dev
Creating lambda function: vanguard-dev
Creating Rest API
Resources deployed:
  - Lambda ARN: arn:aws:lambda:us-west-2:12345:function:vanguard-dev
  - Rest API URL: https://abcd.execute-api.us-west-2.amazonaws.com/api/
```

You now have an API up and running using API Gateway and Lambda:

```bash

$ curl https://qxea58oupc.execute-api.us-west-2.amazonaws.com/api/
{"hello": "vanguard team"}

```
#### Cleanup

If you're done experimenting with Chalice and you'd like to cleanup, you can use the chalice delete command, and Chalice will delete all the resources it created when running the chalice deploy command.

```bash
$ chalice delete
Deleting Rest API: qxea58oupc
Deleting function aws:arn:lambda:region:123456789:vanguard-dev
Deleting IAM Role vanguard-dev
```
At this point, there are several next steps you can take.

    1. Tutorials - Choose from among several guided tutorials that will give you step-by-step examples of various features of Chalice.
    https://aws.github.io/chalice/tutorials/index.html
    2. Topics - Deep dive into documentation on specific areas of Chalice. This contains more detailed documentation than the tutorials.
    https://aws.github.io/chalice/topics/index.html
    3. API Reference - Low level reference documentation on all the classes and methods that are part of the public API of Chalice.
    https://aws.github.io/chalice/api.html

 

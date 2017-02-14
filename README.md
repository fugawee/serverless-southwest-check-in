# Serverless Southwest Check In

[![Build Status](https://travis-ci.org/DavidWittman/serverless-southwest-check-in.svg?branch=master)](https://travis-ci.org/DavidWittman/serverless-southwest-check-in)

Automatically check in to your Southwest flight with Amazon Lambda and DynamoDB.

This project was inspired by similar projects from [Aaron Ortbals](https://github.com/aortbals/southwest-checkin) and [Joe Beda](https://github.com/jbeda/southwest-checkin).

## Installation

Skip to the [Deploy](#deploy) section if you already have the Serverless framework installed and configured with your AWS credentials.

### Requirements

 - [Serverless](https://serverless.com/framework/docs/providers/aws/guide/installation/). Install this first.
 - IAM user credentials with Administrator access (for Serverless)

### Configure your AWS Credentials

Add your credentials to your environment, with `aws configure`, or directly with Serverless.

Here's an example of setting your credentials via environment variables. For more detailed explanations, see the [Serverless documentation](https://serverless.com/framework/docs/providers/aws/guide/credentials/).

``` bash
$ export AWS_ACCESS_KEY_ID=YOUR_ACCESS_KEY
$ export AWS_SECRET_ACCESS_KEY=YOUR_SECRET_KEY
```

## Usage

### Deploy

To package, build, and deploy to AWS, run:

``` bash
$ make deploy
```
Or, if you don't have make installed:

```
$ pip install -r requirements.txt -t vendor && serverless deploy
```

### Add a flight

Invoke the `add` lambda function via serverless, and pass in your check-in details in JSON as parameters for the event. Here's an example:

```
$ serverless invoke --log -f add -d '{
"first_name": "George",
"last_name": "Bush",
"confirmation_number": "ABC123",
"email": "gwb@example.com"
}'

```

The `email` parameter is optional and sets the email address to which your boarding passes will be sent.

I'll likely add some helper scripts (or an API gateway) around this invocation in the future.

## Contributing

### Testing

To run tests, you must first have the requirements provided in `requirements-dev.txt` installed:

``` bash
$ pip install -r requirements-dev.txt
```

After you have installed the test dependencies, you can run the test suite with:

``` bash
# unit tests
$ make test
# flake8 style check
$ make lint
```

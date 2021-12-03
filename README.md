# smithy-typescript-template-lambda-service
A template repository for a Smithy Typescript service hosted on AWS Lambda.

# Overview

This repository is divided into three projects:

- `model` contains the Smithy model for the service.
- `typescript-client` contains the generated TypeScript client generated from `model`.
- `server` contains the service, written in TypeScript, for `model`.

# Building

## Prerequisites

[JDK](https://aws.amazon.com/corretto/) >= 8, 
[NodeJS](https://nodejs.org/en/download/) >= 14, 
[Yarn](https://yarnpkg.com/getting-started/install) >= 2, and
[Docker](https://docs.docker.com/get-docker/) should be installed before you begin, and you should have an AWS account 
[set up for the CDK](https://docs.aws.amazon.com/cdk/latest/guide/getting_started.html#getting_started_prerequisites).

## Getting started

1. After the first checkout, you will need to kick off the initial code generation by running:
    ```bash
    cd model
    ./gradlew build pTML
    cd ../typescript-client/codegen
    ./gradlew clean build
    cd ../../server/codegen
    ./gradlew clean build
    cd ../../
    ```
2. Next, run `yarn install && yarn build` to do the initial build of the entire project.
3. To deploy the service, run `cd server && yarn cdk deploy`. When complete, the CDK will print out the value for your 
   newly deployed service.
4. To test your service, switch to the `typescript-client` and use `yarn str-length` to call the `Length` operation. 
   For example, given an output from the CDK of `https://somerandomstring.execute-api.us-west-2.amazonaws.com/prod/`,
   ```bash
   yarn str-length https://somerandomstring.execute-api.us-west-2.amazonaws.com/prod/ foobar
   ```
   should print out `6`.

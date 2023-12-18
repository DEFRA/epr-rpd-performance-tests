# JMeter performance tests

## Introduction

This repo is for the performance scripts related to EPR

## Getting Started

To run the JMeter scripts you will have to install JMeter, Java and maven on your machine

## Running JMeter locally

Once you have downloaded JMeter there should be a script `bin/jmeter` that runs JMeter.

Some of the information used by the performance scripts is sensitive information e.g. Passwords, these should not be committed to the repo, examples of the runs can be found below

### POM Upload script

Example command:

``` bash
./jmeter -n -t ~/EPR_POM_Upload_Script.jmx -JUSERS=1 -JITERATIONS=1 -JUSER_CSV_FILE=Users.csv -JPASSWORD=EXAMPLE -l RESULTS
```

The above command will launch the EPR POM Upload Script with -J denoting each of the parameters to use, there are other parameters in the repo however most of them have a default value. Once run the above command will spit out a file called 'RESULTS' which will have each sample in it.

For running the above you will need two key resources, a valid POM file to upload and a csv with user email addresses to feed the tests login steps.

#### Parameters

List of CLI parameters allowed by the script:

| Parameter | Notes |
| --- | --- |
| PASSWORD | Password used by all users in the run. This parameter has a default value but it is not displayed here |
| THINK_TIME | How much time the script will wait between steps. Default: 1000ms |
| UPLOAD_REFRESHER | How much time the script will wait after uploading a file. Default: 5000ms |
| USERS | Number of users (threads) per iteration. This number must mach the number of users in the User CSV below. Default: 10 |
| ITERATIONS | Number of times the test will run. Default: 1 |
| RAMP | Ramp-up value for the tests. Default: 10 |
| USER_CSV | Path to the CSV containing the user information.  Default: users-dev4.csv |
| POM_FILE | Path to the POM file for the test.  Default: smallValidFile.csv |
| DOMAIN | Domain for theh test requests. Default: rwd-dev8.azure.defra.cloud |
| B2C_DOMAIN | B2C domain used for the sign-in process. Default: azdcuspoc2.onmicrosoft.com |
| B2C_TENANT | Name for the tenant's policy. Default: B2C_1A_EPR_SignUpSignIn |
| B2C_SERVER | Name of the B2C server for the authentication process. Default: azdcuspoc2.onmicrosoft.com |

## Contributing to this project
Please read the [contribution guidelines](CONTRIBUTING.md) before submitting a pull request.

## Licence
[Licence information](LICENCE.md).
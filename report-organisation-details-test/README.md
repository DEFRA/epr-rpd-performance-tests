# Registration files upload test

## Extract registration CSV files
```
tar -xzf organisations-brands-partners.tar.gz
```

The files in the organisations-brands-partners.tar.gz are:

Organisation details uploads:
- 1-organisations-2.5k.csv
- 1-organisations-24k.csv 
- 1-organisations-6k.csv 
- 1-organisations-6k-errors.csv 
- 1-organisations-all-error-types.csv 

Brand details uploads:

- 2-brands-2.5k.csv
- 2-brands-24k.csv
- 2-brands-6k.csv

Partner details uploads:
- 3-partners-24k.csv
- 3-partners-2.5k.csv
- 3-partners-6k.csv 

## Run parameters (registration-upload-valid.jmx)

| Parameter | Notes | Default Value |
| - | - | - |
| PASSWORD | Password used by all users in the run | ReplacePassword |
| THINK_TIME | How much time the script will wait between steps| 1 s |
| UPLOAD_REFRESHER | How much time the script will wait after uploading a file | 5 s |
| USERS | Number of users (threads) per iteration, must mach the number of users in the User CSV (USERS_CSV) file. | 1 |
| USER_CSV | Path to the CSV containing the user information | users-run-1.csv |
| ITERATIONS | Number of times the test will run| 1 |
| RAMP | Ramp-up value for the tests | 10 |
| DOMAIN | Domain for the test requests | rwd-dev8.azure.defra.cloud |
| B2C_DOMAIN | B2C domain used for the sign-in process | azdcuspoc2.onmicrosoft.com |
| B2C_TENANT | Name for the tenant's policy | B2C_1A_EPR_SignUpSignIn |
| B2C_SERVER | Name of the B2C server for the authentication process | azdcuspoc2.onmicrosoft.com |

The below commands will launch the upload script with -J denoting each of the parameters to use, there are other parameters in the repo however most of them have a default value. Once run the above command will spit out a file called 'RESULTS' which will have each sample in it.

## Run commands

[CLI Mode documentation link](https://jmeter.apache.org/usermanual/get-started.html#non_gui)

The run commands below require that the `output` directory exists.
```
mkdir output
```

### Run 1 
> 10 users - 6,000 rows

```
jmeter -n -t ./dev2-registration-upload-valid.jmx -JUSERS=10 -JITERATIONS=5 -JUSER_CSV_FILE="users-run-1.csv" -JPASSWORD=ReplacePassword -l ./output/run-1.log -e -o ./output/run-1-dashboard
```

### Run 2
> 9 users - 2,500 rows \
> 1 user - 24,000 rows

```
jmeter -n -t ./dev2-registration-upload-valid.jmx -JUSERS=10 -JITERATIONS=5 -JUSER_CSV_FILE="users-run-2.csv" -JPASSWORD=ReplacePassword -l ./output/run-2.log -e -o ./output/run-2-dashboard
```

### Run 3
> 1 user - 24,000 rows

```
jmeter -n -t ./registration-upload-valid.jmx -JUSERS=1 -JITERATIONS=10 -JUSER_CSV_FILE="users-run-3.csv" -JPASSWORD=ReplacePassword -l ./output/run-3.log -e -o ./output/run-3-dashboard
```

### Run 4 - Errors
> 1 user - organisation file with errors

```
jmeter -n -t ./registration-upload-errors.jmx -JUSERS=1 -JITERATIONS=10 -JUSER_CSV_FILE="users-run-4.csv" -JPASSWORD=ReplacePassword -l ./output/run-4.log -e -o ./output/run-4-dashboard
```
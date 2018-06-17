# sample-taskcat-project

## What is TaskCat?
> TaskCat is a tool that tests AWS CloudFormation templates. It deploys your AWS CloudFormation template in multiple AWS Regions and generates a report with a pass/fail grade for each region. You can specify the regions and number of Availability Zones you want to include in the test, and pass in parameter values from your AWS CloudFormation template. TaskCat is implemented as a Python class that you import, instantiate, and run.

See [taskcat.io](https://aws-quickstart.github.io/taskcat/) for more details.

### Installing TaskCat (Docker install)
> Prerequisites: docker
```
curl -s https://raw.githubusercontent.com/aws-quickstart/taskcat/master/installer/docker-install-master| sudo python -E
```
> Note: (If you do not have root privileges taskcat will install in the current directory)

### Installing via pip3 (for those who do not want to use the docker installer)
> Prerequisites: Python 3.5+ and pip3
```
pip3 install taskcat
```

### Installing via pip3 --user (for those who want to install taskcat into their homedir)
> Prerequisites: Python 3.5+ and pip3
> Note: (the user install dir is platform specific)

> For Example: (On Mac: ~/Library/Python/3.x/bin/taskcat)

> For Example: (On Linux: ~/.local/bin)

```
pip3 install taskcat --user
```
> Warning: Be sure to add the python bin dir to your `$PATH`

### Running TaskCat
> If you have AWS credentials sourced (or default boto profile is available)
```
taskcat -c sample-taskcat-project/ci/config.yml
```
> If you need to pass ACCESS and SECRET keys
```
taskcat -c sample-taskcat-project/ci/config.yml -A YOUR_ACCESS_KEY -S YOUR_SECRET_KEY
```
> If you want to use a different account or profile
```
taskcat -c sample-taskcat-project/ci/config.yml -P boto-profile-name
```

See [installing-taskcat](https://github.com/aws-quickstart/taskcat#installing-taskcat) for more details.

### Running the `sample-taskcat-project`

Use the [sample-taskcat-project]() folder as a working starting point for taskcat based quickstarts.

```bash

export AWS_DEFAULT_PROFILE=russomi
export AWS_DEFAULT_REGION=us-east-1

taskcat -c sample-taskcat-project/ci/taskcat-autobucket.yaml -v

```

### Usage
```
usage: taskcat [-h] [-c CONFIG_YML] [-P BOTO_PROFILE] [-A AWS_ACCESS_KEY]
               [-S AWS_SECRET_KEY] [-n] [-N] [-p] [-v] [-m] [-t TAG]
               [-s STACK_PREFIX]

            Multi-Region CloudFormation Test Deployment Tool
            For more info see: http://taskcat.io


optional arguments:
  -h, --help            show this help message and exit
  -c CONFIG_YML, --config_yml CONFIG_YML
                         (Config File Required!)
                         example here: https://raw.githubusercontent.com/aws-quickstart/taskcat/master/examples/sample-taskcat-project/ci/taskcat.yml
  -P BOTO_PROFILE, --boto_profile BOTO_PROFILE
                        Authenticate using boto profile
  -A AWS_ACCESS_KEY, --aws_access_key AWS_ACCESS_KEY
                        AWS Access Key
  -S AWS_SECRET_KEY, --aws_secret_key AWS_SECRET_KEY
                        AWS Secret Key
  -n, --no_cleanup      Sets cleanup to false (Does not teardown stacks)
  -N, --no_cleanup_failed
                        Sets cleaup to false if the stack launch fails (Does not teardown stacks if it experiences a failure)
  -p, --public_s3_bucket
                        Sets public_s3_bucket to True. (Accesses objects via public HTTP, not S3 API calls)
  -v, --verbose         Enables verbosity
  -m, --multithread_upload
                        Enables multithreaded upload to S3
  -t TAG, --tag TAG     add tag to cloudformation stack, must be in the format TagKey=TagValue, multiple -t can be specified
  -s STACK_PREFIX, --stack-prefix STACK_PREFIX
                        set prefix for cloudformation stack name. only accepts lowercase letters, numbers and '-'
```

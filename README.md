# taskcat-examples

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

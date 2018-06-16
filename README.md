# taskcat-examples

## What is TaskCat?
> TaskCat is a tool that tests AWS CloudFormation templates. It deploys your AWS CloudFormation template in multiple AWS Regions and generates a report with a pass/fail grade for each region. You can specify the regions and number of Availability Zones you want to include in the test, and pass in parameter values from your AWS CloudFormation template. TaskCat is implemented as a Python class that you import, instantiate, and run.

## Example

Use the [sample-taskcat-project]() folder as a working starting point for taskcat based quickstarts.

```bash

export AWS_DEFAULT_PROFILE=russomi
export AWS_DEFAULT_REGION=us-east-1

taskcat -c sample-taskcat-project/ci/taskcat-autobucket.yaml -v

```

## References
[taskcat.io](https://aws-quickstart.github.io/taskcat/)
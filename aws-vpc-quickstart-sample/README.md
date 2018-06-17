# aws-vpc-quickstart-template
Example AWS VPC Quickstart + TaskCat

## CLI quickstart
```bash

# add submodules:
git submodule add -b master git@github.com:aws-quickstart/quickstart-aws-vpc.git submodules/quickstart-aws-vpc

export AWS_DEFAULT_PROFILE=russomi
export AWS_DEFAULT_REGION=us-east-1

taskcat -c sample-taskcat-project/ci/taskcat-autobucket.yaml -v

```

### taskcat usage

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

# Builders Guide

**What you’ll need to set up:**

*   Get a GitHub account.
    *   We use GitHub for source control. The GitHub organization for AWS Quick Starts is at [https://github.com/aws-quickstart](https://github.com/aws-quickstart).
    *   We use SSH authentication in the submodules, so if you want to contribute to the Quick Starts, you must have your public key registered in your GitHub account.
    *   For security, you must enable [two-factor authentication (2FA)](https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/) on your account.
*   Set up your development environment:
    *   For an IDE, you can use: Visual Studio with AWS Tools, Atom, Sublime Text, Visual Studio Code
    *   For source control, use: Git, GitHub.com website, SSH keys

**What you’ll need to know:**

*   If you haven’t used Git before, learn about commands and concepts at [https://git-scm.com/doc](https://git-scm.com/doc), especially the following sections:
    *   [Branching](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
    *   [Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
    *   For a refresher, use the [Git cheat sheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet/)
*   Familiarize yourself with [JSON](http://www.json.org/) or [YAML](http://www.yaml.org/).
    *   JSON and YAML are the two supported formats for AWS CloudFormation templates. However, note that AWS CloudFormation [doesn’t support all YAML features](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-formats.html).
*   Learn about AWS CloudFormation. Here are some useful links:
    *   [Best practices](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/best-practices.html)
    *   [Metadata and user data](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)
    *   [Parameters](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html)
    *   [cfn-init](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-init.html)
    *   [cfn-signal](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-signal.html)
*   Explore AWS services to include in your deployment to improve the usefulness of your cloud architecture:
    *   View [AWS products and services](https://aws.amazon.com/products/) by category.
    *   See the [planning](planning.html) section for some services to consider based on the characteristics of your workload.
    *   Read the [AWS documentation](https://aws.amazon.com/documentation/) for complete details about a service.

**Planning your architecture**

Here are some of the questions you should consider when designing your architecture.

* How many Availability Zones? You should use at least two for high availability.

* Where should your workload be placed? Consider security and external access when deciding whether to install your software in a public or private subnet.

* How many public and private subnets? If your workload needs an additional level of isolation, you might consider setting up a second private subnet with network ACL protection in each Availability Zone.

* Is your workload distributed across multiple instances? If yes, use [Elastic Load Balancing](https://aws.amazon.com/elasticloadbalancing/) to help ensure availability and fault tolerance.

* Is your workload stateless or stateful? Do you save session state in the workload instances? If you don't, your workload instance would be a good candidate for [Auto Scaling](https://aws.amazon.com/autoscaling/).

* Are you storing data? What kind of database do you need?

  *   If relational, use [Amazon RDS](https://aws.amazon.com/rds/).
  *   If NoSQL, [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) is a good option.
  *   If your database engine is MySQL or PostgreSQL, you can use [Amazon Aurora](https://aws.amazon.com/aurora/).

* Are there any other AWS services that will complement the functionality of your software in the cloud? If yes, consider including them in your architecture. For example:

  *   If you need a directory, add [AWS Directory Service](https://aws.amazon.com/directoryservice/).
  *   For Hadoop processing, use [Amazon EMR](https://aws.amazon.com/emr/).

* If your workload needs to meet compliance requirements such as NIST or PCI, consider using one of the [compliance Quick Starts](https://aws.amazon.com/quickstart/#security) for your infrastructure.

**Submodules**

*   When you add a submodule, make sure it points to the master branch and use SSH to authenticate.
*   Any submodule you add must reside in the submodules/_quickstart-repo-name_ directory of the repository, where _quickstart-repo-name_ is the name of the repository for the Quick Start that you are using as a submodule.
*   To add a Git submodule, run the following command from your Quick Start root directory:
*   `git submodule add –b master git@github.com:aws-quickstart/<quickstart-repo-name>.git submodules/<quickstart-repo-name>`
*   For example, to add the VPC Quick Start as a submodule, use the command:
*   `git submodule add -b master git@github.com:aws-quickstart/quickstart-aws-vpc.git submodules/quickstart-aws-vpc`
*   To clone a repository that has submodules, use:
*   `git clone --recursive git@github.com:aws-quickstart/<quickstart-repo-name>.git`
*   To synchronize all submodules in a Quick Start after a `git pull` use:
*   `git submodule update --recursive`
*   To update the submodules to the latest version, use:
*   `git submodule update --remote --merge`
*   Do not use the `--recursive` option in this case, but you can also update an individual module by specifying its name at the end as `submodules/<quickstart-repo-name>`.


## References
* [Quick Start Builder's Guide](https://aws-quickstart.github.io/building.html)
* [Planning](https://aws-quickstart.github.io/planning.html)
* [Submodules](https://aws-quickstart.github.io/design.html#submodules)
* [Modularity](https://aws-quickstart.github.io/design.html#modularity)




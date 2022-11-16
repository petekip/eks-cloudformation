# Amazon EKS Cluster Template

Automate your infrastructure deployment with cloudformation.

- [eks.yml](eks.yml): a CloudFormation template that defines an EKS cluster, including a VPC, the EKS control plane (master nodes) and the EKS worker nodes.
- [run.sh](up.sh): a Bash script that applies the CloudFormation template to your AWS account and finalises the cluster creation, including `kubectl` configuration.

## Usage

### Prerequisites

- Install the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/installing.html):
    ~~~homebrew
    brew install awscli
    ~~~
- Install the [AWS IAM Authenticator](https://docs.aws.amazon.com/eks/latest/userguide/configure-kubectl.html):
    ~~~homebrew
    brew curl get -u -v github.com/kubernetes-sigs/aws-iam-authenticator/cmd/aws-iam-authenticator
    ~~~
- Install [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/):
   ~~~homebrew
   brew install kubernetes-cli
   ~~~

### Run

1. Edit parameters in `up.sh`:
    - `NUM_WORKER_NODES`: number of worker nodes for your EKS cluster
    - `WORKER_NODES_INSTANCE_TYPE`: EC2 instance type for the worker nodes
    - `STACK_NAME`: name of the CloudFormation stack for your EKS cluster
    - `KEY_PAIR_NAME`: name of an existing EC2 key pair for connecting to the worker nodes with SSH

2. Run:
    ~~~bash
    bash run.sh
    ~~~

#### Note

Any arguments that you pass to `run.sh` will be forwarded to the AWS CLI commands within the script. Thus, it is possible to specify an explicit region fo the cluster as follows: `--region us-east-1`

~~~bash
bash up.sh --region us-east-1
~~~

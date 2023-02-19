# pra_GithubAction_CDK
practice　GithubAction and CDK

# reference

## CDK
https://aws.amazon.com/jp/getting-started/guides/setup-cdk/module-two/

https://cdkworkshop.com/30-python/20-create-project.html

## GithubAction


# Goal
1. setting CDK(assume role)
2. deploy CDK（making simple app)
3. setting GithubAction

# setting CDK
we need below software.
- node (I use v14.15.1)
- python (I use Python3.9.6)

install aws-cdk
~~~
npm install -g aws-cdk
~~~

check installed
~~~
cdk --version
~~~

install aws-cli(refer:https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
~~~
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
~~~

click AWSCLIV2.pkg and follow the on-screen instructions.

check installed AWSCLI like below.
~~~
which aws 
output:/usr/local/bin/aws
~~~
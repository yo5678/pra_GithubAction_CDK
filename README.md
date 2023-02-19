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

# Setting CDK
we need below software.
- node (I use v14.15.1)
- python (I use Python3.9.6)
- AWS Account(I made switchrole which has AdministratorAccess)
- AWS_Vault(reference:https://dev.classmethod.jp/articles/aws-vault/) 

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

Now you can bootstrap the account with the following command
~~~
cdk bootstrap aws://ACCOUNT-NUMBER/REGION
~~~

What is boostrap:we need to perform this command just once when
you make new cdk-app. After perfomr this commmand, AWS start preparing　resource that needs deploying.

https://dev.classmethod.jp/articles/cdk-bootstrap-modern-template/


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


# make CDK-app

~~~
mkdir cdk_workshop && cd cdk_workshop
~~~

cdk init command
~~~
cdk init sample-app --language python
~~~

activate virtualenv and install python package
~~~
source .venv/bin/activate

pip install -r requirements.txt
~~~

The folder cdk_workshop, there are many directorys and files.

below two file is important in this app.

- app.py: main file.
  ~~~
  #!/usr/bin/env python3

    import aws_cdk as cdk

    from cdk_workshop.cdk_workshop_stack import CdkWorkshopStack


    app = cdk.App()
    CdkWorkshopStack(app, "cdk-workshop")

    app.synth()

  ~~~
- cdk_workshop_stack.py
  cdk_workshop is python module directory.
  cdk_workshop_stack.py is below code and is refered by app.py.
  ~~~
    from constructs import Construct
    from aws_cdk import (
        Duration,
        Stack,
        aws_iam as iam,
        aws_sqs as sqs,
        aws_sns as sns,
        aws_sns_subscriptions as subs,
    )


    class CdkWorkshopStack(Stack):

        def __init__(self, scope: Construct, construct_id: str, **kwargs) -> None:
            super().__init__(scope, construct_id, **kwargs)

            queue = sqs.Queue(
                self, "CdkWorkshopQueue",
                visibility_timeout=Duration.seconds(300),
            )

            topic = sns.Topic(
                self, "CdkWorkshopTopic"
            )

            topic.add_subscription(subs.SqsSubscription(queue))

  ~~~

if you are same directly as cdk.json, you can use below command. You can get CDK stack list.
~~~
cdk ls
~~~

If you use this commnad, you can make template of cloudformation.
~~~
cdk synth
~~~

Next, you can deploy app with below command.
If you use aws-vault, please refer below command(you write commnad you want todo after "--" ).

~~~
aws-vault exec {Assumerole-RoleName} -- cdk deploy  
~~~

You want to clean resources, Please use below command.
~~~
aws-vault exec {Assumerole-RoleName} -- cdk destroy  
~~~

# 사전 준비
Elastic beanstalk를 사용하기 위해서는 사전에 필요한 설치 파일 혹은 AWS 리소소를 사용할 권한이 필요하다. <br />


## 설치 구성
- aws-cli
- eb-cli

## 권한 
Elastic beanstalk은 아래와 같은 권한을 요청한다.

### Service role
'Service role'은 Elastic beanstalk이 AWS리소스를 사용하도록 위임받는 권한(IAM role)을 의미한다. <br />
만약 아래와 같이 환경을 구성할때 service role를 지정하지 않는다면, <br />
환경을 생성할때 'aws-elasticbeanstalk-service-role'라는 이름으로 service role을 생성한다.
```
$ eb create --service-role <role-name>
```
<br />

### Instance Profile
Elastic beanstalk 환경에서 생성한 인스턴스에 부여하는 IAM role입니다. <br />
관려형 정책으로는 'AWSElasticBeanstalkWorkerTier'과 'AWSElasticBeanstalkMulticontainerDocker'를 제공하고 있다.<br />
기본적으로 이런 정책들이 'aws-elasticbeanstalk-ec2-role'에 연결됨.
<br />

### User policy
Elastic beanstalk를 사용하기위하여 다양한 권한이 필요하다. <br />
그러므로 이런 복잡한 권한에 대하여 아마존에서는 'AWSElasticBeanstalkFullAccess'라는 사전에 준비된 정책(Managed policy)을 사용할 수 있다.
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "elasticbeanstalk:*",
        "ec2:*",
        "ecs:*",
        "ecr:*",
        "elasticloadbalancing:*",
        "autoscaling:*",
        "cloudwatch:*",
        "s3:*",
        "sns:*",
        "cloudformation:*",
        "dynamodb:*",
        "rds:*",
        "sqs:*",
        "logs:*",
        "iam:GetPolicyVersion",
        "iam:GetRole",
        "iam:PassRole",
        "iam:ListRolePolicies",
        "iam:ListAttachedRolePolicies",
        "iam:ListInstanceProfiles",
        "iam:ListRoles",
        "iam:ListServerCertificates",
        "acm:DescribeCertificate",
        "acm:ListCertificates",
        "codebuild:CreateProject",
        "codebuild:DeleteProject",
        "codebuild:BatchGetBuilds",
        "codebuild:StartBuild"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:AddRoleToInstanceProfile",
        "iam:CreateInstanceProfile",
        "iam:CreateRole"
      ],
      "Resource": [
        "arn:aws:iam::*:role/aws-elasticbeanstalk*",
        "arn:aws:iam::*:instance-profile/aws-elasticbeanstalk*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:CreateServiceLinkedRole"
      ],
      "Resource": [
        "arn:aws:iam::*:role/aws-service-role/autoscaling.amazonaws.com/AWSServiceRoleForAutoScaling*"
      ],
      "Condition": {
        "StringLike": {
          "iam:AWSServiceName": "autoscaling.amazonaws.com"
        }
      }
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:CreateServiceLinkedRole"
      ],
      "Resource": [
        "arn:aws:iam::*:role/aws-service-role/elasticbeanstalk.amazonaws.com/AWSServiceRoleForElasticBeanstalk*"
      ],
      "Condition": {
        "StringLike": {
          "iam:AWSServiceName": "elasticbeanstalk.amazonaws.com"
        }
      }
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:AttachRolePolicy"
      ],
      "Resource": "*",
      "Condition": {
        "StringLike": {
          "iam:PolicyArn": [
            "arn:aws:iam::aws:policy/AWSElasticBeanstalk*",
            "arn:aws:iam::aws:policy/service-role/AWSElasticBeanstalk*"
          ]
        }
      }
    }
  ]
}
```

## Link
- [MacOS에서 aws-cli 설치가이드](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/cli-install-macos.html)
- [MacOS에서 eb-cli 설치가이드](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/eb-cli3-install-osx.html)
- [사용자 권한](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts-roles-user.html)
- [EB EC2 인스턴스 역할](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/concepts-roles-instance.html)

---
title: "aws cli resource commands"
date: 2023-04-11
categories: [ devops-sre ]
---
## aws cli resource commands  
sometimes you just need to have things crated and done in the cli.

## create cloudwatch alarm  
```
aws \
 cloudwatch put-metric-alarm --alarm-name test-alarm --alarm-description "Alarm when  CPU exceeds 70 percent" \
   --metric-name CPUUtilization --namespace AWS/EC2 --statistic Average --period 300 --threshold 70 \
   --comparison-operator GreaterThanThreshold  --dimensions "Name=InstanceId,Value=i-12345678" --evaluation-periods 1 \
   --alarm-actions arn:aws:sns:us-east-1:546781284141:alerting --unit Percent \
   --tags Key=routing,Value=Platform Key=alertLevel,Value=INFO Key=slack_channel,Value=alerts-info Key=alarmType,Value=test
``` 

## trigger cloudwatch alarm
aws cloudwatch set-alarm-state --alarm-name "test-alarm" --state-value ALARM --state-reason "testing purposes" 
```

## create lambda via docker image  
```
aws \
lambda create-function --region us-east-1 --package-type Image --function-name test-lambda --handler handler.handler \
 --code ImageUri=123451234512345.dkr.ecr.us-east-1.amazonaws.com/reponame:imagenametag --role arn:aws:iam::000000000:role/lambda-role
```

## lambda invoke from sns
```
aws \
lambda add-permission --function-name test-lambda \
--statement-id function-with-sns --action "lambda:InvokeFunction" \
--principal sns.amazonaws.com 
```
```
aws lambda add-permission \
    --function-name test-lambda \
    --action lambda:InvokeFunction \
    --statement-id sns \
    --principal sns.amazonaws.com
```
## directly invoke lambda
```
aws lambda invoke --function-name arn:aws:lambda:us-east-1:000000000000:function:test-lambda --payload '{"test":"test"}' response.json
```

## delete lambda
```
aws lambda delete-function --function-name test-lambda
```
## updating an existing lambda 
```
aws \
lambda update-function-code --function-name test-lambda --image-uri 11111111111.dkr.ecr.us-east-1.amazonaws.com/somerepo:latest 

```
## create sns topic  
``` 
aws sns create-topic \
  --region us-east-1 \
  --name testTopic 

```

## create sns topic permissions 
```
aws \
sns add-permission --label lambda-access --aws-account-id 000000000000 \
--topic-arn arn:aws:sns:us-east-1:000000000000:testTopic \
--action-name Subscribe ListSubscriptionsByTopic
```
##  write to sns topic
```
aws events put-events --entries file://root_login.json 
```
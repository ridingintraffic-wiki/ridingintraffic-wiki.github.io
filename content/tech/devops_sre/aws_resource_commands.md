---
title: "aws cli resource commands"
date: 2023-04-11
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

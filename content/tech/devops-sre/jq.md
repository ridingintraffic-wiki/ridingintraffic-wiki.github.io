---
title: "jq snippets"
date: 2023-05-22
categories: [ devops-sre ]
---
## all the jq things all the time

### using jq with terraform
taking a terraform plan and outputting only the things that will change on the plan.   such as only the resource names.  
this is useful when you need to do some targeted deploys.  
```
terraform plan -input=false -compact-warnings -out plan.tfplan;  
terraform show -no-color -json plan.tfplan | jq -r '.resource_changes[] | select(.change.actions[0]=="update" or .change.actions[0]=="create" or .change.actions[0]=="create") | .address
```
# packer-ansible-lesson
PackerとAnsibleのお勉強用資料

## 一気呵成にデプロイする

### 1. Packerでビルド

```
packer build packer.json
```

### 2. AWS CLIでIDを取得

```
aws ec2 describe-images --filters "Name=tag:Amazon_AMI_Management_Identifier,Values=packer-ansible-lesson" --query 'Images[*].[ImageId]' --output text
```

### 3. CFnにわたす

```
aws cloudformation deploy \
--template-file packer.yaml \
--stack-name packer-lesson \
--s3-bucket packer-lesson-stack \
--parameter-overrides AmiId=$AMI_ID $(cat parameters/.env) \
--region=ap-northeast-1
```
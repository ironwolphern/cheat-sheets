# AWS CLI Cheatsheet

## Configuración Inicial
```bash
# Configurar credenciales AWS
aws configure
aws configure set region us-east-1
aws configure list

# Listar perfiles configurados
aws configure list-profiles
```

## EC2 (Elastic Compute Cloud)
```bash
# Listar instancias
aws ec2 describe-instances
aws ec2 describe-instances --filters "Name=instance-state-name,Values=running"

# Iniciar/Detener instancias
aws ec2 start-instances --instance-ids i-1234567890abcdef0
aws ec2 stop-instances --instance-ids i-1234567890abcdef0

# Crear instancia
aws ec2 run-instances \
    --image-id ami-12345678 \
    --instance-type t2.micro \
    --key-name MyKeyPair \
    --security-group-ids sg-903004f8

# Terminar instancia
aws ec2 terminate-instances --instance-ids i-1234567890abcdef0
```

## S3 (Simple Storage Service)
```bash
# Listar buckets
aws s3 ls

# Listar contenido de un bucket
aws s3 ls s3://nombre-bucket

# Copiar archivos
aws s3 cp archivo.txt s3://nombre-bucket/
aws s3 cp s3://nombre-bucket/archivo.txt ./

# Sincronizar directorios
aws s3 sync . s3://nombre-bucket
aws s3 sync s3://nombre-bucket .

# Eliminar objetos
aws s3 rm s3://nombre-bucket/archivo.txt
aws s3 rb s3://nombre-bucket --force  # Eliminar bucket
```

## IAM (Identity and Access Management)
```bash
# Usuarios
aws iam list-users
aws iam create-user --user-name nombre-usuario
aws iam delete-user --user-name nombre-usuario

# Grupos
aws iam list-groups
aws iam create-group --group-name nombre-grupo
aws iam add-user-to-group --user-name usuario --group-name grupo

# Roles
aws iam list-roles
aws iam create-role --role-name nombre-rol --assume-role-policy-document file://trust-policy.json
```

## RDS (Relational Database Service)
```bash
# Listar instancias de base de datos
aws rds describe-db-instances

# Crear instancia de base de datos
aws rds create-db-instance \
    --db-instance-identifier mydb \
    --db-instance-class db.t3.micro \
    --engine mysql \
    --master-username admin \
    --master-user-password mypassword \
    --allocated-storage 20

# Modificar instancia
aws rds modify-db-instance \
    --db-instance-identifier mydb \
    --backup-retention-period 7

# Eliminar instancia
aws rds delete-db-instance \
    --db-instance-identifier mydb \
    --skip-final-snapshot
```

## Lambda
```bash
# Listar funciones
aws lambda list-functions

# Crear función
aws lambda create-function \
    --function-name mi-funcion \
    --runtime python3.9 \
    --role arn:aws:iam::123456789012:role/lambda-role \
    --handler index.handler \
    --zip-file fileb://function.zip

# Invocar función
aws lambda invoke \
    --function-name mi-funcion \
    --payload '{"key": "value"}' \
    output.txt

# Actualizar código
aws lambda update-function-code \
    --function-name mi-funcion \
    --zip-file fileb://function.zip
```

## CloudWatch
```bash
# Obtener métricas
aws cloudwatch get-metric-statistics \
    --namespace AWS/EC2 \
    --metric-name CPUUtilization \
    --dimensions Name=InstanceId,Value=i-1234567890abcdef0 \
    --start-time 2024-01-01T00:00:00 \
    --end-time 2024-01-02T00:00:00 \
    --period 3600 \
    --statistics Average

# Crear alarma
aws cloudwatch put-metric-alarm \
    --alarm-name cpu-mon \
    --alarm-description "CPU utilization" \
    --metric-name CPUUtilization \
    --namespace AWS/EC2 \
    --statistic Average \
    --period 300 \
    --threshold 70 \
    --comparison-operator GreaterThanThreshold \
    --evaluation-periods 2
```

## ECS (Elastic Container Service)
```bash
# Listar clusters
aws ecs list-clusters

# Crear cluster
aws ecs create-cluster --cluster-name mi-cluster

# Listar servicios
aws ecs list-services --cluster mi-cluster

# Actualizar servicio
aws ecs update-service \
    --cluster mi-cluster \
    --service mi-servicio \
    --desired-count 2
```

## VPC (Virtual Private Cloud)
```bash
# Listar VPCs
aws ec2 describe-vpcs

# Crear VPC
aws ec2 create-vpc --cidr-block 10.0.0.0/16

# Crear subred
aws ec2 create-subnet \
    --vpc-id vpc-12345678 \
    --cidr-block 10.0.1.0/24

# Crear Internet Gateway
aws ec2 create-internet-gateway
aws ec2 attach-internet-gateway \
    --vpc-id vpc-12345678 \
    --internet-gateway-id igw-12345678
```

## EKS (Elastic Kubernetes Service)
```bash
# Crear cluster de EKS
aws eks create-cluster \
    --name mi-cluster-eks \
    --role-arn arn:aws:iam::123456789012:role/eks-cluster-role \
    --resources-vpc-config subnetIds=subnet-12345678,subnet-87654321,securityGroupIds=sg-12345678

# Listar clusters
aws eks list-clusters

# Describir cluster
aws eks describe-cluster --name mi-cluster-eks

# Actualizar versión de Kubernetes
aws eks update-cluster-version \
    --name mi-cluster-eks \
    --kubernetes-version 1.27

# Gestionar node groups
aws eks create-nodegroup \
    --cluster-name mi-cluster-eks \
    --nodegroup-name mi-nodegroup \
    --node-role arn:aws:iam::123456789012:role/eks-node-role \
    --subnets subnet-12345678 subnet-87654321 \
    --instance-types t3.medium \
    --scaling-config minSize=2,maxSize=5,desiredSize=3

# Listar node groups
aws eks list-nodegroups --cluster-name mi-cluster-eks

# Eliminar node group
aws eks delete-nodegroup \
    --cluster-name mi-cluster-eks \
    --nodegroup-name mi-nodegroup

# Actualizar kubeconfig
aws eks update-kubeconfig --name mi-cluster-eks --region us-east-1

# Crear/actualizar add-ons
aws eks create-addon \
    --cluster-name mi-cluster-eks \
    --addon-name vpc-cni \
    --addon-version v1.12.0-eksbuild.1

# Listar add-ons
aws eks list-addons --cluster-name mi-cluster-eks
```

## Load Balancer
```bash
# Crear Application Load Balancer
aws elbv2 create-load-balancer \
    --name mi-alb \
    --subnets subnet-12345678 subnet-87654321 \
    --security-groups sg-12345678 \
    --type application

# Crear Network Load Balancer
aws elbv2 create-load-balancer \
    --name mi-nlb \
    --subnets subnet-12345678 subnet-87654321 \
    --type network

# Crear Target Group
aws elbv2 create-target-group \
    --name mi-target-group \
    --protocol HTTP \
    --port 80 \
    --vpc-id vpc-12345678 \
    --target-type instance

# Registrar targets
aws elbv2 register-targets \
    --target-group-arn arn:aws:elasticloadbalancing:region:123456789012:targetgroup/mi-target-group/1234567890 \
    --targets Id=i-12345678

# Crear listener
aws elbv2 create-listener \
    --load-balancer-arn arn:aws:elasticloadbalancing:region:123456789012:loadbalancer/app/mi-alb/1234567890 \
    --protocol HTTP \
    --port 80 \
    --default-actions Type=forward,TargetGroupArn=arn:aws:elasticloadbalancing:region:123456789012:targetgroup/mi-target-group/1234567890

# Describir load balancers
aws elbv2 describe-load-balancers

# Describir target groups
aws elbv2 describe-target-groups

# Describir target health
aws elbv2 describe-target-health \
    --target-group-arn arn:aws:elasticloadbalancing:region:123456789012:targetgroup/mi-target-group/1234567890

# Modificar atributos del load balancer
aws elbv2 modify-load-balancer-attributes \
    --load-balancer-arn arn:aws:elasticloadbalancing:region:123456789012:loadbalancer/app/mi-alb/1234567890 \
    --attributes Key=idle_timeout.timeout_seconds,Value=120

# Añadir/modificar tags
aws elbv2 add-tags \
    --resource-arns arn:aws:elasticloadbalancing:region:123456789012:loadbalancer/app/mi-alb/1234567890 \
    --tags Key=Environment,Value=Production
```

## Tips Generales
```bash
# Formato de salida
aws ec2 describe-instances --output json
aws ec2 describe-instances --output table
aws ec2 describe-instances --output text

# Filtrado JMESPath
aws ec2 describe-instances \
    --query 'Reservations[*].Instances[*].[InstanceId,State.Name]'

# Debug mode
aws --debug ec2 describe-instances

# Perfiles nombrados
aws --profile produccion ec2 describe-instances
```

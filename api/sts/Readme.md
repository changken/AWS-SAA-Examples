## Create a user with no permission

We need to create a new user with no premission and generate access key

```sh
aws iam create-user --user-name sts-machine-user
aws iam create-access-key --user-name sts-machine-user --output table
```

copy the access key and secret here
```sh
aws configure
```

That edit credentials file to change away from default profile

Test who you are:
```sh
aws sts get-caller-identity --profile sts
```

Make sure you dont have access to s3
```sh
aws s3 ls --profile sts
```

An error occurred (AccessDenied) when calling the ListBuckets operation: User: arn:aws:iam::xxxx:user/sts-machine-user is not authorized to perform: s3:ListAllMyBuckets because no identity-based policy allows the s3:ListAllMyBuckets action


## Create a Role

we need to create a role that will access a new resoure

```sh
chmod u+x bin/deploy
./bin/deploy
```

## use new user crendtials and assume role

```sh
aws sts assume-role \
    --role-arn arn:aws:iam::xxx:role/my-sts-fun-stack-STSRole-TNek7HB1QQDr \
    --role-session-name s3-sts-fun \
    --profile sts
```

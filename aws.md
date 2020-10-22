# AWS scripts 

## Description

Mainly relate to automating common AWS infrastructure tasks via the AWS CLI

## Key Pairs

> some of the commands are generic and some are geared for EC2 usage

### ✏️ Creating a keypair

Creating a keypair is easy

```bash
aws ec2 create-key-pair --key-name my-service
```

Except the problem is that we usually want to use this keypair and the above command returns JSON. 

Now you might say 'Aha use the jq module' but the aws cli already has a widespread way to convert the format to text. 

We make use the ```--query``` and the ```--output``` flags to pipe the KeyMaterial (key contents) to a .pem file

```bash
aws ec2 create-key-pair \ 
--key-name my-service \
--query 'KeyMaterial' \ 
--output text > my-service-key-pair.pem
```

Before we use the pem we also will need to tweek permission

```
chmod 400 my-key-pair.pem
```

[AWS EC2 keypair docs - CLI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#aws-cli)

### ✏️ Getting a keypair (not for EC2)

This gets you all the keypairs in an account. 

That being said this only works for some services eg. Lightsail. This DOES NOT WORK for EC2

For example 👇
```zsh
aws lightsail get-key-pairs
```

[AWS | get-key-pairs docs](]https://docs.aws.amazon.com/cli/latest/reference/lightsail/get-key-pairs.html?highlight=keypair)


### ✏️ Describing a keypair (EC2)

Will return JSON

```
aws ec2 describe-key-pairs --key-name MyKeyPair
```

### ✏️ Deleting a keypair

```
aws ec2 delete-key-pair --key-name my-key-pair
```

## Resources

- [AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/index.html)
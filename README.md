# Lab: Kali linux on EC2

This lab shows how to setup Kali Linux on an AWS EC2 instance and connect to it via RDP.

## Prerequisites

AWS cli installed and configured with proper credentials.

An RDP client installed.

## Steps

1. create a security group: `./create-security-group <name> <description>`

2. create a key pair: `./create-key-pair <name>`

3. find the AMI id: `./list-marketplace-ami <region> <marketplace url>`

3. edit the instance.json file: add the security group, key pair and AMI id

4. create an EC2 instance: `./create-instance instance.json`

5. find the instance ip: `./get-instance-ip`

6. connect to the instance via SSH: `./kali-ssh <key file> <instance ip>`

7. run the commands listed in `rdp-setup.txt`

8. connect via RDP client with username and password, through the public ip

Note: the default username for the Kali AMI is ec2-user

## AWS Marketplace URL

The URL for the Kali Linux AMI at the time of this writing is:

<https://aws.amazon.com/marketplace/pp/B01M26MMTT>


## Warning

Before doing penetration testing in AWS, make sure you read the [AWS Customer Support Policy for Penetration Testing](https://aws.amazon.com/security/penetration-testing/).

Remember to clean up the created resources from your AWS account after this lab.


## Author

**Andre Silva** [adev@disroot.org](mailto:adev@disroot.org)

## License

This project is licensed under the [Unlicense](UNLICENSE.md).

## References

<https://www.kali.org/>

<https://remmina.org/>

<https://aws.amazon.com/security/penetration-testing/>

<https://docs.aws.amazon.com/cli/latest/>

<https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-skeleton.html>

<https://serverfault.com/questions/981763/how-do-i-set-user-data-when-using-the-aws-cli-cli-input-json-argument>



# Lab: Kali linux on EC2

This lab shows how to setup Kali Linux on an AWS EC2 instance and connect to it
via RDP.

## Warning

Before going through this lab or doing any penetration testing in AWS, make sure
you read the
[AWS Customer Support Policy for Penetration Testing](https://aws.amazon.com/security/penetration-testing/).

Remember to clean up the created resources from your AWS account after this lab.

## Pre-requisites

- AWS CLI installed and configured with proper credentials.

- An RDP client installed.

- A subscription to the Kali Linux official AWS AMI on the
  [AWS Marketplace](https://aws.amazon.com/marketplace) (search for "Kali
  Linux").

- Go to the product subscription page in the AWS Marketplace and find the AMI
  ID. Save it for later.

## Steps

0. copy the example instance configuration:
   ```sh
   cp instance.example.json instance.json
   ```

1. set environment variables for the scripts:
   ```sh
   export SECURITY_GROUP_ALLOWED_CIDR="$(curl --silent checkip.amazonaws.com)/32" 
   export SECURITY_GROUP_NAME="kali-lab"
   export SECURITY_GROUP_DESCRIPTION="Allow SSH and RDP traffic"
   export KEY_NAME="kali"
   ```

2. create a security group:
   ```sh
   ./create-security-group
   ```

3. create a key pair:
   ```sh
   ./create-key-pair
   ```

4. edit the `instance.json` file to add the property:

- `ImageId`: the Kali AMI ID (from **Pre-requisites**)
- also remove the `DryRun` property

5. create an EC2 instance:
   ```sh
   ./create-instance
   ```

6. find the instance ip:
   ```sh
   export INSTANCE_IP=$(./get-instance-ip)
   ```

7. connect to the instance via SSH:
   ```sh
   ./kali-ssh "${INSTANCE_IP}"
   ```

8. install a kali metapackage to get some tools:
   ```sh
   sudo apt install --yes kali-linux-headless
   ```

9. run the commands listed in [rdp-setup.md](rdp-setup.md)

10. connect via RDP client through the public ip with the username and password
    created in the previous step

## Next Steps

Set up some vulnerable infrastructure to test against !

Check out, for example, [AWSGoat](https://github.com/ine-labs/AWSGoat).

## Clean Up

Go to the AWS console and delete the resources created during the lab:

- EC2 instance
- SSH key pair
- Security group

## Author

**Andre Silva** - [@andreswebs](https://github.com/andreswebs)

## License

This project is licensed under the [Unlicense](UNLICENSE.md).

## References

<https://aws.amazon.com/security/penetration-testing/>

<https://www.kali.org/>

<https://remmina.org/>

<https://docs.aws.amazon.com/cli/latest/>

<https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-skeleton.html>

<https://serverfault.com/questions/981763/how-do-i-set-user-data-when-using-the-aws-cli-cli-input-json-argument>

<https://www.onemarcfifty.com/blog/video/How-to-build-Kali-Linux-from-Debian/>

<https://www.kali.org/docs/cloud/aws/>

<https://www.kali.org/docs/general-use/xfce-with-rdp/>

<https://github.com/ine-labs/AWSGoat>

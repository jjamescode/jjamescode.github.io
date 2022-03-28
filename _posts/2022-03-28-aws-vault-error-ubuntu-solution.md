# AWS-Vault Error Ubuntu Solution

AWS-Vault is a tool used to keep your AWS credentials hidden and secure. 
![ubuntu-aws-vault-error-solution](/images/ubuntu-aws-vault-error-solution.jpg)
When you install [AWS CLI tool](https://aws.amazon.com/cli/) from AWS, the default location stores your AWS credentials in plain text. This is dangerous because your credentials can be exposed to outsiders and may result in a huge AWS bill. AWS-Vault to the rescue. 

The installation instructions for installing AWS-Vault on a Linux computer are sparse. In fact they just list one command. There is no documentation to help with errors. So while installing using Homebrew is easy, it's not error free.

## AWS-Vault Not Found In Linux
The problem is after you successfully install AWS-Vault using Homebrew, after exiting the session and begining a new one, you'll get an error message saying *"AWS-Vault Not Found"*. So annoying. I had to keep reinstalling both AWS programs at the beginning of each session. The steps below outline how to install AWS CLI and AWS-Vault on Ubuntu Linux to prevent this problem.

## Install AWS CLI on Linux
Installing AWS CLI for Linux is pretty simple. You enter the following commands separately. 
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

See AWS Installation Guide 
[AWS Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) for more details.

The most important step is to locate the path where the program is installed. You'll need this later. "/usr/local/bin/aws" is the default location.

```
which aws 
/usr/local/bin/aws
```
## Install AWS-Vault For Linux Without Using Homebrew

Installing AWS-Vault using Homebrew while easy, resulted in a ton of problems for me. Installing AWS-Vault manually has proved to be less problematic.

## Step 1: Download latest release of AWS-Vault
Visit [99 Designs AWS-Vault repo ](https://github.com/99designs/aws-vault)for a link to the download. (There are 2 linux-amd64 links. I used the first one). Click link to download to your computer.

## Step 2: Change permissions on downloaded file
1. Change to Downloads folder
```
cd Downloads/ 
```
2. List files
```
ls
```
3. Make file executable
```
chmod +x aws-vault-linux-amd64
```
4. Path should end in same place you have the AWS CLI *"/usr/local/bin/aws"*
```
echo $PATH
```
5. Move file from Downloads folder to new location. You'll need to add *"aws-vault"* to Path.
```
mv aws-vault-linux-amd64 /usr/local/bin/aws-vault
```
6. Verify AWS-Vault was installed.
```
aws-vault --version
```

## Step 3: Add Profile Details to AWS-Vault
You'll need the secret credentials from your AWS User profile to complete this step. Simply go to **IAM > Users > Security Credentials** to get details.
You may need to create new access keys if you don't have your "Secret access key". Make the existing one inactive to delete it and then create a new one.

### Store AWS credentials to AWS-Vault
```
$ aws-vault add ProfileName
Enter Access Key Id: ABDCDEFDASDASF
Enter Secret Key: %%%
```
Linux will ask you to set a password for a keyring for AWS-Vault. Create a new password and store it securely. You'll need it.

## Step 4: Activate AWS-Vault in Linux
You must activate AWS-Vault for each new session. You can specify how long you want the computer to hold your credentials. I like to set my duration for 12hrs to give me flexibility. 

### Activate AWS-Vault
```
aws-vault exec ProfileName --duration=12h
```
### Verify AWS-Vault is working with the following commands. 
```
- aws sts get-caller-identity    or 
- aws vault list
```
## AWS-Vault Error
Occasionally you'll get an error saying
"aws-vault: error: exec: aws-vault sessions should be nested with care, unset AWS_VAULT to force"

```
unset AWS_VAULT"
```
This means that an existing aws-vault credential is already stored from a prior session. If you still have problems accessing aws-vault use the "unset AWS_VAULT" command to release the previous session. 

I hope this helps. Every time I closed Linux, I had to reinstall both AWS CLI and AWS-Vault to get them to work. Once I moved them both to the same $Path and installed manually instead of using Homebrew, I didn't have any more problems. Good luck.

Let's go through my project cloud vulnerability scanner
This is a A Python-based automated cloud security scanner that audits AWS environments for common misconfigurations in IAM roles, S3 buckets, and EC2 security groups using the boto3 SDK.

🚀 Features

*Scans AWS IAM for: Users without MFA
                 Overly permissive policies (Action: "*" or Resource: "*")
*Scans AWS S3 for: Public buckets
                Unencrypted buckets
                Missing bucket versioning
*Scans EC2 Security Groups for: Wide-open inbound rules (0.0.0.0/0)
                               Open SSH/RDP ports
*Simple Python CLI tool
*Uses AWS Access Key authentication
*Fully modular and easily extendable



You can directly go to the installation part in the end just to clone the scanner and use it.. if want to see how i did the whole this then just start to read from the next line..


Clear explaination on how i did it and also you can learn how to do it
I used Windows Vscode + WSL

open WSL terminal... 
now create a folder for this project and navigate to that folder
--> mkdir cloud_vuln_scanner
--> cd cloud_vuln_scanner

now open vscode through this wsl terminal so that in vscode we can use wsl
--> code .
type this in wsl terminal 
Now Vscode will be opened


To create a virtual environment-- In VScode terminal
--> sudo apt update
--> sudo apt install python3-venv -y   (module venv is used to create Python virtual environments)
--> python3 -m venv myvenv        (creating a environment named myvenv)


to activate the environment
--> source myvenv/bin/activate
Now it will enter into the myvenv virtual environment inside the VScode terminal

Install required python libraries
-->pip install boto3
-->pip install botocore


Now configure the aws
If aws cli is not installed, then
--> sudo apt install aws-cli -y

-->aws configure 
and give aws credentials like secret key and access key

But wait what will you give.. which one to give.. where do you find it...
We have to create an IAM USER so that this scanner is inside this user and can scan the aws account's services


Go to AWS console--> IAM--> USERS--> Create user with programmatic access and also add policies like only readonlyaccess and no access to change anything
like IAMReadOnlyAccess
     AmazonS3ReadOnlyAccess
     AmazonEC2ReadOnlyAccess

and after creating the IAM user --> create the access keys and save it

Now configure the aws cli credentials in the vscode terminal
--> aws configure

give the access keys


create the python file in this folder
vscode-->file-->newfile-->cloud-vuln-scanner.py

paste the code in my repository in the python file-- save it


now run the script
python3 cloud-vuln-scanner.py

you can see the output





🛠️ Installation
1️⃣ Clone the repository (or download your own code)
git clone https://github.com/YOUR_USERNAME/cloudvuln-scanner.git    // go to my repository and copy the pathhhh to clone it.....
cd cloudvuln-scanner

2️⃣ Create & activate virtual environment (WSL)
python3 -m venv myvenv
source myvenv/bin/activate

3️⃣ Install dependencies
pip install -r requirements.txt

🔐 AWS Credentials Setup
Option A: Use IAM Access Keys (Recommended for this project)

Go to AWS Console → IAM

Open your IAM User → Security Credentials

Under “Access Keys” → click Create access key

Select Command Line Interface (CLI)

Copy Access Key ID and Secret Access Key

Then configure in WSL:

aws configure


Enter the credentials when asked.

▶️ Running the Scanner

Inside your virtual environment:
--> python3 cloud_vuln_scanner.py

📄 Output

The tool prints:
Issues found
Services scanned
Summary report









The output will be like this

--- Running CloudVuln Scanner ---

Security Findings:
 - [HIGH] IAM Role 'cdk-hnb659fds-cfn-exec-role-793976186299-us-east-1' has admin (*:* permissions).
 - [HIGH] Security Group 'launch-wizard-2' (sg-014b9d89af6ced762) allows 0.0.0.0/0 on port 80
 - [HIGH] Security Group 'launch-wizard-2' (sg-014b9d89af6ced762) allows 0.0.0.0/0 on port 22
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 80
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 1805
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 8000
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 22
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 5000
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 8999
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 8086
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 8082
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 3000
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 3306
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 8088
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 443
 - [HIGH] Security Group 'launch-wizard-1' (sg-011451653a45f17bd) allows 0.0.0.0/0 on port 8081
 - [HIGH] Security Group 'default' (sg-062bded0e6b8c816b) allows 0.0.0.0/0 on port 8080
 - [HIGH] Security Group 'default' (sg-062bded0e6b8c816b) allows 0.0.0.0/0 on port 8000
 - [HIGH] Security Group 'default' (sg-062bded0e6b8c816b) allows 0.0.0.0/0 on port 1805
 - [HIGH] Security Group 'default' (sg-062bded0e6b8c816b) allows 0.0.0.0/0 on port 22
 - [HIGH] Security Group 'launch-wizard-3' (sg-0b00e374f595f86dc) allows 0.0.0.0/0 on port 1805
 - [HIGH] Security Group 'launch-wizard-3' (sg-0b00e374f595f86dc) allows 0.0.0.0/0 on port 22
 - [HIGH] Security Group 'launch-wizard-3' (sg-0b00e374f595f86dc) allows 0.0.0.0/0 on port 3000
 - [HIGH] Security Group 'ec2_ebs1' (sg-08633e8fcbbb0633b) allows 0.0.0.0/0 on port 22
 - [HIGH] Security Group 'launch-wizard-4' (sg-0a27ea73c534bcab2) allows 0.0.0.0/0 on port 80
 - [HIGH] Security Group 'launch-wizard-4' (sg-0a27ea73c534bcab2) allows 0.0.0.0/0 on port 22
 - [HIGH] Security Group 'launch-wizard-4' (sg-0a27ea73c534bcab2) allows 0.0.0.0/0 on port 443

--- Scan Complete ---

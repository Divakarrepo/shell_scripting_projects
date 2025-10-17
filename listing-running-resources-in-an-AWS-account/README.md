# listing-all-the-resources-in-an-AWS-account
Script to automate the process of listing all the resources in an AWS account

🧩 Step-by-Step Explanation

1️⃣ Argument Check

if [ $# -ne 2 ]; then

    echo "Usage: ./aws_resource_list.sh <aws_region> <aws_service>"
    
    echo "Example: ./aws_resource_list.sh us-east-1 ec2"
    
    exit 1
fi

$# → **number of arguments passed to the script.**

It expects exactly 2 arguments

AWS Region (us-east-1, ap-south-1, etc.)

AWS Service (ec2, s3, etc.)

If not provided → shows usage help and exits.

2️⃣ Assigning Variables

aws_region=$1

aws_service=$2

$1 → first argument (AWS region)

$2 → second argument (AWS service name)

3️⃣ Check if AWS CLI is Installed

if ! command -v aws &> /dev/null; then

    echo "AWS CLI is not installed. Please install the AWS CLI and try again."
    
    exit 1
    
fi
! → **not exists**

Uses **command -v aws** to check if AWS CLI exists in system PATH.

if its available redirect the output in to empthy path ie. **/dev/null**

If not found → prints error and exits.

4️⃣ Check if AWS CLI is Configured

if [ ! -d ~/.aws ]; then

    echo "AWS CLI is not configured. Please configure the AWS CLI and try again."
    
    exit 1
    
fi

Checks if AWS config directory (~/.aws) exists.

If not → means aws configure hasn’t been run, so it exits.

5️⃣ Service-Based AWS Resource Listing

The **case** block handles different AWS services.

case $aws_service in

    ec2)
    
        echo "Listing EC2 Instances in $aws_region"
        
        aws ec2 describe-instances --region $aws_region
        ;;
        .
        .
        .
      esac
      
case ... esac is like **switch** in other languages.

For each supported service (e.g., ec2, s3, rds...), it runs the corresponding AWS CLI command.

6️⃣ Invalid Service Handler

      *)
          echo "Invalid service. Please enter a valid service."
          
          exit 1
          
          ;;
(*) → otherthen everything

If user enters a service not in the list → prints error and exits.

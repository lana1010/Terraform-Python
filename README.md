# Terraform-Python
This project includes 2 tasks:
* Terraform - creates AWS S3 bucket with no public access, with versioning turned off, and a bucket_name provided as a user's input.
* Python - a python script that populates the bucket, able to delete these objects and describe them as well. The script takes 3 arguments: uploaded files, delete files, and description.

**Terraform**

To use Terraform, first check if it installed on your host. Run 'terraform -version' command on any platform. If it's not installed, you can install it 
on Linux: sudo apt terraform --classic,
on Windows - check this link https://learn.microsoft.com/en-us/azure/developer/terraform/get-started-windows-bash?tabs=bash

Create AWS User and save its AWS_ACCESS_KEY, AWS_SECRET_ACCESS_KEY.
Clone Git repository:
git clone https://github.com/lana1010/Terraform-Python

**Usage**

1) Go to S3-manipulations folder: cd /Terraform/S3-manipulations

2) Update file terraform.tfvars: change values for variables 'bucket_name' and 'location' for those that you need. Location is avalability zone that is more geographically close to you. Check availble zones here https://awsregion.info/ By default it set to 'location = us-east-1'.

3) Set Environment Variables for current session:
    * Linux:   
      export AWS_ACCESS_KEY_ID=<YOUR_AWS_ACCESS_KEY>
      export AWS_SECRET_ACCESS_KEY=<YOUR_AWS_SECRET_ACCESS_KEY>
    * Windows: 
      set AWS_ACCESS_KEY_ID=<YOUR_AWS_ACCESS_KEY>
      set AWS_SECRET_ACCESS_KEY=<YOUR_AWS_SECRET_ACCESS_KEY>
4) Run terraform init

5) Run terraform plan. Verify that the preliminary execution goes fine.

6) Execute: terraform apply.

To verify the S3 bucket is created, go to AWS Console and check it exists with yout given bucket_name from terraform.tfvars file.

**Python**

To run successfully this script, verify if boto3 library is installed on your host. If not, install it on
Linux: sudo apt install boto3
Windows: pip install boto3

Use the same AWS User's credentials.

**Usage**

1) Go to Python folder: cd /Python

2) Set Environment Variables for the current session, see above.

3) If you need to update AWS Region value, open file and change 'AWS_DAFAULT_REGION' value.                        
   By default it's us-west-1.

4) Run Python script:                                                                            
   python s3_operations.py <bucket_name> --upload <file_paths> --delete <object_keys> --describe,                    
   where <bucket_name> is your S3 bucket name, <file_paths> is one or more absolute path to the files to be uploaded, 
         <object_keys> is one or more object/file names to be removed from the S3 bucket.

For example:                                                                                               
python s3_operations.py lana-s3-test1 --upload index.html image.jpg notes.txt --delete notes.txt --describe

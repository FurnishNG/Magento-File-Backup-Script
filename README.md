# Magento File Backup Script
This bash script automates the process of backing up your Magento root directory and uploading the backup file to an S3 bucket
It can equally be used for backing up any other folder.

<h2>Prerequisite</h2>
1.Ensure that AWS CLI is fully installed on your server and AWS credentials setup for root and/or {user}

On Ubuntu:

\# aptitude install awscli

2.After installation, run:

\# aws configure

Set up your AWS Access Key ID, AWS Secret Access Key, Default region name, and Default output format.

See http://aws.amazon.com/documentation/cli/ for the AWS CLI Documentation

3.Install mailutils

\# aptitude install mailutils

<h2>To use the script:</h2>
Download from GitHub and upload to your server or clone from GitHub, and make it executable.

\# cd /home/{username}/bin/

\# git clone https://github.com/FurnishNG/Magento-File-Backup-Script.git

\# mv Magento-File-Backup-Script/Magento-File-Backup-Script magento-file-backup.sh

\# chmod og+x magento-file-backup.sh

If you have access to root privileges, you can save it to /usr/local/bin/magento-file-backup.sh

If you do not have access to root privileges, you can save it to /home/{username}/bin/magento-file-backup.sh.
Ensure that you have read and execute privileges to the Magento Root Directory.

If you have root privileges:
\# chmod og+x /usr/local/bin/magento-file-backup.sh

Alternatively, 

Open up Nano Editor

\# nano /usr/local/bin/magento-file-backup.sh

Copy code from https://github.com/FurnishNG/Magento-File-Backup-Script/blob/master/Magento-File-Backup-Script
and paste into Nano Editor.

On Line 45, set your Base Directory with no trailing slashes.

On Line 107, set your Magento Root Folder with no trailing slashes.

On Line 165, set your S3 Bucket with no trailing slashes.

//  Please do not use s3://backups or s3:/file-backups as your S3 bucket name. Those are reserved S3 bucket names.

//	Also note that underscores are not allowed in bucket names. Limit symbols to hypens and dots.

//	Please do not add a trailing slash to the $S3_BUCKET variable

Write out and exit Nano Editor

In Nano Editor:

CTRL + X

Type "Y" and click Enter

You can run directly on Bash shell

As root:

\# cd /usr/local/bin/

Or as user:

\# cd /home/{username}/bin/

Then execute:

\# ./magento-file-backup.sh

To automate the backup process, set up a Cron job

For root:

\# crontab -e

For {user}

\# crontab -u {username} -e

Using Nano Editor, paste the following to run the job daily at 11:50PM

50 23 * * * /usr/local/bin/magento-file-backup.sh 2>&1 | tee output.txt | mail -s "Magento Filesystem Backup Cron Job" admin@example.com

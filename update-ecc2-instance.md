# How to update EC2 Instance

## Extend EBS columns (zero downtime)
1. Backup data
2. Create snapshot (If change instance type, creating image will create a snapshot so this step can be skipped)
![Create snapshot](images/update-ec2/image3.png)
3. Modify volume
![Modify volume](images/update-ec2/image1.png)
4. Check in server with command `df -h`

## Change instance type
1. Verify Elastic IP
![Modify volume](images/update-ec2/image4.png)
2. Create Image
3. Stop instance
![Stop instance](images/update-ec2/image2.png)
4. Change instance type
![Change instance type](images/update-ec2/image5.png)
5. Start instance
6. Check in server with command `top`

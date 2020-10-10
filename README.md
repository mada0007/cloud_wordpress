# cloud_wordpress
Cloudformation template to create Wordpress website on an EC2 instance using an RDS mysql database, all in a newly created VPC with a new route53 record to host the website in a subdomain on an existing hosted zone.


Requirements: 
- Route 53 Hosted Zone

Changes to make: 
- Change initialDomain on Route53.yaml to your Route53 domain
- Upload RDS/VPC/EC2/Route53 files to S3
- Change master TemplateURL under each stack to reflect the new S3 URL's

If you need SSH:
- Replace SSH KEY GOES HERE below with your public SSH key
- Add the code below to the EC2.yaml Userdata section
- Connect with [ssh -i "privateKey" member@EC2IP]

#!/bin/bash  
USER1=member  
adduser $USER1 && mkdir /home/$USER1/.ssh && chmod 700 /home/$USER1/.ssh  
echo "SSH KEY GOES HERE" > /home/$USER1/.ssh/authorized_keys  
chmod 600 /home/$USER1/.ssh/authorized_keys  
chown -R $USER1:$USER1 /home/$USER1/.ssh  
echo "$USER1 ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers  

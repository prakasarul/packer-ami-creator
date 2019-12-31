#aws cli to list images from Redhat owner
aws ec2 describe-images --owners 309956199498 --filters "Name=is-public,Values=true" "Name=name,Values=RHEL-7.7*" --region ap-south-1 --output text

#Packer-cli

#build command
packer build rhel.json

#Build with vars
packer build -var "aws_access_key=key" -var "aws_secret_key=key" rhel1.json

#Build with var file
packer build -var-file variables.json rhel1.json


#aws cli to test newly created image
aws ec2 run-instances --instance-type t2.micro --count 1 --key-name rhel-key --image-id <newlycreatedImage> 


#Download nginx role from galaxy site
ansible-galaxy install -r requirements_ngx.yml 
OR
ansible-galaxy install nginxinc.nginx

#Run in debug mode 

 packer build -debug rhel_ngx_ansible.json

 #Run with log files

PACKER_LOG=1 packer build -debug rhel_ngx_ansible.json

PACKER_LOG=1 packer build -debug rhel_ngx_ansible.json|& tee debug.txt 


#Server Hardening role to download from galaxy 
ansible-galaxy install -r requirements_serverhard.yml 

#Build with hardend roles 
packer build rhel_hard_ansible.json



#Validate the syntax packer 
packer validate rhel1.json

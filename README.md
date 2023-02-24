# gns3-gcloud
GNS3 over Google cloud Compute Engine

Tested on February 2023

GNS3 server version: 2.2.37
Compute Engine : debian 11- 

# Create VM  
Open your cloud-shell on your project

### Verify zone 
gcloud compute zones list


### Create firewall rule
NOTE: 
gcloud compute firewall-rules create ssh-gns3 \
  --direction=INGRESS \
  --action=allow \
  --rules=tcp:22,tcp:3080 \
  --source-ranges=<PUBLIC_IPCIDR/28>
  
### Select CPU "Intel Haswell"

gcloud compute instances create VM_NAME \
  --enable-nested-virtualization \
  --zone=us-west1-b \
  --min-cpu-platform="Intel Haswell"

### ingress VML1 ( your Cloud Compute VM)
gcloud compute ssh gns3server --zone=us-west1-b  
  
### Verify virtualization 
grep -cw vmx /proc/cpuinfo

# To ingres outside SSH  (linux)
Open your local computer  (ex: your laptop with OS debian, ubuntu etc)
### create ssh keys

ssh-keygen
EXAMPLE: directory path is /home/JonsLaptop/.ssh/id_rsa,/home/JonsLaptop/.ssh/id_rsa.pub

### Copy files to VM Instance

Example: diretory path for cloud-shell doc/id_rsa.pub

gcloud compute os-login ssh-keys add \
    --key-file= doc/id_rsa.pub \
    --project=your_project 

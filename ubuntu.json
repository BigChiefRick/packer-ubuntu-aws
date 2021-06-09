{
  "variables": {
    "aws_access_key": "",
    "aws_secret_key": "",
    "region" : "us-east-1"
     },
	"builders": [
    {
      "type": "amazon-ebs",
      "access_key": "{{user `aws_access_key`}}",
      "secret_key": "{{user `aws_secret_key`}}",
      "region": "{{user `region`}}",
      "source_ami": "ami-0817d428a6fb68645",
      "vpc_id": "vpc-0fe5523276e3e4ca5",
      "subnet_id": "subnet-04092d2c00cdd0ba6",
      "instance_type": "t2.micro",
      "ssh_username": "ubuntu",
      "associate_public_ip_address": "true",
      "ami_name": "Ubuntu-AIP{{timestamp}}"
    }
 ],
 "provisioners": [
     {
      "type": "file",
      "source": "./linux-client-bundle.zip",
      "destination": "/tmp/"
    },
 {
      "type": "file",
      "source": "NessusAgent-8.2.2-ubuntu1110_amd64.deb",
      "destination": "/tmp/"
    },

	 
    {"type": "shell",
       "inline":["sudo apt-get update && sudo apt -y upgrade"]},
    {
  "type": "shell",
  "inline": ["sleep 20"]},
    {"type": "shell",
       "inline":["sudo apt install -y jq unzip",
	        "sudo dpkg -i /tmp/NessusAgent-* && sudo  /opt/nessus_agent/sbin/nessuscli agent link --host=nmanager.itsec.tamu.edu --port=8834 --key=2c165f682a11309b7bfca1a82e2c0c191025ab068d2af02122b6277ef84bc298 --group=AIP",
                "sudo unzip /tmp/linux-client-bundle.zip -d /tmp",
                "sudo chmod +x /tmp/install.sh",
                "cd /tmp && sudo ./install.sh",
                "sudo apt -y upgrade"]},   
    {"type": "shell",
     "script": "falcon-download.sh"}
  ]
}

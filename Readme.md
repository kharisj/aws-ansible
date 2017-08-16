*Properties of Kharis Jirvaranunt The Marlo Group Thailand*
# Requirements:
 1. vagrant:
 2. virtualbox:
 3. aws-account:
    - aws-credential-key:
    - aws-secret-key:
 4. aws-network:
    - aws-vpc-with-subnet:
    - aws-vpn-security-allow-ports:
      - 8443
      - 22
      - application-ports
 5. aws-key(ssh)
    - key-name:
    - key-file: (.pem) -- place it in root directory of project
 
# Steps:
  1. git clone project and goto directory
  2. vagrant up && vagrant rsync-auto
  3. open another console and vagrant ssh
  4. goto /vagrant/source directory
  5. define variables in .yml files at /vagrant/sources/vars directory
      - common.yml
        - aws_access_key
        - aws_secret_key
        - region
          -  code: "ap-southeast-1" # for sg based
             - oc_subnet: "subnet-xxxxxxxx" #OpenShift subnet
             - centos7:
               - code: "ami-xxxxxxxx"
               - user: "ec2-user"
             - keyname: "xxx"
             - keyfile: "/vagrant/xxx.pem"
      - vm_details.yml
        - cluster_name
        - owner
        - class
  6. command: sudo ansible-playbook /vagrant/sources/manifest.yml
  7. define hosts file in Windows/Linux
      - Windows [C:/Windows/system32/drivers/etc/hosts]
      - Linux [/etc/hosts]
      - Add following line to hosts file
        ```
        $proxy_ip_address  $clustername
        ```
  8. define password for openshift origin web-console
      - ssh to oc_master0 and configure username:password by htpasswd command
        ```
        > vagrant ssh
        vagrant]$ ssh -i $keyfile $username@oc_master0.$clustername
        ec2-user]# sudo htpasswd -b /etc/origin/master/htpasswd admin:$password
        ```
  9. login to webconsole and start project via [https://$clustername:8443/console/](https://$clustername:8443/console/)
  ![](images/login-console.PNG?raw=true)
  ![](images/project-console.PNG?raw=true)
  
  
  
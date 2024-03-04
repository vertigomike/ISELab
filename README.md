# ISELab
 Automation to build ISE deployment on Proxmox

This contains files used to build out a fully function lab deployment of ISE 3.2 on Proxmox 8.1x

The files are:
proxcreate.yml - Build out a complete setup of 8 ISE VM nodes using eval sizing.  This can be modified to add/move nodes as necessary for your specific setup also also adjust CPU/Memory/Disk space to meet your desired node nodes
proxremove.yml - Stop and remove the 8 ISE VM nodes deployed previously via proxcreate.yml.  This can also be modified to as necessary for specific setup
newise.yml     - This playbook will build out personas on the previously deployed nodes.  This script sets up two admin, two monitoring and four policy nodes from the previously deployed VMs.  This can be modified to fit your specific needs.  This should only be run after all the aforementioned nodes have been deployed, patched, and services on all nodes are running.  This may take 60-90 minutes.
check.yml      - This playbook will check all the nodes to make sure application server is started by checking the login.jsp for a HTTP/200 status
check1.yml	- This ploybook will be called by the check.yml and newise.yml files in order to check specific node statuses.  By default. This will wait a check amount of time and retries.  This can be adjusted to meet your needs if your lab is maybe slower to start/build.  In most cases 15min is a appropriate time to wait for services to come up after restart
sample.conf	- sample ZTP configuration file.  This is used as part of the proxcreate.yml file to stage each nodes setup.  You'll modify this file and then use the create_ztp_image.sh file to build a .img file for each node.  This isn't required but automates the CLI configuration of each node.  More details on the ZTP process is available on Cisco's site at https://community.cisco.com/t5/security-knowledge-base/ise-zero-touch-provisioning-ztp/ta-p/4541606


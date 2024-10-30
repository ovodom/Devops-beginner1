# Deploying the Prometheus Stack using Docker Compose

**Introduction:**

1.	Prometheus: Prometheus is an open-source monitoring system designed to collect metrics from various sources, such as application and system performance data, and store them in a time-series database. It scrapes metrics from exporters, processes them, and provides this data to visualization tools like Grafana for real-time monitoring and alerting.

2.	On this project, Prometheus will work with Alert Manager, Node Exporter, Grafana, Terraform(this is to generate server), Docker, and Docker Compose.

**Procedure:**

**1.	Spin up an Ubuntu 24.04 EC2 Instance and connect your instance via ssh.**


•	Visit I AM page on AWS to gain access to AmazonVPCFullAccess
•	AmazonEC2FullAccess



![1](img/img1.png)



![1](img/IMG2.png)



![1](img/img3.png)



![1](img/img4.png)



![1](img/img5.png)



![1](img/IMG6.png)



![1](img/IMG7.png)



![1](img/img8.png)



![1](img/img8.png)




**2.	Provision server using Terraform**

- a. Connect your Instance via SSH

- b. Clone the project repository to your instance


```
git clone https://github.com/TobiOlajumoke/prometheus-observability-stack

```



![2](img/img10.png)




cd into prometheus-observability-stack folder to get the project code.


```
cd prometheus-observability-stack
```


![2](img/img11.png)




- c. Install Terraform


```
sudo snap install terraform --classic
```


![2](img/img12.png)




**3. Provision Server Using Terraform**

- a. Modify the values of ec2.tfvars file present in the terraform-aws/vars folder

```
cd terraform-aws/vars

```


![3](img/img13.png)



- b. If you are using us-west-2, you can continue with the same AMI ID else change the AMI ID

```
vi ec2.tfvars
```



![3](img/img14.png)




```
# EC2 Instance Variables
region         = "us-west-2"
ami_id         = "ami-0aff18ec83b712f05"
instance_type  = "t2.large"
key_name       = "add keyname"
instance_count = 1
volume-size = 20

# VPC id
vpc_id  = "add a vpc"
subnet_ids     = "add a subnet"

# Ec2 Tags
name        = "prometheus-stack"
owner       = "devops-mastery"
environment = "dev"
cost_center = "devops-project"
application = "monitoring"

# CIDR Ingress Variables
create_ingress_cidr        = true
ingress_cidr_from_port     = [22, 80, 443, 9090, 9100, 9093, 3000]  # List of from ports
ingress_cidr_to_port       = [22, 80, 443, 9090, 9100, 9093, 3000]  # List of to ports
ingress_cidr_protocol      = ["tcp", "tcp", "tcp", "tcp", "tcp", "tcp", "tcp"]        # Protocol for all rules (you can add more if needed)
ingress_cidr_block         = ["0.0.0.0/0", "0.0.0.0/0", "0.0.0.0/0", "0.0.0.0/0", "0.0.0.0/0", "0.0.0.0/0", "0.0.0.0/0"]
ingress_cidr_description   = ["SSH", "HTTP", "HTTPS", "Prometheus", "Node-exporter", "Alert manager", "Grafana"]

# CIDR Egress Variables
create_egress_cidr    = true
egress_cidr_from_port = [0]
egress_cidr_to_port   = [0]
egress_cidr_protocol  = ["-1"]
egress_cidr_block     = ["0.0.0.0/0"]

```



![3](img/img15.png)



Now we can provision the AWS EC2 & Security group using Terraform.

```
cd ../prometheus-stack

```



![3](img/img16.png)



```
terraform fmt
```



![3](img/img17.png)



```
terraform init
```



![3](img/img18.png)



```
terraform validate
```



![3](img/img19.png)



Execute the plan and apply the changes.

```
terraform plan --var-file=../vars/ec2.tfvars
```



![3](img/img20.png)



```
terraform apply --var-file=../vars/ec2.tfvars
```



![3](img/img21.png)



![3](img/img22.png)



![3](img/img25.png)




**4.	Connect to your new Instance**



![4](img/img26.png)



![4](img/img27.png)



Run the following command on your new instance:

```
tail /var/log/cloud-init-output.log
```
This is to check the cloud-init logs to see if the user data script has run successfully. An example output is shown below. It should show Docker and Docker compose versions as highlighted in the image.


![4](img/img28.png)



![4](img/img29.png)



verify the docker and docker-compose versions again.



```
sudo docker version
```



![4](img/img30.png)



![4](img/img31.png)



```
sudo docker-compose version
```


![4](img/img32.png)



**5.	Deploy Prometheus Stack using Docker Compose**

First, clone the project code repository to the server.

```
git clone https://github.com/TobiOlajumoke/prometheus-observability-stack
```



![5](img/img34.png)




```
cd prometheus-observability-stack
```



![5](img/img35.png)



continue with the following command: 

```
make all
```



![5](img/img35.png)



![5](img/img36.png)



Bring up the stack using Docker Compose. It will deploy Prometheus, Alert manager, Node exporter and Grafana.


```
sudo docker-compose up -d
```



On a successful execution, you should see the following output saying Running 5/5



![5](img/img37.png)



![5](img/img38.png)




**6.	Validate Prometheus Node Exporter Metrics**

If you visit http://your-public-ip-address:9090, you will be able to access the Prometheus dashboard as shown below.

Validate the targets, rules and configurations as shown below. The target would be Node exporter url.




![6](img/img39.png)




![6](img/img40.png)



![6](img/img41.png)



![6](img/img42.png)



![6](img/img43.png)



![6](img/img44.png)



**7.	Validating Prometheus Rules and Targets**

Now lets execute a promQL statement to view node_cpu_seconds_total metrics scrapped from the node exporter.


```
avg by (instance,mode) (irate(node_cpu_seconds_total{mode!='idle'}[1m]))
```



![7](img/img46.png)



![7](img/img47.png)



You should be able to data in graph as shown below.



![7](img/img48.png)



![7](img/img49.png)



![7](img/img50.png)




**8.	Configure Grafana Dashboards**

Grafana can be accessed at: http://your-ip-address:3000




![8](img/img51.png)



![8](img/img52.png)



![8](img/img53.png)



![8](img/img54.png)



![8](img/img55.png)



![8](img/img56.png)



![8](img/img57.png)




**9.	Configure Node Exporter Dashboard**



![9](img/img58.png)



![9](img/img59.png)



![9](img/img60.png)



![9](img/img61.png)



![9](img/img62.png)



Once the dashbaord template is imported, you should be able to see all the node exporter metrics as shown below.



![9](img/img63.png)




**10.	Simulate and Test Alert Manager Alerts**

You can access the Alertmanager dashbaord on http://your-ip-address:9093



![10](img/img64.png)



Alert rules are already backed in to the prometheus configuration through alertrules.yaml. If you go the alerts option in the prometheus menu, you will be able to see the configured alerts as shown below. http://your-ip-address:9090



![10](img/img65.png)



![10](img/img66.png)



Run the following command:

```
sudo docker exec -it prometheus promtool check rules /etc/prometheus/alertrules.yml
```



**11.	Test: High Storage & CPU Alert**



```
dd if=/dev/zero of=testfile_16GB bs=1M count=16384; openssl speed -multi $(nproc --all) &
```



![11](img/img67.png)



![11](img/img68%20(2).png)



![11](img/img69.png)




**12.	Cleanup The Setup**

To tear down the setup, execute the following terraform command from your workstation.


```
cd prometheus-observability-stack/terraform-aws/prometheus-stack
```

```
terraform destroy --var-file=../vars/ec2.tfvars
```


![12](img/img70.png)



![12](img/img73.png)



![12](img/img74.png)




![12](img/img75.png)




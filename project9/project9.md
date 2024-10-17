# Dockerizing Flask Application

**Procedure:**

**1.	Provision of an Instance**


- Spin up an Ubuntu 24.04 t2.micro this is where we'll be doing the project in


- SSH into the instance


**2.	Install and start Docker**

- Update your package index for ubuntu

```
sudo apt update
```




![2](img/img1.png)



- Install Docker:

```
sudo apt install docker.io -y
```




![2](img/img2.png)



- Start Docker:

```
sudo systemctl start docker
sudo systemctl enable docker
```



![2](img/img3.png)




- Check the Status of Docker

```
sudo systemctl status docker
```



![2](img/img4.png)



![2](img/img5.png)




- ctrl + c to exit the running docker


**3.	Clone the Docker project**

- Clone the project repository:

```
git clone https://github.com/TobiOlajumoke/docker-flask
cd docker-flask
```



![3](img/img6.png)




**4.	Run the Docker Application**


- Build the Docker Image:


```
docker build -t flask-application:1.0.0 .
```


![4](img/img7.png)



![4](img/img8.png)


- Check if the image built


```
sudo docker images
```



![4](img/img9.png)




![4](img/img10.png)


- Run the Docker Container:

```
docker run -d -p 8000:8000 flask-application:1.0.0

```




![4](img/img12.png)




Test in Browser Now, go to your browser and access your EC2 public IP to check if the app is running properly:

```
http://<your-ec2-public-ip>:8000

```



![4](img/img13.png)



The webpage will not work, WHY?

we have not added the port 8000 to our security group of our instance so do that and try accessing the EC2 public IP



![4](img/img14.png)




![4](img/img15.png)




**5.	Push Image to the Docker Hub**



- Go to your Docker hub account and create a repo



![5](img/img16.png)



![5](img/img17.png)



- Log In to Docker Hub from Your Terminal

Use the Docker CLI to log in to your Docker Hub account:

```
sudo docker login

```

You will be prompted to enter your Docker Hub username and password



![5](img/img18.png)



![5](img/img19.png)



![5](img/img20.png)



- Tag Your Image

```
<your-dockerhub-username>/<repository-name>:<tag>
```


For example:

```
sudo docker tag flask-application:1.0.0 yourusername/flask-application:1.0.0

```





![5](img/img22.png)





- Push the Image to Docker Hub



![5](img/img23.png)




![5](img/img24.png)




**6.	Verify the push**



![6](img/img25.png)




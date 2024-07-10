# Django Dockerized Web Application

This repository contains the necessary files to deploy a Django web application as a Docker container. Follow the instructions below to set up and run the application on your local machine or a cloud instance, such as AWS EC2.

## Prerequisites

- Basic knowledge of Docker , Django, and EC2 of AWS .

## Installing Docker

### Windows

1. Download Docker Desktop from the [Docker Hub](https://hub.docker.com/editions/community/docker-ce-desktop-windows).
2. Run the installer.
3. Follow the installation instructions.
4. Once installed, Docker will start automatically. You can also manually start Docker from the Start menu.

### macOS

1. Download Docker Desktop for Mac from the [Docker Hub](https://hub.docker.com/editions/community/docker-ce-desktop-mac).
2. Open the downloaded file and drag Docker to the Applications folder.
3. Open Docker from the Applications folder.
4. Follow the installation instructions.

### Linux

#### Ubuntu

1. Update your package list and install necessary dependencies:

    ```bash
    sudo apt-get update
    sudo apt-get install \
        ca-certificates \
        curl \
        gnupg \
        lsb-release
    ```

2. Add Docker’s official GPG key:

    ```bash
    sudo mkdir -p /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    ```

3. Set up the Docker repository:

    ```bash
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```

4. Install Docker Engine:

    ```bash
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
    ```

5. Verify Docker is installed correctly by running the hello-world image:

    ```bash
    sudo docker run hello-world
    ```

#### Other Distributions

For other Linux distributions, please refer to the [official Docker installation guide](https://docs.docker.com/engine/install/).

## Getting Started

### Clone the Repository

```bash
git clone https://github.com/Kcubez/To-do-List-DjangoApp.git
cd To-do-List-DjangoApp
```

### Build the Docker Image
```bash
docker build .
```
### Search the Docker Image ID
```bash
docker images
```
### Run the Docker container
```bash
docker run -p 8000:8000 -it your-docker-image-id
```

### Access the Application
Open your web browser and go to http://localhost:8000 to see the running Django application.


### Setting Up on AWS EC2

Launch an EC2 Instance

- Go to the AWS Management Console and launch an EC2 instance.

- Choose an Amazon Machine Image (AMI), such as Amazon Linux 2 or Ubuntu.

- Select an instance type, such as t2.micro, which is eligible for the free tier.

- Configure the instance details, add storage, and configure security groups. Make sure to add a rule to allow inbound traffic on port 8000.
    
- Launch the instance and connect to it via SSH.

### Install Docker on EC2

Connect to your EC2 instance using SSH:
```bash
ssh -i /path/to/your-key-pair.pem ec2-user@your-ec2-instance-public-dns
```
Update the package list and install Docker:
```bash
sudo apt update
sudo apt install docker.io -y
```

### Start Docker daemon
You use the below command to verify if the docker daemon is actually started and Active
```bash
sudo systemctl status docker
```
If you notice that the docker daemon is not running, you can start the daemon using the below command

```bash
sudo systemctl start docker
```
### Grant Access to your user to run docker commands
To grant access to your user to run the docker command, you should add the user to the Docker Linux group. Docker group is create by default when docker is installed.
```bash
sudo usermod -aG docker ubuntu
```
In the above command `ubuntu` is the name of the user, you can change the username appropriately.

### Clone this repository
```bash
git clone https://github.com/Kcubez/To-do-List-DjangoApp.git
cd To-do-List-DjangoApp
```
### Login to Docker [Create an account with https://hub.docker.com/]
```bash
docker login
```
```
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: kcube
Password:
WARNING! Your password will be stored unencrypted in /home/ubuntu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```

### Build the Docker Image on EC2
```bash
docker build -t todo
```
### Verify the Docker Image
```bash
docker images
```

### Run the Docker Container
```bash
docker run -t 8000:8000 -it your-image-id
```

---

### Open your web browser and go to http://your-ec2-instance-public-dns:8000/todo to see the running Django application.

---
### Project Structure

-	Dockerfile: Instructions to build the Docker image.

-	requirements.txt: Python dependencies for the Django application.
-	src/: Source code of the Django application.
-	settings.py: Configuration for the Django project.
-	urls.py: URL routing for the application.
-	views.py: Logic for handling requests and responses.
-	templates/: HTML templates for the application.

### Dockerfile Explained

-	Base Image: Using ubuntu as the base image.

-	Working Directory: Set to /app.
-	Copy Requirements: Copy requirements.txt to the working directory.
-	Install Dependencies: Install Python and required packages.
-	Copy Source Code: Copy the Django application source code to the working directory.
-	Set Entry Point: Define the entry point for the container to run the Django application.

### Running the Application

-	Build the Image: docker build -t todo .

-	Run the Container: docker run -p 8000:8000 -it your-image-id

Ensure you have the necessary ports open in your firewall or security groups if running on a cloud instance.

### Troubleshooting

- Port Conflicts: If port 8000 is already in use, change the mapping in the docker run command (-p 8000:8000).

- Dependency Issues: Ensure all dependencies in requirements.txt are correct and compatible with your application.

### Contributing

Feel free to fork this repository, make improvements, and submit pull requests. For major changes, please open an issue first to discuss what you would like to change.

---

### Reference
https://www.youtube.com/watch?v=3IAvr_O6vao

### Questions and Feedback

If you have any questions or feedback, please open an issue or contact me at kcubez21@gmail.com.

---
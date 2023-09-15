# Deployment of a Django To-Do Application on Kubernetes 
![maxresdefault](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/ecd546e3-d28a-419e-a1dd-aad9ce46ee40)

## Create jenkinsfile and push to GitHub.

![Screenshot 2023-09-15 193857](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/eba40c2a-0781-4551-a009-6cad7285bcc2)


## Create EC2 Instance (t2.micro), Install Docker and Jenkins, add jenkins and USER to docker group.
```
$ sudo usermod -aG docker $user
$ sudo usermod -aG docker jenkins
```

Access jenkins using ec2 ip address and 8080 port number 
**<ec2_ip_address>:8080**

![Screenshot 2023-09-14 045631](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/a1905dd0-f0f2-4217-b843-da969e4e70e6)


In Jenkins go to **manage** -> **credentials** 

![Screenshot 2023-09-14 045410](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/f1dd1318-5356-4725-a9a8-774fb2f7f4f6)


In **system** -> **global credentials** -> **add credentials**

![Screenshot 2023-09-14 045444](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/0292cab1-0816-4ca4-a37c-5aed312f9e25)

**add docker ID, Username, Password and save it**

![Screenshot 2023-09-14 045600](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/d535a13f-6e80-4582-8ab0-33b5feab8a4f)

**Now Docker credential has been created**

![Screenshot 2023-09-14 045608](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/1daadadc-4ef0-4fb4-a1bd-1edd556dbb19)


## create **new item** 

![Screenshot 2023-09-14 045631](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/5732662a-0a41-4bc4-8200-3377d4c4a2e8)

**Enter an Item Name**
Click on **pipeline** 

![Screenshot 2023-09-14 045657](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/fcaae2e8-1afe-4614-8858-a0b7e3485b11)

In **configure** section enter Description
add **description** Django-Todo-App after that tick on **GitHub project**

![Screenshot 2023-09-14 045740](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/14a3a78c-406a-43c6-a5a0-8b2e14b00f8b)

### Pipeline

In **definition** section : Select **pipeline script from SCM**
**SCM -> Git**
**Repository URL** copy the repository url
Select **credentials** of docker hub

![Screenshot 2023-09-14 045907](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/e3c77b54-7dd8-4874-b811-b2ac3934cfa3)

In **ScriptPath** name of jenkinsfile then save it.

![Screenshot 2023-09-14 045923](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/e7aae987-49f4-43cf-9567-490971459071)

## jenkinsfile 

![Screenshot 2023-09-14 190836](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/2176db2f-1970-4ac9-b011-ded20563f5c3)



Click on **Build Now**
## Now you youcan see detail of stages 

![Screenshot 2023-09-14 054744](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/f54f1556-c35c-496d-a990-50147592a357)

### Now docker image has be build and pushed to Docker hub 

![Screenshot 2023-09-14 054842](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/be4921e0-1afa-4f95-9060-bb4428b6dbd1)

# Install minikube

## Create EC2 instance (t2.medium) instance.

### First you need to install Docker on your machine. Install Docker and run below command.

```
$sudo usermod -aG docker $USER
$sudo reboot
```

![Screenshot 2023-09-14 090531](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/e8084076-c739-4ec4-9d08-7cf6e2a21881)

```
$minikube start --driver=docker
```

Once minikube start finishes, run the command below to check the status of the cluster:
```
$minikube status
```

### Install kubectl
```
$sudo snap install kubectl --classic
$kubectl version
```

![Screenshot 2023-09-14 120218](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/aa0b564a-1c18-4ae7-8370-079bc90cdb57)

### Create YAML Manifest
```
$vi djanjo-app-deploy.yaml
$vi django-app-service.yaml
$vi django-app-ingress.yaml
```

![Screenshot 2023-09-14 121433](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/155aee48-e6be-462a-9289-a19589dc0294)

The below commands apply the configurations defined in the YAML files to your Kubernetes cluster.

```
$kubectl apply -f djanjo-app-deploy.yaml
$kubectl apply -f django-app-service.yaml
$kubectl apply -f django-app-ingress.yaml
```

![Screenshot 2023-09-14 121601](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/63218609-4b59-47e2-b845-6c1eb6d7e7e2)

The bellow command enable the Ingress addon in a Minikube Kubernetes cluster. This addon allows you to use Ingress resources to expose services and routes HTTP traffic into your Minikube cluster.

```
$minikube addons enable ingress
```

![Screenshot 2023-09-14 122037](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/a55dc990-16f1-4ad7-b8ff-9ca41317292d)

The command minikube addons list is used to list the available addons and their status in your Minikube Kubernetes cluster. This command provides information about which addons are currently enabled and which ones are disabled.

```
$minikube addons list
```

![Screenshot 2023-09-14 122122](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/9886e0f5-b64f-4500-baa9-ca43f186b620)

When you run these commands, you'll get output displaying the relevant information for each resource type.

```
$kubectl get ingress
$kubectl get deploy
$kubectl get svc
$kubectl get pods
```

![Screenshot 2023-09-14 122339](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/f2156893-140f-459a-ad62-e133d5b2e8c4)

## To expose application to the internet copy ec2_instance_IP:8000 

![Screenshot 2023-09-14 123817](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/8a632754-fec9-45fe-bd8f-ceb71f6a9719)

```
12.53.52.34:8000
```

![Screenshot 2023-09-14 123850](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/164ab14f-547e-40d0-8ddf-49e8b0e4563e)


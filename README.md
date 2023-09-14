# Django Todo App Deployment on Kubernetes 

## create ec2 instance (t2.micro), install Docker and Jenkins, add jenkins and USER to docker group.
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


Click on **Build Now**
## Now you youcan see detail of stages 

![Screenshot 2023-09-14 054744](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/f54f1556-c35c-496d-a990-50147592a357)

### Now docker image has be build and pushed to Docker hub 

![Screenshot 2023-09-14 054842](https://github.com/pradip2994/Project_k8_django_app/assets/124191442/be4921e0-1afa-4f95-9060-bb4428b6dbd1)



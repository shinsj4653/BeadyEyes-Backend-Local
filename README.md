# GDSC Solution Challenge - BeadyEyes

## Main Improvements
### 1. Adding Zero-Downtime Deployment
- Before


- After


## Backend repo

### How to run my code on local environment by using SpringBoot Framework
1. Use SpringBoot Framework and open the cloned repository  


![image](https://github.com/GDSC-Solution-Challenge-Team-4/BeadyEyes-Backend/assets/49470452/ccc97d74-6631-4892-90ea-d7167731e258)

2. Then, click the green start button on the right above area, or select the 'Run Pointer Application' option in the Run Menu.  


![image](https://github.com/GDSC-Solution-Challenge-Team-4/BeadyEyes-Backend/assets/49470452/c8a06217-5c7a-4d37-825a-e6b102817d17)

![image](https://github.com/GDSC-Solution-Challenge-Team-4/BeadyEyes-Backend/assets/49470452/23fd330c-2d12-4b78-9795-518fc58a48f7)


### How to run my code on vm instance console by using docker, docker-compose, and DockerHub

1. Make sure you have installed docker and DockerHub repository on your local area. Also you must have docker and docker-compose in your server area.  

2. Click the bootJar button to build the backend project.  
![image](https://github.com/GDSC-Solution-Challenge-Team-4/BeadyEyes-Backend/assets/49470452/c141d028-3163-4758-a22e-810b5f973ad4)


3. Create docker image of the project.
From the project that was build, make a docker image and push it to your own DockerHub repository.  
```bash
docker login -u ${{ secrets.DOCKERHUB_USERNAME }} -p ${{ secrets.DOCKERHUB_PASSWORD }}
docker buildx build --push --platform linux/amd64 -t ${{ secrets.DOCKERHUB_REPOSITORY }}:${GITHUB_SHA::7} .
```

4. Pull the docker image and use docker-compose to deploy.  
Inside the vm instance ssh console, use these process to deploy the image via docker-compose.  
Make sure to tag the correct image name, so that the docker-compose.yml file can detect it.  
Also, deploy.sh file with Nginx feature allows the project to be deployed with zero downtime.  
```bash
sudo docker login -u ${{ secrets.DOCKERHUB_USERNAME }} -p ${{ secrets.DOCKERHUB_PASSWORD }}
sudo docker pull ${{ secrets.DOCKERHUB_REPOSITORY }}:${GITHUB_SHA::7}
sudo docker tag ${{ secrets.DOCKERHUB_REPOSITORY }}:${GITHUB_SHA::7} beadyeyes-spring
sudo chmod 777 ./deploy.sh
./deploy.sh
sudo docker image prune -f
```

## Docker Compose Demo

1. Make Directory
   a. In a Command Console window make a director with the `md DockerDemo\ExampleCode\`.

   ### Console

   ```Console
       md DockerDemo\ExampleCode\
   ```

2. Change Directory with the command `cd DockerDemo|ExampleCode\`.

   ### Console

   ```Console
      cd DockerDemo\ExampleCode\
   ```

3. Clone code from git repo with command `git clone https://github.com/Azure-Samples/azure-voting-app-redis.git`.

   ### Console

   ```Console
       git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
   ```

4. Navigate to directory `cd c:\DockerDemo\ExampleCode\azure-voting-app-redis`.

   ### Console

   ```Console
       cd  c:\DockerDemo\ExampleCode\azure- voting-app-redis
   ```

5. Run docker compose to build images and run the container `docker-compose up –d`.

   ### Console

   ```Console 
       docker-compose up –d
   ```

   > Note: `-d` or `--detach` run containers detached mode which run container in the background.

   5a. To see the running application, enter `http://localhost:8080` in a local web browser.

6. List local images `docker images`.

   ### Console

   ```Console
       docker images
   ```

7. Show running Containers Open another command prompt `docker ps -l`

   ### Console

   ```Console
       docker ps -l
   ```

8. Stop container running `docker-compose down`

   ### Console

   ```Console
       docker-compose down
   ```

### [Docker Compose Tutorial](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app)

# Docker Registry Demo

1. Create Resource Group.

   ### Console

   ```Shell
          az group create  --name   dockerdemoregistry-rg     --location eastus

   ```

2. Create ACR.

   ### Console

   ```Shell
          az acr create    --resource-group   dockerdemoregistry-rg     --name  dockerdemoacr01 --sku    Basic

   ```

3. Login To ACR.

   ### Console

   ```Shell
          az acr login --name  dockerdemoacr01

   ```

4. Tag Image local copy.

   ### Console

   ```Shell

          docker tag mcr.  microsoft.com/    azuredocs/  azure-vote-front:v1   dockerdemoacr01.  azurecr.io/   azure-vote-front:v1    (change v1 to v2)

   ```

5. Find ACR to push Image to.

   5a.Get list of ACR login servers.

   ### Console

   ```Shell

          az acr list --resource-group dockerdemoregistry-rg --query "[].{acrLoginServer:loginServer}" --output table

   ```

   ### Output

   ```Shell

          dockerdemoacr01. azurecr.io

   ```

   5b. Get list of images local.

   ### Console

   ```Shell

          docker images

   ```

   ### Output

   ```Shell

          REPOSITORY                                           TAG                  IMAGE ID             CREATED              SIZE
   mcr.microsoft.com/azuredocs/    azure-vote-front        v1                      84b41c268ad9        16  minutes ago      944MB
   mycontainerregistry.azurecr.    io/azure-vote-front     v1                      84b41c268ad9        16  minutes ago      944MB
   mcr.microsoft.com/oss/  bitnami/redis             6.  0.8                   3a54a920bb6c        2 days  ago          103MB
   tiangolo/   uwsgi-nginx-flask                        python3.    6               a16ce562e863        6 weeks     ago         944MB

   ```

6. Push Image to ACR.

   ### Console

   ```Shell

          docker push  dockerdemoacr01. azurecr.io/  azure-vote-front:v1

   ```

7. List images in ACR.

   ### Console

   ```Shell
   
          az acr repository list --name dockerdemoacr01 --output table
   ```

8. List image tags.

   ### Console

   ```Shell

          az acr repository    show-tags --name   dockerdemoacr01   --repository  azure-vote-front     --output table
   ```

   ### [ACR Tutorial](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app)

# Docker Build Demo

1.  Navigate the app folder
    `cd samples/aspnetapp/aspnetapp`.
    .

    ### Console

    ```Shell
           cd samples/aspnetapp/aspnetapp


    ```

2.  Run app local.

    ### Console

    ```Shell

           dotnet run

    ```

3.  Navigate to Web page
    `https://localhost:5001/`

        ### Browser

    ```Shell

           https://localhost:5001/

    ```

4.  Change directory `C:\DockerDemo\ExampleCode\dotnet-docker\samples\aspnetapp\aspnetapp> cd..`.

    ### Console

    ```Shell

          C:\DockerDemo\ExampleCode\dotnet-docker\samples\aspnetapp\aspnetapp> cd..
    ```

5.  Build image.

    ### Console

    ```Shell

           docker build -t aspnetapp .

    ```

6.  Run container.

    ### Console

    ```Shell

           docker run -it --rm -p 5000:80 --name aspnetcore_sample aspnetapp

    ```

    > Note:--rm Automatically remove the container when it exits

7.  View app in the browser.

    ### Browser

    ```Shell


     http://localhost:5000


    ```

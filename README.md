# basic-docker-webapp
Testing container applications on dotnet6 web application and publishing on docker hub

## Installation

https://docs.docker.com/desktop/windows/install/

## Commands

- docker --help
- docker build --help
- docker build . # create docker image
- docker run --name test 75957569658569 # create docker container
- docker rm test # delete container test
- docker images
- docker run -d -p 55002:80 --env "COMPANY_NAME=Osemeke" --name myappcontname myappimage
- docker run -d -p 55003:80 -p 55004:443 --env "COMPANY_NAME=ANYIRAH" --name myappcontainername myapp2
- docker image rm 4s567d
- docker tag local-image:tagname new-repo:tagname
- docker push new-repo:tagname
- docker tag firstimage YOUR_DOCKERHUB_NAME/firstimage
- docker push YOUR_DOCKERHUB_NAME/firstimage

## Image Configuration (enviromental variables)

> dotnet will load all configuration settings like appsettings.json and properties/lounchsettings.json into the DI container. Any of the keys can be overridden in the Dockerfile to enable config at running a container like `-e "APP_NAME=XYZ Cooperative"`

As seen below;
```cs
var configuration = new ConfigurationBuilder()
  .AddJsonFile("appsettings.json")
  .AddJsonFile($"appsettings.{env.EnvironmentName}.json")
  .AddEnvironmentVariables()
  .Build();
```

### See links:
1. https://www.scottbrady91.com/docker/aspnet-core-and-docker-environment-variables
1. https://blog.matjanowski.pl/2017/11/18/managing-options-and-secrets-in-net-core-and-docker/
1. https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-6.0
1. https://stackoverflow.com/questions/68506243/read-docker-compose-environment-variable-from-asp-net-core-controller


## Docker Compose

> Use to store docker run commands and parameters for one or multiple related (solution) image(s). Suitable for running microservice ecosystem.

## Tips
    1. Visual studio projects build command from solution folder:
    docker build -f .\WebApp\Dockerfile -t myapp1 .
    # -f docker file path, -t image name, . 
    # https://stackoverflow.com/questions/66933949/failed-to-compute-cache-key-csproj-not-found

    2. HTTPS configuration
    dotnet dev-certs https -ep %USERPROFILE%\.aspnet\https\aspnetapp.pfx -p mycertpassword
    dotnet dev-certs https --trust
    docker run --rm -it -p 8000:80 -p 8001:443 -e ASPNETCORE_URLS="https://+;http://+" -e ASPNETCORE_HTTPS_PORT=8001 -e ASPNETCORE_Kestrel__Certificates__Default__Password="password" -e ASPNETCORE_Kestrel__Certificates__Default__Path=/https/aspnetapp.pfx -v %USERPROFILE%\.aspnet\https:/https/ mcr.microsoft.com/dotnet/core/samples:aspnetapp

    3. Volumes can be used to persist database data or appsettings configuration files

## Docker Hub Account

https://hub.docker.com -- osemeke1/lowUP@4


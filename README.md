
# Create Docker image with Nginx & PHP7 over Alpine Linux
## 1a. Cloning data from GitHub and modify config files
```
$ git clone 
$ cd docker-nginxphp
$ nano <configfile>
```
## 1a. Create the working directory and the configuration files

```
$ mkdir docker-nginxphp && cd docker-nginxphp
$ mkdir config scr
$ nano Dockerfile
$ nano <allfiles>
```
## 2. Create a docker image

``` 
$ docker build --rm -t docker-nginxphp .
```

The image docker-nginxphp:latest has been created with a size of 106MB

## 3. Run Nginx & PHP7 in a container ...
  ### 3a. ... with data & files in Docker area filesystem

  ```
  $ docker run -d --name nginx --net=host -v /var/www/html:/var/www/html docker-nginxphp:latest
  ```
  
  ### 3b. ... with data & files in server filesystem

  ```
  $ docker run -d --name nginx --net=host docker-nginxphp:latest
  ```

  ### 3c. ... with data & files in a Docker volume

  ```
  $ docker run -d --name nginx --net=host --mount source=nginx-html,target=/var/www/html docker-nginxphp:latest
  ```

## 4. Run Nginx & PHP7 in a container and start automatically


$ docker run -d --restart always --name nginx --net=host -v /var/media:/media docker-nginxphp:latest


## Configuration of Web Directory
The configuration file of the program that is fixed when compiling the image in ./config directory

The port of service has been fixed at 80

The internal data directory is set to "/var/www/html"

## Creation and use of Docker volume
To create and view existents volumes:
 ```
  $ docker volume create nginx-html
  $ docker volume ls
  $ docker volume inspect nginx-html
  ```

To add data to Docker volume copy files at directori indicated on ```$ docker volume inspect```
 ```
  $ sudo cp src/ /var/lib/docker/volumes/nginx-html/_data/
  ```





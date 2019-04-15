# sass-docker-builder

[![dockeri.co](https://dockeri.co/image/acegrc/sass)](https://hub.docker.com/r/acegrc/sass)

[![GitHub issues](https://img.shields.io/github/issues/acegrc/sass-docker-builder.svg "GitHub issues")](https://github.com/acegrc/sass-docker-builder/issues)
[![GitHub stars](https://img.shields.io/github/stars/acegrc/sass-docker-builder.svg "GitHub stars")](https://github.com/acegrc/sass-docker-builder)

[![Docker build](https://img.shields.io/docker/cloud/build/acegrc/sass.svg)]((https://hub.docker.com/r/acegrc/sass))
[![Docker Pulls](https://img.shields.io/docker/pulls/acegrc/sass.svg)]((https://hub.docker.com/r/acegrc/sass))

# What is this image about?
This image is based on <a href="https://hub.docker.com/_/node">node:alpine</a> docker image with extra package installed the <a href="https://www.npmjs.com/package/sass">sass package</a>.

# How to use this image

## Windows OS
You can run the Docker image with the `docker run` command.

Windows cmd:
```command
C:\Projects\MyProject> docker run -d --rm -v %cd%:/src --entrypoint sass acegrc/sass /src:/src --watch --poll
```

The correct syntax is: `docker run [DOCKER OPTIONS] --entrypoint PROGRAM IMAGE [PROGRAM ARGS]`

Keep in mind that our entry program is `sass` and runs as: `sass input_dir:output_dir --watch --poll`.
To comply with the `docker run` command we need to split the program arguments from the program as mentioned above.

The command `-v %cd%:/src` maps our current directory to the `/src` directory in the container.

## Linux OS
You can run the Docker image with the `docker run` command.

Linux console command:
```
$ docker run -d --rm -v $PWD:/src --entrypoint sass acegrc/sass /src:/src --watch --poll
```

The correct syntax is: `docker run [DOCKER OPTIONS] --entrypoint PROGRAM IMAGE [PROGRAM ARGS]`

Keep in mind that our entry program is `sass` and runs as: `sass input_dir:output_dir --watch --poll`.
To comply with the `docker run` command we need to split the program arguments from the program as mentioned above.

The command `-v $PWD/src` maps our current directory to the /src directory in the container.

## docker-compose

You can run the Docker image with the `docker-compose` command.

Create a `docker-compose.yml` in your app project:
```yaml
version: '3.6'
services:
  sass:
    image: acegrc/sass
    entrypoint:
      - sass
      #- /src     # uncomment this and comment below when the input_directory is same as the output directory
      - /src:/src # input_directory:output_directory
      - --watch
      - --poll
    volumes:
      - ./:/src
```

You can then build and run the Docker image with the `docker-compose` command:

```bash
$ docker-compose build
$ docker-compose up -d
```

## Compiling css with different input and output directory

Lets assume that our project has the following directory structure:
```text
MyProject
    |---src
    |   `-css
    `-css
```

And we want to build everything in the `MyProject/src/css` directory with output to `MyProject/css` directory.

Since we run the `sass` inside the container we need to specify the input and the output directory path as they exist inside the container.

Consider the following table to find out the mapped paths and create yours:

 Project Directory | Mapped Path 
-------------------|--------------
 MyProject         | /src 
 MyProject/src     | /src/src 
 MyProject/src/css | /src/src/css 

### Windows OS

Windows cmd:
```command
C:\Projects\MyProject> docker run -d --rm -v %cd%:/src --entrypoint sass acegrc/sass /src/src/css:/src/css --watch --poll
```

The command `-v %cd%:/src` maps our current directory to the `/src` directory in the container.


## Linux OS
You can run the Docker image with the `docker run` command.

Linux console command:
```
$ docker run -d --rm -v $PWD:/src --entrypoint sass acegrc/sass /src:/src --watch --poll
```

The command `-v $PWD/src` maps our current directory to the /src directory in the container.
 
 ## docker-compose
 
Create a `docker-compose.yml` in your app project:
```yaml
version: '3.6'
services:
sass:
 image: acegrc/sass
 entrypoint:
   - sass
   #- /src      # uncomment this and comment below when the input_directory is same as the output directory
   - /src/src/css:/src/css # input_directory:output_directory
   - --watch
   - --poll
 volumes:
   - ./:/src
```

You can then build and run the Docker image with the `docker-compose` command:

```bash
$ docker-compose build
$ docker-compose up -d
```

## Copyright

Copyright (c) 2019 Haris Sofos. See [LICENSE](https://github.com/acegrc/sass-docker-builder/blob/master/LICENSE) for details.


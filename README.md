`adzerk/boot-clj` is a public Docker image that installs and sets up Oracle Java 8 and the latest version of Boot.

This repo is set up as an [automated build](https://docs.docker.com/docker-hub/builds) on Docker Hub. The `adzerk/boot-clj` Docker image is automatically built from the Dockerfile in this repo and deployed to Docker Hub.

To use as a base image for another Dockerfile, put this at the top of the Dockerfile:

    FROM adzerk/boot-clj

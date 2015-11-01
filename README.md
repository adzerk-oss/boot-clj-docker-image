# boot-clj-docker-image

`adzerk/boot-clj` is a public Docker image that installs and sets up Oracle
Java 8 and the latest version of [Boot][boot].

This repo is set up as an [automated build][docker] on Docker Hub. The
`adzerk/boot-clj` Docker image is automatically built from the _Dockerfile_
in this repo and deployed to Docker Hub.

## Try It

```
$ docker run -it adzerk/boot-clj repl
```

## Extend It

To use as a base image for another _Dockerfile_, put this at the top of your
_Dockerfile_: 

    FROM adzerk/boot-clj:latest

## Cache Maven Artifacts At Build Time

The image is constructed to cache Maven artifacts in _/m2_, and Boot JAR
files in _/.boot_ in the container. You can cache these things at build
time in your container by adding commands similar to the following to
your _Dockerfile_:

    RUN boot <yourtask>

Assuming that _yourtask_ doesn't block the Boot pipeline it will exit, but
not before downloading all of its dependencies into the Maven repository
in the container. This way it won't need to download them at runtime.

## Setting The Version Of Boot / Clojure

You can use any version of Boot with this image by specifying the
`BOOT_VERSION`. You can do this in a couple of ways:

- You can make a _boot.properties_ file in your project that specifies the
  version of Boot and/or Clojure to use,
- or you can set the `BOOT_VERSION` and/or `BOOT_CLOJURE_VERSION` environment
  variables in your _Dockerfile_.

_boot.properties_

    BOOT_VERSION=2.3.0
    BOOT_CLOJURE_VERSION=1.6.0

_Dockerfile_

    ENV BOOT_VERSION=2.3.0
    ENV BOOT_CLOJURE_VERSION=1.6.0

Environment variables set in the _Dockerfile_ will override settings in the
_boot.properties_ file.

[boot]:   https://github.com/boot-clj/boot
[docker]: https://docs.docker.com/docker-hub/builds

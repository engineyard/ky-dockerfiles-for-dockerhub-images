# Dockerfiles for the Docker Hub images
This repository has the Dockerfiles used for the Docker images uploaded on Docker Hub for Engine Yard Kontainers here: https://hub.docker.com/r/engineyard/kontainers.

## Structure
The Dockerfiles are the only resource needed in order to build and upload the images to Docker Hub. In order to keep track of the current and future images, the directories are structured as follows:

```
ruby/
└── ruby_version
    └── base_OS
        └── OS_distro
```

The above structure means that we can have images for `ruby`, `nodejs`, `php` etc and various linux distros e.g. `Alpine`, `Ubuntu`, `Debian` etc.

## Parent image
We have selected as `parent image` the  Debian's `buster` or `stretch` version that offer LTS support that covers our needs until June 2022 ([source](https://en.wikipedia.org/wiki/Debian_version_history))
## Versioning 
The images that are uploaded to Docker Hub follow the Semantic Versioning.

## Process
The steps followed are:

1. create a new Dockerfile e.g. `ruby/2.5.8/debian/slim-buster/Dockerfile.ruby_2.5.8_debian_slim_buster`
2. build the image locally: `docker build --file ./ruby/2.5.8/debian/slim-buster/Dockerfile.ruby_2.5.8_debian_slim_buster --tag=ruby_2.5.8_debian_slim_buster .`
3. test the image: `docker run --rm -ti ruby_2.5.8_debian_slim_buster /bin/bash`
4. create an image tag to upload: `docker build --no-cache --file ./ruby/2.5.8/slim-buster/Dockerfile.ruby_2.5.8_debian_slim_buster -t engineyard/kontainers:ruby-2.5-v1.0.0 .`
5. push the image to Docker Hub: `docker push engineyard/kontainers:ruby-2.5-v1.0.0`
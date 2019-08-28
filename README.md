# git_commands
useful git commands

## Keep a file in git but don't track changes

git has a different solution to do this. First change the file you do not want to be tracked and use the following command:

```git update-index --assume-unchanged FILE_NAME```

and if you want to track the changes again use this command:

```git update-index --no-assume-unchanged FILE_NAME```

ref: https://stackoverflow.com/questions/9794931/keep-file-in-a-git-repo-but-dont-track-changes


## Keep directories in git but don't track changes

The above method to keep files but not track changes do not work on directories that contain subdirectories. For example if the folder stucture is as follows, and all the files including the ones in subdirectories are to be excluded from tracking

```
 root   
 |-DIR1   
 |  |-File1   
 |  |-File2   
 |-DIR2   
 |  |-File3   
 |  |-File4   
 |-File5   
 .
 .
 .
 |-File_n
 ```
 
 update-index is an internal plumbing command and thus not as comfortable as the real front-end commands. You will have to handle the recursion bit yourself:

```git ls-files -z myFolderToIgnore/ | xargs -0 git update-index --assume-unchanged```

ref: https://stackoverflow.com/questions/16346535/recursive-git-update-index-assume-unchanged

## Remove a directory from being tracking
Add the directory to the .gitignore
`path_to/the_directory_to_ignore/`

run
`git rm -r --cached path_to/the_directory_to_ignore/`

# Docker commands

## list images
`docker image ls`

## Add a new tag to an image
`docker image tag <image-id> <new-name:[tag]>`

## list containers
`docker container ls`
or
`docker ps`

`--all` flag can be used to list all containers

## Build image
`docker build --tag=name:tag .`

## Deploy a container from image
`docker run name:tag`

## bash in to a container if it's linux
`docker run -it --name="name_for_container" image_name:tag /bin/bash`

## restart a container
`docker restart container_name`

## Run a stopped container with the same command
`docker start -ai <container_name>`

## Run a stopped container with a differnt command (for example start an interactive terminal)
`docker start <container_name>`

`docker exec -it <container_name> /bin/bash`

## Save a docker image
`docker save -o <path for generated tar file> <image name>`

## Load an image from file
`docker load -i <path to image tar file>`

## Remove all docker containers (ref: https://coderwall.com/p/ewk0mq/stop-remove-all-docker-containers)
```bash
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```

# <span style="color:green">gcloud SDK</span>
## Install gcloud sdk (linux)
1. Follow the instructions in https://cloud.google.com/sdk/docs/downloads-apt-get
2. If the above instructions don't work
 - Follow this link https://github.com/GoogleContainerTools/base-images-docker/issues/50
 - Execute the following,
 ```bash
 echo "deb http://packages.cloud.google.com/apt cloud-sdk-stretch main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get update -y && apt-get install google-cloud-sdk -y
 ```

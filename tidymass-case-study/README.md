# Create a repo for docker image

1. Sign in or sign up in [`Docker Hub`](https://hub.docker.com/).

2. Click the Create Repository button. 

3. For the repo name, use the name same with your building, here is `tidymass-case-study`. Make sure the Visibility is `Public`.

4. Click the `Create` button!

# Creat a image

1. In on folder, create a file named as `Dockerfile` without any extension.

2. This is a shell like script.

3. Write code in it.

# Build docker image

Open the terminal, and run the code below to build image.

```
docker build -t tidymass-case-study -f tidymass-case-study/Dockerfile .
```

`-t`: tag name, here is `tidymass-case-study`

`-f`: `Dockerfile` path. Here I put it in the sub folder named `tidymass-case-study`.

Then check it in local.

```
docker run -e PASSWORD=tidymass -p 8787:8787 tidymass-case-study
```

Open this in browser: http://localhost:8787

# Push the image.

1. First, let check if there is a image named as `tidymass-case-study` has been created.

```
docker image ls
```

2. In the terminal, log in the `Docker Hub` using the command docker.

```
docker login -u jaspershen
```

3. Then input your password.

4. Use the `docker tag` command to give the `tidymass-case-study` image a new name. 

```
docker tag tidymass-case-study jaspershen/tidymass-case-study:latest
```

5. Now try your push command.

```
docker push jaspershen/tidymass-case-study:latest
```

`:tag` here can be the version of the image. We set it as `:latest`.

# Reference:

1. https://aboland.ie/Docker.html

2. https://github.com/yufree/xcmsrocker

3. https://docs.docker.com/get-started/04_sharing_app/

4. https://stackoverflow.com/questions/51500385/how-to-speed-up-r-packages-installation-in-docker

5. https://www.techrepublic.com/article/how-to-build-a-docker-image-and-upload-it-to-docker-hub/

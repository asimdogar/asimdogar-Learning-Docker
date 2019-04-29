Build the app

We are ready to build the app. Make sure you are still at the top level of your new directory. Here’s what ls should show:

$ ls
Dockerfile		app.py			requirements.txt

Now run the build command. This creates a Docker image, which we’re going to name using the --tag option. Use -t if you want to use the shorter option.

docker build --tag=friendlyhello .

Where is your built image? It’s in your machine’s local Docker image registry:

$ docker image ls

REPOSITORY            TAG                 IMAGE ID
friendlyhello         latest              326387cea398


Run the app, mapping your machine’s port 4000 to the container’s published port 80 using -p:

$ docker run -p 4000:80 friendlyhello

Tag the image

$ docker tag friendlyhello gordon/get-started:part2

$ docker push username/repository:tag

$ docker run -p 4000:80 username/repository:tag





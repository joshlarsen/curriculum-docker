# Lesson 2: Building a docker image

To get the benefits of Docker for your own project, you'll need to "Dockerize" that project.

For most small code bases, this is pretty simple. You write a file that defines all the dependancies that your code needs to run, and then you use `docker build` to build an image that you can run from any computer. 

The food truck app you worked with in the last lesson was already dockerized. Below, we're going to take you through the steps fo dockerizing yourself from scratch.

In this lesson, we're going to be referencing the Docker docs a lot. The Docs are a great place to learn from, and include a lot of in-depth information on the way Docker works. We want to teach you not just about Docker, but also how to get information about Docker yourself in the future. 

## How Docker Works

The `Dockerfile` is a plaintext file that defines a Docker image, which once built can then be run in a Docker conatiner on any computer.

So to Dockerize an app, first you have to write the dockerfile for that app. The dockerfile contains all the information that Docker needs to know to run the app: where the code is contained on your local computer, what OS it runs on, what dependancies it has, and what commands should be run at start-up.

Once you write the `Dockerfile`, you run `docker build` on that file, and the Docker daemon takes the information from the `Dockerfile` and creates an image from it. This Docker image is a binary file containing the OS and program data that can be transfered to any computer, and run on that computer using Docker inside a container.

It's easy to confuse images and containers, because an image always runs in one container, and one container can only run a single image. Think of the image as the data necessary to run a container.


## Writing the `Dockerfile`

A Dockerfile is a plaintext file named simply `Dockerfile`—there's no extension. 

Inside the file is a series of comments and commands, in this format:

    # comment
    COMMAND arguments

While the file is not case-sensative, it's recommended to write all commands in ALL CAPS to make the file easier to read.

The commands are interpreted by the Docker Daemon when you call `docker build`, and are executed in order to set up the Image.

### The `FROM` Command

The Dockerfile must start with the `FROM` command. Images are created in layers, which means you can use an Image as the base image for your own. The `FROM` command defines what your base layer will be. As arguments, it takes the name of the image. This name can be extended with the Docker Hub Username of the maintainer of the image, and the version of the image, in the format `username/imagename:version`. For instance:

    FROM python:3.5

This command will build an image from the 3.5 version of the official Python image.

    FROM prakhar1989/catnip

This command takes the most recent version of the Image `catnip` from the user `prakhar1989`.


### The `RUN` Command

Perhaps the most common command is the `RUN` command. `RUN` is used to build up the Image you're creating. For each `RUN` command, Docker will run the command then create a new layer of the image. This way you can roll back your image to previous states easily.

The `RUN` command is largely used to install necessary components onto your new Image. So you'll see a lot of `apt-get` commands.

The syntax for a `RUN` instruction is to place the full text of the shell command after the `RUN`:

    RUN apt-get install -y curl

    RUN mkdir /user/local/foo

This will create an Image with curl installed, then use that Image to create an image and create a new image from it with a /user/local/foo folder.

This will automatically run in the `/bin/sh` shell. If you'd like to define a different shell, then the syntax is:

    RUN /bin/bash -c 'mkdir /user/local/foo'


### `LABEL`

`LABEL` is used to add labels to your Image. These labels will be used on Docker Hub and other applications. For instance, the following will set the version number of this particular container:

    LABEL version=1.0


### `EXPOSE`

The `EXPOSE` command opens ports in your Image so that it can speak to the outside world. The following tells the Image to listen at port 4000:

    `EXPOSE 4000`


### `CMD`

The final really important command is `CMD`. 

`CMD` defines the commands that will run on the Image at start-up. Unlike a `RUN`, this does not create a new layer for the Image, but simply runs the command.

There can only be one `CMD` per a Dockerfile/Image. If you need to run multiple commands, the best way to do that is to have the `CMD` run a script.

`CMD` requires that you tell it where to run the command, unlike `RUN`. So example `CMD` commands would be:

    CMD ["python", "./app.py"]

    CMD ["/bin/bash", "echo", "Hello World"]



# Project 2: Build a Dockerfile for an existing code base

## Walk thru Demo App Architecture
- Add Architectural Diagram with each components
- Examine code FoodTrucks/flask-app/app.py

## Checkout undockerized git branch to start your `FoodTruck` project

* From your terminal window, Use the command line to navigate to the Foodtrucks working directory.

`$ cd ~/sit/Foodtrucks`

* Checkout the GitHub branch called undockerised.

` $ git checkout undockerized `

## Dockerize Web-app

- First, create a `Dockerfile` with your choice of editor, for example:

` vi Dockerfile `

- Add the following items on Dockerfile, instructions for writing docker files, replace your anme and your email for `MAINTAINER`


```

FROM ubuntu:14.04

MAINTAINER Your Name <your email address>

RUN apt-get -yqq update

RUN apt-get -yqq install python-pip python-dev

RUN apt-get -yqq install nodejs npm

RUN ln -s /usr/bin/nodejs /usr/bin/node


ADD flask-app /opt/flask-app

WORKDIR /opt/flask-app

RUN npm install

RUN npm run build

RUN pip install -r requirements.txt

EXPOSE 5000

CMD [ "python", "./app.py" ]

```

- Build the docker image for `foodtrucks-web` from the current directory. It will take few minutes for the firs time.

` $ docker build -t foodtrucks-web . ` 

- Check that new docker images are created

` $ docker images `

## Set-up Web app container manually in command line. Learn commands needed to get it up and running correctly—database container, networking, etc.


- create docker network `foodtrucks`

` $ docker network create foodtrucks ` 

- start the ES container 

` $ docker run -d --net foodtrucks -p 9200:9200 -p 9300:9300 --name es elasticsearch `

- start the flask app container 

` $ docker run -d --net foodtrucks -p 5000:5000 --name foodtrucks-web prakhar1989/foodtrucks-web `

- Verify that two docker containers are started and running 

`$ docker ps -a`

- You should see 2 containers running, elasticsearch and foodtruck-web.

## Start a browser on your laptop and navigate to [http://localhost:5000](http://localhost:5000) to perform search.

-  In your browser, go to `localhost:5000`

-  Verify the Foodtruck applicaiton is running correctly, by performing a search for "Tacos" or "Burges" etc, and find location of Foodtrucks. 

-  Navigate maps by scrolling up and down, zooming in and out, and mouse over to a particluar location for more detail informations.



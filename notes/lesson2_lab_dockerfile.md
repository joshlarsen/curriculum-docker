# Lesson 2: Building a docker image

To get the benefits of Docker for your own project, you'll need to "Dockerize" that project.

For most small code bases, this is pretty simple. You write a file that defines all the dependancies that your code needs to run, and then you use `docker build` to build an image that you can run from any computer. 

The food truck app you worked with in the last lesson was already dockerized. Below, we're going to take you through the steps fo dockerizing yourself from scratch.

In this lesson, we're going to be referencing the Docker docs a lot. The Docs are a great place to learn from, and include a lot of in-depth information on the way Docker works. We want to teach you not just about Docker, but also how to get information about Docker yourself in the future. 

## dockerfile

The dockerfile is a plaintext file that defines 


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



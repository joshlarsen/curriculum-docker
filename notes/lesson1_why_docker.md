# Lesson 1 : Intro to Docker

Docker is a tool that lets you easily run code on any machine you'd like. While building and running a new in-development program often takes a large amount of set-up and managing dependencies, Docker makes this process relatively trivial once an app has been set up to work with Docker, or "dockerized".

In this course, we'll teach you how to set up and use Docker to speed up the most common developer workflow.


## What is Docker?

Docker is a suite of products that all focus on running applications on any server or computer architecture. This means that once you get your application running using Docker, you can port it to any other computer with Docker installed by simply running a few commands.

Docker Engine is the product that most people refer to when they discuss "docker". Engine is the underlying technology behind all Docker products which builds images and runs them in containers. However, Engine on its own doesn't get you much.

When Engine is combined with other Docker tools such as Compose and Swarm, it can help you solve more common software development problems. Docker for Mac and Windows bundles Engine with these and other tools in an easy to install package.

In addition to local tools, Docker also has public and private cloud products which make managing images and deploying to production easy.


## Why Docker?

There are several common problems that Docker solves. The first and most common is normalizing development environments so that code that works on one machine works on all of them. This is the first forray into Docker for most firms and individuals. Each developer has Docker on their computer, and every time they push code to GitHub (or the version control solution of their choice), a new image is created that anyone can test and change. This also makes it very easy to get new developers onboarded: all they have to do is run a single docker command, and the code is guaranteed to be running on their machine.

A variant on this workflow is used at **Keybase**. Keybase is cryptography software that requires a lot of low-level code to be written. Compiling and building this code requires a number of specific Linux dependencies. Rather than have every developer manage these dependencies, there is a "build image". When testing new code, the developers build the project in that image, and then save it to their local machine. They can then run the application locally, or release it to the public. 

Docker can also speed up your production process. Tools like Docker Cloud and Swarm make managing images across your cloud infrastructure easy. **Major League Soccer** runs their production infrastructure on Docker. When they have a new build, they push out the new Docker image to their cloud host, and it automatically takes over from the old one. In addition to being easy to test code to know that it will work in production, when bugs do get through all the Ops people have to do is revert the image to the last working version in production while they fix the bug in the code.

These and many more workflows are made possible by using Docker. In this course, we'll be focusing on the first one: how to use Docker Engine and Docker Compose to standardize your dev environment and get it up and running on any machine in just a few minutes. On the next page, we'll walk you through getting a pre-built dev environment running on your computer, then in the next few lessons we'll teach you how to "dockerize" your own projects.

---

# Project 1: Using Docker to Set Up a Development Environment Locally

Let's look at how you might use Docker to speed up your developer workflow. We've set up a project so that you can see how easy Docker makes set-up for someone new to your code base, which we'll use in the tutorial below.

Pretend its your first day on a new job, and your boss wants you to write and test some new code. Without Docker, you'd have to get an environment up and running that runs your code, often following a long set of instructions on downloading the right linux distro and adding the right versions of the right packages to it.

With Docker, you can do all of this on your local machine by running a single command, `docker-compose up -d`. When run in the directory that your code lives in, it will run the docker image associated with that code, and any others that are needed to get it up and running. 

The first time you do this, downloading the images might take a few minutes, but after that you can have your code up and running in seconds. 

One of the nice things about this workflow is that your code can still live on your local machine, even while it's run in the docker container. That way, you can edit the code locally using whatever set-up you like the most (this course was written in Sublime Text 3, for instance), and it will auto-update in the container when you save it.

Run through the steps below on the learning container you set up earlier to see how this works in action.

* From your terminal window, create and go to your project directory under your home directory.

`$ mkdir ~/sit`

`$ cd ~/sit`

* Clone the GitHub Repo (or download and extract the code) [here](link/for/the/future).

`$ git clone https://github.com/wheelhouseio/Foodtrucks`

* Use the command line to navigate to the Foodtrucks working directory.

`$ cd Foodtrucks`

* Run your Foodtrucks applicaiton in detached mode. (First time running this, it may take some time to download container images.
)

`$ docker-compose up -d`

* HINT: starts the containers in the background and leaves them running. 

`
Options:
    -d                         Detached mode: Run containers in the background,
                               print new container names.
                               Incompatible with --abort-on-container-exit.

`

* Verify that two docker containers are started and running 

`$ docker ps -a`

* You should see 2 containers running, elasticsearch and foodtruck-web.

## Start a browser on your laptop and navigate to [http://localhost:5000](http://localhost:5000) to perform search.
*  In your browser, go to `localhost:5000`
*  Verify the Foodtruck applicaiton is running correctly, by performing a search for "Tacos" or "Burges" etc, and find location of Foodtrucks. 
*  Navigate maps by scrolling up and down, zooming in and out, and mouse over to a particluar location for more detail informations.


## Edit code in your local machine(or training container), see it instantly changed on foodtruck-web container by sharing user volume

* Now, let's change color of the banner to purple color instead of yellow. 
* From your laptop terminal window (or Learning container depending on how you set up), go to the Foodtruck project directory. 
* Change CSS in flask-app/static/styles/main.css file. For example, change heading color from to `#ac39fd`

```
html, body { padding: 0; color: #ac39fd; box-sizing: border-box; font-family: 'Titillium Web', sans-serif; margin: 0;) }
```

* Verify the changes you have made are reflected on Foodtruck application, by refresh your browser to [http://localhost:5000](http://localhost:5000)
* The change should show up instantly. 


## Verify sharing of volume between applicaiton container and your local machine (or training container).

* Goto foodtrucks-web container `docker exec -i -t <container ID for foodtrucks-web>`
* Check the volume is created `docker volume ls`
* Check the network is created `docker network ls`
* Verify volume /opt is mounted in foodtrucks-web container same volume as from training container as a local directory by
inspecting docker container `docker inspect <container ID for foodtrucks-web>`


## Cleanup 

* Run `docker compose down` and go back to [http://localhost:5000](http://localhost:5000). Check that he application is no longer running. 
* Check `docker ps`. The containers should be stopped.





---
Old version:

* Clone the GitHub Repo (or download and extract the code) [here](link/for/the/future).
* Use the command line to navigate to the repo.
* Run `docker compose up` in the base directory.
* When it's done running, go to `localhost` in your browser—it should show you the app!
* Now go back to the repository, and change `file_x.code`.
* Refresh `localhost`—the changes should show up instantly.
* Run `docker compose down` and go back to `localhost`. The app isn't running. 
* Check `docker ps`. The images should all be run down.

---
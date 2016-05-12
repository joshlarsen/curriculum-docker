# Lesson : Intro to Docker

Docker is a tool that lets you easily run code on any machine you'd like. While building and running a new in-development program often takes a large amount of set-up and managing dependencies, Docker makes this process relatively trivial once an app has been set up to work with Docker, or "dockerized".

In this course, we'll teach you how to set up and use Docker to speed up several common workflows.


## What is Docker?

Docker is a suite of products that all focus on running applications on any server or computer architecture. This means that once you get your application running using Docker, you can port it to any other computer with Docker installed by simply running a few commands.

Docker Engine is the product that most people refer to when they discuss "docker". Engine is the underlying technology behind all Docker products which builds images and runs them in containers. However, Engine on its own doesn't get you much.

When Engine is combined with other Docker tools such as Compose and Swarm, it can help you solve more common software development problems. Docker for Mac and Windows bundles Engine with these and other tools in an easy to install package.

In addition to local tools, Docker also has public and private cloud products which make managing images and deploying to production easy.


## Why Docker?

There are several common problems that Docker solves. The first and most common is normalizing development environments so that code that works on one machine works on all of them. This is the first forray into Docker for most firms and individuals. Each developer has Docker on their computer, and every time they push code to GitHub (or the version control solution of their choice), a new image is created that anyone can test and change. This also makes it very easy to get new developers onboarded: all they have to do is run a single docker command, and the code is guaranteed to be running on their machine.

A variant on this workflow is used at **Keybase**. Keybase is cryptography software that requires a lot of low-level code to be written. Compiling and building this code requires a number of specific Linux dependencies. Rather than have every developer manage these dependencies, there is a "build image". When testing new code, the developers build the project in that image on their local machine. They can then run the application locally, or release it to the public. 

Docker can also speed up your production process. Tools like Docker Cloud and Swarm make managing images across your cloud infrastructure easy. **Major League Soccer** runs their production infrastructure on Docker. When they have a new build, they push out the new Docker image to their cloud host, and it automatically takes over from the old one. In addition to being easy to test code to know that it will work in production, when bugs do get through all the Ops people have to do is revert the image to the last working version in production while they fix the bug in the code.

These and many more workflows are made possible by using Docker. In this course, we'll be focusing on the first one: how to use Docker Engine and Docker Compose to standardize your dev environment and get it up and running on any machine in just a few minutes. On the next page, we'll walk you through getting a pre-built dev environment running on your computer, then in the next few lessons we'll teach you how to "dockerize" your own projects.


# Project 1: Using Docker to Set Up a Development Environment Locally

We've set up a project so that you can see how easy Docker makes set-up for someone new to your code base.

Below we'll walk you through the steps of getting your first Docker environment up and running. After each step, we'll let you know if you did it right and that it's safe to move onto the next one. 

* Clone the GitHub Repo (or download and extract the code) [here](link/for/the/future).
* Use the command line to navigate to the repo.
* Run `docker compose up` in the base directory.
* When it's done running, go to `localhost` in your browser—it should show you the app!
* Now go back to the repository, and change `file_x.code`.
* Refresh `localhost`—the changes should show up instantly.
* Run `docker compose down` and go back to `localhost`. The app isn't running. 
* Check `docker ps`. The images should all be run down.
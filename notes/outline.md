# Getting Started with Docker

## Why Docker?

- Get up and running with code quickly.
- Guaranteed to work no matter the computer you're using.
- Speed up iteration time.
  + http://it20.info/2016/01/how-is-your-shopping-experience-related-to-docker/
- Share your project easily.
  + Docker Hub

## First Lab: Running Dev Environment

* Run docker app with docker-compose
    - go to demo code directory
    - run `$ docker-compose up -d`
      - may take some time to run
      - verified by app
    - User verify that docker containers are started and running. `$docker ps -a` (add expected output, see 2 containers running elasticsearch and web-app)
* Run demo application
    - From your browser, visit `http://localhost:5000` to see running app
    - Perform search
* Edit code, see it instantly by mounting user volume
    - Change CSS in `flask-app/static/styles/mail.css`
    - Modify Static text  `/Users/inyoungcho/docker/FoodTrucks/flask-app/static/src/components/Intro.js` with Bla-Bla-Blah.
    - Verify the changes you have made are reflected


# Setting up your own project

## What is Docker? (Containers & Images)

- How Docker works
  + https://docs.docker.com/engine/understanding-docker/
  - What is a container?
- What is an image (non-abstractly)?
  - What kind of file?
  - Where is it stored.
  - etc.
  - Image management (building/downloading/deleting)
- Writing a dockerfile
  + https://docs.docker.com/engine/reference/builder/
- Building the image
  - Go through all the components of a Dockerfile
  - Walk through how the current app works.

## Image Lab: Build a Dockerfile for an existing code base.

* Walk thru Demo App Architecture
  - Add Architectural Diagram with each components
  - Examine code FoodTrucks/flask-app/app.py
* `git checkout undockerized` to start the project.
* Dockerize Web-app  
  - Write a dockerfile for a project
    - instructions for writing docker files
  - Build the image (`docker build`), test it (`docker run`)
* Set-up Web app manually in command line.
  - build your own flask container
`docker network create foodtrucks`
  - start the ES container
`docker run -d --net foodtrucks -p 9200:9200 -p 9300:9300 --name es elasticsearch`
  - start the flask app container
`docker run -d --net foodtrucks -p 5000:5000 --name foodtrucks-web prakhar1989/foodtrucks-web`
  - Learn commands needed to get it up and running correctly—database container, networking, etc.


## What is Docker Compose?

- What does compose do?
  + https://docs.docker.com/compose/overview/
  - how does it work non-abstractly?
- Why use compose?
- Writing a compose file.
  - Go over syntax, `image, command, ports, volumes, links`
- Running `docker compose up` as part of the dev cycle

## Compose Lab
* Write a compose file
  - Create docker-compose.yml files
    - Defining services
    - Calling the proper images (official vs. user)
    - Opening ports
    - Mounting volumes (how/why)
    - Linking images together so they can communicate
  - **Validate compose file for student in app?**
* Run compose, test it.
  - `docker-compose up -d`
  - `docker ps -a`
* Change code, test code.


## Conclusion, Summary, + Links to more info

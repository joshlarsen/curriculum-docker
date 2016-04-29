# Getting Started with Docker

## Why Docker?

- Get up and running with code quickly.
- Guaranteed to work no matter the computer you're using.
- Speed up iteration time.
  + http://it20.info/2016/01/how-is-your-shopping-experience-related-to-docker/
- Share your project easily.
  + Docker Hub

## First Lab: Running Dev Environment

* Download code from GitHub.
  - Open docker-compose.yaml file and find out the port number where app is running.
* `docker compose up`
    - run `$ docker-compose up`
* Run demo application
    - Visit localhost with port to run app
    - Run search
* Edit code, see it instantly by mounting user volume
    - Change CSS in `flask-app/static/styles/mail.css`
    - Modify Static text in `/Users/inyoungcho/docker/FoodTrucks/flask-app/static/src/components/Intro.js` with Bla-Bla-Blah.
    - Verify the changes you have made


# Setting up your own project

## What is Docker? (Containers & Images)

- How Docker works
  + https://docs.docker.com/engine/understanding-docker/
- Writing a dockerfile
  + https://docs.docker.com/engine/reference/builder/
- Building the image

## Image Lab: Build a Dockerfile for an existing code base.

* Walk thru Demo App Architecture
  - Add Architectural Diagram with each components
  - Examine code FoodTrucks/flask-app/app.py
* Create your project workspace and code.
  - Checkout `undockerized` branch
  - Create project directory `your_project_name`
  - Copy the existing web-app code from FoodTrucks/flask-app/
  - Open FoodTrucks/flask-app/requirements.txt to see required software libraries and tools.
* Dockerize Web-app  
  - Write a dockerfile for a project
  - Build the image (`docker build`), test it (`docker run`)
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
- Why use compose?
- Writing a compose file.
- Running `docker compose up` as part of the dev cycle

## Compose Lab
* Write a compose file
  - Create docker-compose.yaml files
  - Go over syntax, `image, command, prots, volumes, links`
* Run compose, test it.
* Change code, test code.


## Conclusion, Summary, + Links to more info

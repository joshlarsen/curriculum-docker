# Getting Started with Docker

## Why Docker?

- Get up and running with code quickly.
- Guaranteed to work no matter the computer you're using.
- Speed up iteration time.
  + http://it20.info/2016/01/how-is-your-shopping-experience-related-to-docker/
- Share your project easily.
  + Docker Hub

## First Lab: 2-minute Dev Environment

* Download code from GitHub.
* `docker compose up`
* Visit localhost to use app
* Edit code, see it instantly by mounting user volume

# Setting up your own project

## What is Docker? (Containers & Images)

- How Docker works
  + https://docs.docker.com/engine/understanding-docker/
- Writing a dockerfile
  + https://docs.docker.com/engine/reference/builder/
- Building the image

## Image Lab: Build a Dockerfile for an existing code base.

- Checkout `undockerized` branch
- Write a dockerfile for a project
- Build the image (`docker build`), test it (`docker run`)
- Learn commands needed to get it up and running correctly—database container, networking, etc.


## What is Docker Compose?

- What does compose do?
  + https://docs.docker.com/compose/overview/
- Why use compose?
- Writing a compose file.
- Running `docker compose up` as part of the dev cycle

## Compose Lab

- Write a compose file
- Run compose, test it.
- Change code, test code. 


## Conclusion, Summary, + Links to more info
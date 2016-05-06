# Pre-Course Set-up

1. Wants to learn about Docker
2. Docker.com
3. "Download Docker for Mac to Learn More"
4. Download and Install Docker to Mac
5. Pop-up on Install: "Would you like to learn more?" -> YES
6. Wheelhouse Web App opens in browser.
7. Log in using DockerID.
8. Redirects to First Page of Course.
9. Instructions on running the learning container. (aka Lab.0)
  + `docker run wheelhouse`
  + log in to DockerID in the container
    * VERIFIED -> Click next to continue

# Lesson 1: Getting Started with Docker

## Content 1.1: Why Docker?

- Get up and running with code quickly.
- Guaranteed to work no matter the computer you're using.
- Speed up iteration time.
  + http://it20.info/2016/01/how-is-your-shopping-experience-related-to-docker/
- Share your project easily.
  + Docker Hub
- What is `docker-compose` command?

## Lab 1.2: Running Dev Environment

* Run docker app with docker-compose
    - go to demo code directory
    - run `$ docker-compose up -d`  
        - (Note: I suggest to build new image prakhar1989/foodtrucks-web with docker beta in training container, this will save time to download, the downloaded version may not work in docker beta) 
      - may take some time to run
      - verified by running app
    - User verify that docker containers are started and running. `$docker ps -a` (add expected output, see 2 containers running elasticsearch and web-app)
* Run demo application
    - From your browser, visit `http://localhost:5000` to see running app
    - Perform search 
* Edit static code, see it instantly by mounting user volume
    - From training container, Change CSS in `flask-app/static/styles/main.css`
        - change text color from #aaa to #ac39fd
           (`html, body {
              padding: 0;
              color: #ac39fd;
              box-sizing: border-box;
              font-family: 'Titillium Web', sans-serif;
              margin: 0;)
             }`)
        - change heading color from to #ac39fd 
            (`div#heading {
               background: #ac39fd;
               margin: 0;
              height: 10vh;
              text-align: center;
              }`)
    - Verify the changes you have made are reflected on localhost:5000 and perform search
* See volume /opt is mounted in web container properly and seen from training container as a local directory.
    - Goto foodtrucks-web container `docker exec -i -t <container ID for prakhar1989/foodtrucks-web>`
    - create a file `touch newFile` from `foodtrucks-web` container
    - Goto training container, verify this  `newFile` exists
* Check the volume is created 
    - `docker volume ls` 
* Check the network is created for foodtrucks 
    - `docker network ls`
* Inspect docker container 
    - `docker inspect <container ID for prakhar1989/foodtrucks-web>`


# Lesson 2: Setting up your own project

## Content 2.1: What is Docker? (Containers & Images)

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

## Lab 2.2: Build a Dockerfile for an existing code base.

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


## Content 2.3: What is Docker Compose?

- What does compose do?
  + https://docs.docker.com/compose/overview/
  - how does it work non-abstractly?
- Why use compose?
- Writing a compose file.
  - Go over syntax, `image, command, ports, volumes, links`
- Running `docker compose up` as part of the dev cycle

## Lab 2.4: Compose Lab
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
* Change code, change docker-compose.yaml to build new image, test code.
  - Modify Static java script code,  ~/flask-app/static/src/components/Intro.js
      - (Note: We need to build as this javascript code is minified during build) 
  - change docker-compose.yaml `web: image: prakhar1989/foodtrucks-web` to `web: build: . `
  - run `docker-compose up`
  - Verify on browser. 

# Lesson 3: Conclusion, Summary, + Links to more info
